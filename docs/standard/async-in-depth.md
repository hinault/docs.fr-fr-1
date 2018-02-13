---
title: "Async en détail"
description: "Découvrez comme il est simple d’écrire du code asynchrone utilisant des E/S et le processeur avec le modèle asynchrone .NET basé sur des tâches."
keywords: .NET, .NET Core, .NET Standard
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1e38f9d9-8f84-46ee-a15f-199aec4f2e34
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: b23a90de991b31005ba5a07a959c717c24869ffb
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="async-in-depth"></a>Async en détail

L’écriture de code asynchrone utilisant des E/S et le processeur est simple avec le modèle asynchrone .NET basé sur des tâches. Le modèle est exposé par les types `Task` et `Task<T>` et les mots clés `async` et `await` en C# et Visual Basic. (Les ressources propres à chaque langage se trouvent dans la section [Voir aussi](#see-also).) Cet article explique comment utiliser le code asynchrone .NET et fournit un aperçu du framework asynchrone utilisé en coulisses.

## <a name="task-and-tasklttgt"></a>Task et Task&lt;T&gt;

Les tâches sont des constructions utilisées pour implémenter ce que l’on appelle le [modèle de promesses de concurrence](https://en.wikipedia.org/wiki/Futures_and_promises).  En bref, elles vous offrent la « promesse » que le travail sera terminé à un moment ultérieur, ce qui vous permet de coordonner la promesse et une nouvelle API.

*   `Task` représente une opération unique qui ne retourne pas de valeur.
*   `Task<T>` représente une opération unique qui retourne une valeur de type `T`.

Il est important de considérer les tâches comme des abstractions de travail effectuées de manière asynchrone et *pas* comme une abstraction sur le modèle de thread. Par défaut, les tâches s’exécutent sur le thread actuel et délèguent le travail au système d’exploitation, comme il convient. Éventuellement, l’API `Task.Run` peut servir à demander explicitement aux tâches de s’exécuter sur un thread distinct.

Les tâches exposent un protocole d’API pour surveiller et attendre la valeur de résultat d’une tâche et y accéder (dans le cas de `Task<T>`). L’intégration au langage, avec le mot clé `await`, fournit une abstraction de niveau supérieur pour l’utilisation des tâches. 

L’utilisation de `await` permet à votre application ou service d’effectuer un travail utile pendant l’exécution d’une tâche en cédant le contrôle à son appelant jusqu’à ce que la tâche soit terminée. Votre code n’a pas besoin de s’appuyer sur des rappels ou des événements pour continuer l’exécution une fois la tâche terminée. L’intégration des API de langage et de tâche s’en charge pour vous. Si vous utilisez `Task<T>`, le mot clé `await` « désencapsule » également la valeur retournée quand la tâche est terminée.  Les détails de ce fonctionnement sont expliqués plus bas.

Pour en savoir plus sur les tâches et les différentes façons d’interagir avec elles, lisez la rubrique [Modèle asynchrone basé sur les tâches (TAP, Task-based Asynchronous Pattern)](~/docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).

## <a name="deeper-dive-into-tasks-for-an-io-bound-operation"></a>Approfondissement : Tâches pour une opération utilisant des E/S

La section suivante décrit en détail toutes les étapes d’un appel d’E/S asynchrone standard. Commençons par deux exemples.

Le premier exemple appelle une méthode async et retourne une tâche active qui n’est pas encore terminée.

```csharp
public Task<string> GetHtmlAsync()
{
    // Execution is synchronous here
    var client = new HttpClient();
    
    return client.GetStringAsync("http://www.dotnetfoundation.org");
}
```

Le deuxième exemple ajoute l’utilisation des mots clés `async` et `await` pour agir sur la tâche.

```csharp
public async Task<string> GetFirstCharactersCountAsync(string url, int count)
{
    // Execution is synchronous here
    var client = new HttpClient();
    
    // Execution of GetFirstCharactersCountAsync() is yielded to the caller here
    // GetStringAsync returns a Task<string>, which is *awaited*
    var page = await client.GetStringAsync("http://www.dotnetfoundation.org");
    
    // Execution resumes when the client.GetStringAsync task completes,
    // becoming synchronous again.
    
    if (count > page.Length)
    {
        return page;
    }
    else
    {
        return page.Substring(0, count);
    }
}
```

L’appel de `GetStringAsync()` s’effectue par le biais de bibliothèques .NET de niveau inférieur (peut-être en appelant d’autres méthodes async) jusqu’à ce qu’il atteigne un appel interop P/Invoke dans une bibliothèque de réseau native. La bibliothèque native peut ensuite effectuer un appel de l’API système (tel que `write()` pour un socket sur Linux). Un objet de tâche est créé dans la limite native/managée, éventuellement à l’aide de [TaskCompletionSource](xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult(%600)). L’objet de tâche est transmis à travers les couches, éventuellement traité ou directement retourné, ou retourné à l’appelant initial. 

Dans le deuxième exemple ci-dessus, un objet `Task<T>` est retourné par `GetStringAsync`. L’utilisation du mot clé `await` indique à la méthode de retourner un objet de tâche nouvellement créé. Le contrôle retourne à l’appelant à partir de cet emplacement dans la méthode `GetFirstCharactersCountAsync`. Les méthodes et propriétés de l’objet [Task&lt;T&gt;](xref:System.Threading.Tasks.Task%601) permettent aux appelants de surveiller la progression de la tâche, qui se termine quand le code restant dans GetFirstCharactersCountAsync a été exécuté.

Après l’appel de l’API système, la demande se trouve dans l’espace du noyau et transite vers le sous-système de réseau du système d’exploitation (comme `/net` dans le noyau Linux).  Ici, le système d’exploitation gère la demande de mise en réseau de manière *asynchrone*.  Les détails peuvent être différents selon le système d’exploitation utilisé (l’appel du pilote de périphérique peut être planifié comme un signal envoyé au runtime, ou il peut être effectué et *ensuite* un signal est renvoyé), mais finalement le runtime est informé que la demande de mise en réseau est en cours.  À ce stade, le travail du pilote de périphérique est planifié, en cours ou déjà terminé (la demande est déjà « sur le réseau »), mais parce que tout se passe de manière asynchrone, le pilote de périphérique est en mesure de gérer immédiatement autre chose !

Par exemple, dans Windows, un thread de système d’exploitation effectue un appel au pilote de périphérique réseau et lui demande d’effectuer l’opération de mise en réseau via un paquet de requêtes d’interruption qui représente l’opération.  Le pilote de périphérique reçoit le paquet de requêtes d’interruption, effectue l’appel au réseau, marque le paquet comme étant « en attente » et le renvoie au système d’exploitation.  Le thread du système d’exploitation sait maintenant que le paquet de requêtes d’interruption est « en attente », il n’a donc rien d’autre à faire pour ce travail et « revient » pour pouvoir être utilisé pour une autre opération.

Quand la demande est satisfaite et que les données reviennent à travers le pilote de périphérique, il avertit le processeur que de nouvelles données sont reçues via une interruption.  La façon dont cette interruption est gérée varie selon le système d’exploitation, mais les données sont ensuite transmises au système d’exploitation jusqu’à ce que se produise un appel d’interopérabilité système (par exemple, dans Linux, un gestionnaire d’interruptions planifie la moitié inférieure de l’IRQ pour qu’elle transmette les données via le système d’exploitation de façon asynchrone).  Notez que cela se produit *également* de façon asynchrone !  Le résultat est placé en file d’attente jusqu’à ce que le prochain thread disponible soit en mesure d’exécuter la méthode async et de « désencapsuler » le résultat de la tâche effectuée.

Tout au long de ce processus, un élément clé à retenir est qu’**aucun thread n’est dédié à l’exécution de la tâche**.  Bien que le travail soit exécuté dans un contexte (c’est-à-dire que le système d’exploitation doit passer des données à un pilote de périphérique et répondre à une interruption), aucun thread n’est destiné à *attendre* le retour des données de la demande.  Cela permet au système de gérer une plus grande quantité de travail au lieu d’attendre la fin des appels d’E/S.

Bien que les étapes ci-dessus puissent donner l’impression d’un grand nombre d’opérations à effectuer, en termes de durée totale d’exécution, ce n’est rien comparé au temps nécessaire pour effectuer le travail d’E/S réel. Voici une vague idée de ce que pourrait être la chronologie de ces étapes :

0-1————————————————————————————————————————————————–2-3

*   La durée entre les points `0` et `1` représente tout ce qui se passe avant qu’une méthode async cède le contrôle à son appelant.
*   La durée entre les points `1` et `2` représente le temps consacré aux E/S, sans coût de processeur.
*   Enfin, la durée entre les points `2` et `3` représente le temps consacré à rendre le contrôle (et éventuellement une valeur) à la méthode async, moment à partir duquel elle s’exécute à nouveau.

### <a name="what-does-this-mean-for-a-server-scenario"></a>Qu’est-ce que cela signifie dans un scénario de serveur ?

Ce modèle fonctionne correctement avec la charge de travail d’un scénario de serveur classique.  Comme aucun thread n’est destiné à s’interrompre sur les tâches non terminées, le pool de threads serveur peut traiter un plus grand nombre de demandes web.

Prenons deux serveurs : l’un d’eux exécute du code asynchrone et l’autre pas.  Pour les besoins de cet exemple, chaque serveur n’a que 5 threads disponibles pour traiter les demandes.  Notez que ces chiffres sont intentionnellement petits et servent uniquement dans un contexte de démonstration.

Supposons que les deux serveurs reçoivent 6 demandes simultanées. Chaque demande effectue une opération d’E/S.  Le serveur *sans* code asynchrone doit placer en file d’attente la 6ème demande jusqu’à ce que l’un des 5 threads ait terminé le travail utilisant des E/S et écrit une réponse. Quand la 20ème demande arrive, le serveur commence peut-être à ralentir, car la file d’attente devient trop longue.

Le serveur *avec* code asynchrone peut placer en file d’attente la 6ème demande, mais parce qu’il utilise `async` et `await`, chacun de ses threads est libéré quand le travail utilisant des E/S démarre, et non quand il se termine.  Quand la 20ème demande arrive, la file d’attente des demandes entrantes est bien plus petite (ou est totalement vide) et le serveur ne ralentit pas.

Bien qu’il s’agisse d’un exemple fictif, il fonctionne de manière très similaire dans le monde réel.  En réalité, un serveur est capable de gérer un nombre bien plus important de demandes à l’aide de `async` et `await` que s’il dédiait un thread à chaque demande qu’il reçoit.

### <a name="what-does-this-mean-for-client-scenario"></a>Qu’est-ce que cela signifie dans un scénario de client ?

Le plus gros avantage de l’utilisation de `async` et `await` pour une application cliente est l’augmentation de la réactivité.  Même si vous pouvez améliorer la réactivité d’une application en gérant manuellement des threads de manière dynamique, c’est une opération coûteuse par rapport à la simple utilisation de `async` et `await`.  Dans le cas particulier d’un jeu mobile, il est essentiel d’affecter aussi peu que possible le thread d’interface utilisateur en ce qui concerne les E/S.

Plus important encore, parce que le travail utilisant des E/S ne se sert pratiquement pas du processeur, en dédiant un thread de processeur entier pour effectuer vaguement des tâches utiles, vous utilisez mal vos ressources.

Par ailleurs, la répartition du travail sur le thread d’interface utilisateur (par exemple, la mise à jour d’une interface utilisateur) est très simple avec des méthodes `async` et n’engendre pas de travail supplémentaire (par exemple, l’appel d’un délégué thread-safe).

## <a name="deeper-dive-into-task-and-taskt-for-a-cpu-bound-operation"></a>Approfondissement : Task et Task<T> pour une opération utilisant le processeur

Le code `async` utilisant le processeur est un peu différent du code `async` utilisant des E/S.  Comme le travail est effectué sur le processeur, il n’est pas possible de dédier un thread au calcul.  L’utilisation de `async` et `await` est un moyen d’interagir avec un thread en arrière-plan et de faire en sorte que l’appelant de la méthode async reste réactif.  Notez que cela ne protège en rien les données partagées.  Si vous utilisez des données partagées, vous devez quand même appliquer une stratégie de synchronisation appropriée.

Voici une vue générale d’un appel asynchrone utilisant le processeur :

```csharp
public async Task<int> CalculateResult(InputData data)
{
    // This queues up the work on the threadpool.
    var expensiveResultTask = Task.Run(() => DoExpensiveCalculation(data));
    
    // Note that at this point, you can do some other work concurrently,
    // as CalculateResult() is still executing!
    
    // Execution of CalculateResult is yielded here!
    var result = await expensiveResultTask;
    
    return result;
}
```

`CalculateResult()` s’exécute sur le thread sur lequel il a été appelé.  Quand il appelle `Task.Run`, il place en file d’attente l’opération coûteuse qui utilise le processeur, `DoExpensiveCalculation()`, sur le pool de threads et reçoit un handle `Task<int>`.  `DoExpensiveCalculation()` est finalement exécuté simultanément sur le prochain thread disponible, probablement sur un autre cœur d’UC.  Il est possible d’effectuer des tâches simultanées quand `DoExpensiveCalculation()` est occupé sur un autre thread, car le thread qui a appelé `CalculateResult()` est encore en cours d’exécution.

Une fois que `await` a été trouvé, l’exécution de `CalculateResult()` est cédée à son appelant, ce qui permet d’effectuer d’autres tâches avec le thread actuel pendant que `DoExpensiveCalculation()` produit un résultat.  Une fois cette opération terminée, le résultat est placé en file d’attente pour s’exécuter sur le thread principal.  Finalement, le thread principal retourne à l’exécution de `CalculateResult()`, à partir duquel il obtient le résultat de `DoExpensiveCalculation()`.

### <a name="why-does-async-help-here"></a>Pourquoi async est-il utile ici ?

`async` et `await` sont la meilleure approche pour gérer les travaux utilisant l’UC quand vous avez besoin de réactivité. Il existe plusieurs modèles d’utilisation d’async avec des tâches utilisant le processeur. Notez que l’utilisation d’async représente un coût, même s’il est faible, et qu’elle n’est donc pas recommandée pour les boucles serrées.  C’est à vous de déterminer la façon dont vous écrivez votre code autour de cette nouvelle fonctionnalité.

## <a name="see-also"></a>Voir aussi

[Programmation asynchrone en C#](~/docs/csharp/async.md)   
[Programmation asynchrone en F#](~/docs/fsharp/tutorials/asynchronous-and-concurrent-programming/async.md)   
[Programmation asynchrone avec Async et Await (Visual Basic)](~/docs/visual-basic/programming-guide/concepts/async/index.md)
