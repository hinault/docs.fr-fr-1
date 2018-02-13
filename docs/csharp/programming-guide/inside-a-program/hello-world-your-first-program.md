---
title: Hello World -- Votre premier programme (guide de programmation C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: get-started-article
f1_keywords:
- cs.program
- vs.csharp.startpage.firstapplication
helpviewer_keywords:
- examples [C#], Hello World
- Hello World example [C#]
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
caps.latest.revision: "39"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 1b6511394e69edd344c4f4a1bbc9da549a1a2a17
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="hello-world----your-first-program-c-programming-guide"></a>Hello World -- Votre premier programme (guide de programmation C#)
La procédure suivante crée une version C# du traditionnel programme « Hello World ! » . Le programme affiche la chaîne `Hello World!`  
  
 Pour plus d’exemples concernant les concepts de base, consultez [Bien démarrer avec Visual Basic et Visual C#](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-and-run-a-console-application"></a>Pour créer et exécuter une application console  
  
1.  Démarrez Visual Studio.  
  
2.  Dans la barre de menus, sélectionnez **Fichier**, **Nouveau**, **Projet**.  
  
     La boîte de dialogue **Nouveau projet** s'affiche.  
  
3.  Développez **Installé**, **Modèles**, **Visual C#**, puis choisissez **Application console**.  
  
4.  Dans la zone de texte **Nom**, entrez un nom pour votre projet, puis choisissez le bouton **OK**.  
  
     Le nouveau projet s’affiche dans l’**Explorateur de solutions**.  
  
5.  Si Program.cs n’est pas ouvert dans l’**Éditeur de Code**, ouvrez le menu contextuel de **Program.cs** dans **l’Explorateur de solutions**, puis choisissez **Afficher le code**.  
  
6.  Remplacez le contenu de Program.cs par le code suivant.  
  
     [!code-csharp[csProgGuide#21](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_1.cs)]  
  
7.  Appuyez sur la touche F5 pour exécuter le projet. Une fenêtre d’invite de commandes s’affiche avec la ligne `Hello World!`  
  
 Ensuite, les parties importantes de ce programme sont examinées.  
  
## <a name="comments"></a>Commentaires  
 La première ligne contient un commentaire. Les caractères `//` convertissent le reste de la ligne en un commentaire.  
  
 [!code-csharp[csProgGuide#32](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_2.cs)]  
  
 Vous pouvez également créer un commentaire à partir d’un bloc de texte en le plaçant entre les caractères `/*` et `*/`. L'exemple suivant le démontre.  
  
 [!code-csharp[csProgGuide#33](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_3.cs)]  
  
## <a name="main-method"></a>Méthode Main  
 Une application console C# doit contenir une méthode `Main`, dans laquelle le contrôle commence et termine. C’est dans la méthode `Main` que vous créez des objets et exécutez d’autres méthodes.  
  
 La méthode `Main` est une méthode [static](../../../csharp/language-reference/keywords/static.md) qui réside dans une classe ou un struct. Dans l’exemple « Hello World ! » précédent, il réside dans une classe nommée `Hello`. Vous pouvez déclarer la méthode `Main` de l’une des façons suivantes :  
  
-   Elle peut retourner `void`.  
  
     [!code-csharp[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_4.cs)]  
  
-   Elle peut également retourner un entier.  
  
     [!code-csharp[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_5.cs)]  
  
-   Elle peut accepter des arguments avec n’importe quel type de retour.  
  
     [!code-csharp[csProgGuideMain#19](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_6.cs)]  
  
     - ou -  
  
     [!code-csharp[csProgGuideMain#18](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_7.cs)]  
  
 Le paramètre `args` de la méthode `Main` est un tableau `string` qui contient les arguments de la ligne de commande utilisés pour appeler le programme. Contrairement au langage C++, le tableau n’inclut pas le nom du fichier exécutable (exe).  
  
 Pour plus d’informations sur l’utilisation des arguments de ligne de commande, consultez les exemples des rubriques [Main() et arguments de ligne de commande](../../../csharp/programming-guide/main-and-command-args/index.md) et [Guide pratique pour créer et utiliser des assemblys à l’aide de la ligne de commande](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4).  
  
 L’appel à <xref:System.Console.ReadKey%2A> à la fin de la méthode `Main` empêche la fenêtre de console de se fermer avant que vous ayez pu lire la sortie quand vous exécutez votre programme en mode débogage, avec la touche F5.  
  
## <a name="input-and-output"></a>Entrées et sorties  
 Les programmes C# utilisent généralement les services d’entrée/sortie fournis par la bibliothèque runtime du .NET Framework. L’instruction `System.Console.WriteLine("Hello World!");` utilise la méthode <xref:System.Console.WriteLine%2A>. C’est l’une des méthodes de sortie de la classe <xref:System.Console> de la bibliothèque runtime. Elle affiche son paramètre de chaîne dans le flux de sortie standard suivi d’une nouvelle ligne. D’autres méthodes <xref:System.Console> sont disponibles pour différentes opérations d’entrée et de sortie. Si vous incluez la directive `using System;` au début du programme, vous pouvez utiliser directement les classes et les méthodes <xref:System> sans les qualifier complètement. Par exemple, vous pouvez appeler `Console.WriteLine` au lieu de `System.Console.WriteLine` :  
  
 [!code-csharp[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_8.cs)]  
  
 [!code-csharp[csProgGuide#23](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_9.cs)]  
  
 Pour plus d’informations sur les méthodes d’entrée/sortie, consultez <xref:System.IO>.  
  
## <a name="command-line-compilation-and-execution"></a>Compilation et exécution en ligne de commande  
 Vous pouvez compiler le programme « Hello World ! » à l’aide de la ligne de commande au lieu de l’environnement de développement intégré (IDE) Visual Studio.  
  
#### <a name="to-compile-and-run-from-a-command-prompt"></a>Pour compiler et exécuter à partir d’une invite de commandes  
  
1.  Copiez-collez le code de la procédure précédente dans un éditeur de texte, puis enregistrez le fichier en tant que fichier texte. Nommez le fichier `Hello.cs`. Les fichiers de code source C# utilisent l’extension `.cs`.  
  
2.  Effectuez l’une des opérations suivantes pour ouvrir une fenêtre d’invite de commandes :  
  
    -   Dans Windows 10, dans le menu **Démarrer**, recherchez `Developer Command Prompt`, puis choisissez **Invite de commandes développeur pour VS 2017**.  
  
         Une fenêtre d’invite de commandes développeur s’affiche.  
  
    -   Dans Windows 7, ouvrez le menu **Démarrer**, développez le dossier de la version actuelle de Visual Studio, ouvrez le menu contextuel de **Visual Studio Tools**, puis choisissez **Invite de commandes de développeur de VS 2017**.  
  
         Une fenêtre d’invite de commandes développeur s’affiche.  
  
    -   Activez les générations en mode ligne de commande à partir d’une fenêtre d’invite de commandes standard.  
  
         Consultez [Guide pratique pour définir des variables d’environnement pour la ligne de commande Visual Studio](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md).  
  
3.  Dans la fenêtre d’invite de commandes, accédez au dossier qui contient le fichier `Hello.cs`.  
  
4.  Entrez la commande suivante pour compiler `Hello.cs`.  
  
     `csc Hello.cs`  
  
     Si votre programme ne contient pas d’erreurs de compilation, un fichier exécutable nommé `Hello.exe` est créé.  
  
5.  Dans la fenêtre d’invite de commandes, entrez la commande suivante pour exécuter le programme :  
  
     `Hello`  
  
 Pour plus d’informations sur le compilateur C# et ses options, consultez [Options du compilateur C #](../../../csharp/language-reference/compiler-options/index.md).
  
## <a name="see-also"></a>Voir aussi  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [À l’intérieur d’un programme C#](../../../csharp/programming-guide/inside-a-program/index.md)  
 [Chaînes](../../../csharp/programming-guide/strings/index.md)  
 [\<paveover>Exemples d’applications C#](http://msdn.microsoft.com/library/9a9d7aaa-51d3-4224-b564-95409b0f3e15)  
 [Référence C#](../../../csharp/language-reference/index.md)  
 [Main() et arguments de ligne de commande](../../../csharp/programming-guide/main-and-command-args/index.md)  
 [Bien démarrer avec Visual Basic et Visual C#](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)
