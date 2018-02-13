---
title: "Gestion de la réentrance dans Async Apps (C#)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: 47c5075e-c448-45ce-9155-ed4e7e98c677
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 07157057d7ae94d3c6017544ff654ca0ed7b7cf2
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="handling-reentrancy-in-async-apps-c"></a>Gestion de la réentrance dans Async Apps (C#)
Quand vous incluez du code asynchrone dans votre application, vous devez prendre en compte et éventuellement empêcher la réentrance, qui fait référence à une nouvelle entrée d'une opération asynchrone avant qu'elle soit terminée. Si vous n'identifiez pas et ne gérez pas les possibilités de réentrance, les résultats peuvent être inattendus.  
  
 **Dans cette rubrique**  
  
-   [Identification de la réentrance](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Gestion de la réentrance](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Désactiver le bouton Démarrer](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Annuler et redémarrer l’opération](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Exécuter plusieurs opérations et mettre la sortie en file d’attente](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Examen et exécution de l’exemple d’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
> [!NOTE]
>  Pour exécuter l’exemple, Visual Studio version 2012, ou une version ultérieure, et .NET Framework version 4.5, ou une version ultérieure, doivent être installés sur votre ordinateur.  
  
##  <a name="BKMK_RecognizingReentrancy"></a> Identification de la réentrance  
 Dans l’exemple de cette rubrique, les utilisateurs choisissent un bouton **Démarrer** pour lancer une application asynchrone qui télécharge une série de sites web et calcule le nombre total d’octets téléchargés. Une version synchrone de l’exemple répondrait de la même façon quel que soit le nombre de fois où un utilisateur clique sur le bouton car, après la première fois, le thread d’interface utilisateur ignore ces événements jusqu’à ce que l’application arrête de s’exécuter. Dans une application asynchrone, en revanche, le thread d'interface utilisateur continue de répondre et vous pouvez entrer à nouveau l'opération asynchrone avant qu'elle soit terminée.  
  
 L’exemple suivant illustre la sortie attendue si l’utilisateur choisit le bouton **Démarrer** une seule fois. La liste des sites web téléchargés apparaît avec la taille, en octets, de chaque site. Le nombre total d'octets apparaît à la fin.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Toutefois, si l'utilisateur choisit le bouton plusieurs fois, le gestionnaire d'événements est appelé à plusieurs reprises et le processus de téléchargement est à nouveau entré à chaque fois. Ainsi, plusieurs opérations asynchrones s'exécutent en même temps, la sortie entrelace les résultats et le nombre total d'octets est source de confusion.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
7. msdn.microsoft.com                                            42972  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
7. msdn.microsoft.com                                            42972  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Vous pouvez passer en revue le code qui produit cette sortie en accédant à la fin de cette rubrique. Vous pouvez faire des essais avec le code en téléchargeant la solution sur votre ordinateur local, puis en exécutant le projet WebsiteDownload ou en utilisant le code donné à la fin de cette rubrique pour créer votre propre projet. Pour plus d’informations et d’instructions, consultez [Examen et exécution de l’exemple d’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645).  
  
##  <a name="BKMK_HandlingReentrancy"></a> Gestion de la réentrance  
 Vous pouvez gérer la réentrance de différentes façons, selon ce que vous voulez que votre application fasse. Cette rubrique présente les exemples suivants :  
  
-   [Désactiver le bouton Démarrer](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Désactivez le bouton **Démarrer** pendant que l’opération est en cours d’exécution afin que l’utilisateur ne puisse pas l’interrompre.  
  
-   [Annuler et redémarrer l’opération](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Annulez toute opération encore en cours d’exécution quand l’utilisateur choisit le bouton **Démarrer** à nouveau, puis laissez l’opération demandée le plus récemment continuer.  
  
-   [Exécuter plusieurs opérations et mettre la sortie en file d’attente](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Autorisez toutes les opérations demandées à s'exécuter de façon asynchrone, mais coordonnez l'affichage de la sortie de sorte que les résultats de chaque opération apparaissent ensemble et dans l'ordre.  
  
###  <a name="BKMK_DisableTheStartButton"></a> Désactiver le bouton Démarrer  
 Vous pouvez bloquer le bouton **Démarrer** pendant l’exécution d’une opération en désactivant le bouton en haut du gestionnaire d’événements `StartButton_Click`. Ensuite, vous pouvez réactiver le bouton depuis un bloc `finally` quand l'opération se termine pour que les utilisateurs puissent exécuter à nouveau l'application.  
  
 Le code suivant illustre ces modifications, marquées par des astérisques. Vous pouvez ajouter les modifications apportées au code à la fin de cette rubrique, ou vous pouvez télécharger l’application finalisée dans la rubrique [Exemples Async : la réentrance dans les applications de bureau .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Le nom du projet est DisableStartButton.  
  
```csharp  
private async void StartButton_Click(object sender, RoutedEventArgs e)  
{  
    // This line is commented out to make the results clearer in the output.  
    //ResultsTextBox.Text = "";  
  
    // ***Disable the Start button until the downloads are complete.   
    StartButton.IsEnabled = false;   
  
    try  
    {  
        await AccessTheWebAsync();  
    }  
    catch (Exception)  
    {  
        ResultsTextBox.Text += "\r\nDownloads failed.";  
    }  
    // ***Enable the Start button in case you want to run the program again.   
    finally  
    {  
        StartButton.IsEnabled = true;  
    }  
}  
```  
  
 Suite aux modifications, le bouton ne répond pas pendant que `AccessTheWebAsync` télécharge les sites Web, donc le processus ne peut pas être entré de nouveau.  
  
###  <a name="BKMK_CancelAndRestart"></a> Annuler et redémarrer l’opération  
 Au lieu de désactiver le bouton **Démarrer**, vous pouvez garder le bouton actif. Toutefois, si l’utilisateur choisit de nouveau ce bouton, annulez l’opération qui est déjà en cours d’exécution et laissez continuer l’opération le plus récemment démarrée.  
  
 Pour plus d’informations sur l’annulation, consultez [Réglage de votre application Async (C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md).  
  
 Pour configurer ce scénario, apportez les modifications suivantes au code de base fourni dans [Examen et exécution de l’exemple d’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645). Vous pouvez également télécharger l’application finalisée dans la rubrique [Exemples Async : la réentrance dans les applications de bureau .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Le nom de ce projet est CancelAndRestart.  
  
1.  Déclarez une variable <xref:System.Threading.CancellationTokenSource>, `cts`, qui est dans la portée de toutes les méthodes.  
  
    ```csharp  
    public partial class MainWindow : Window   // Or class MainPage  
    {  
        // *** Declare a System.Threading.CancellationTokenSource.  
        CancellationTokenSource cts;  
    ```  
  
2.  Dans `StartButton_Click`, déterminez si une opération est déjà en cours d'exécution. Si la valeur de `cts` est Null, aucune opération n’est active. Si la valeur n'est pas null, l'opération qui est déjà en cours d'exécution est annulée.  
  
    ```csharp  
    // *** If a download process is already underway, cancel it.  
    if (cts != null)  
    {  
        cts.Cancel();  
    }  
    ```  
  
3.  Définissez `cts` sur une autre valeur qui représente le processus en cours.  
  
    ```csharp  
    // *** Now set cts to a new value that you can use to cancel the current process  
    // if the button is chosen again.  
    CancellationTokenSource newCTS = new CancellationTokenSource();  
    cts = newCTS;  
    ```  
  
4.  À la fin de `StartButton_Click`, le processus en cours est terminé, donc redéfinissez la valeur `cts` sur null.  
  
    ```csharp  
    // *** When the process is complete, signal that another process can begin.  
    if (cts == newCTS)  
        cts = null;  
    ```  
  
 Le code suivant illustre toutes les modifications dans `StartButton_Click` : Les ajouts sont marqués par des astérisques.  
  
```csharp  
private async void StartButton_Click(object sender, RoutedEventArgs e)  
{  
    // This line is commented out to make the results clearer in the output.  
    //ResultsTextBox.Clear();  
  
    // *** If a download process is already underway, cancel it.  
    if (cts != null)  
    {  
        cts.Cancel();  
    }  
  
    // *** Now set cts to cancel the current process if the button is chosen again.  
    CancellationTokenSource newCTS = new CancellationTokenSource();  
    cts = newCTS;  
  
    try  
    {  
        // ***Send cts.Token to carry the message if there is a cancellation request.  
        await AccessTheWebAsync(cts.Token);  
  
    }  
    // *** Catch cancellations separately.  
    catch (OperationCanceledException)  
    {  
        ResultsTextBox.Text += "\r\nDownloads canceled.\r\n";  
    }  
    catch (Exception)  
    {  
        ResultsTextBox.Text += "\r\nDownloads failed.\r\n";  
    }  
    // *** When the process is complete, signal that another process can proceed.  
    if (cts == newCTS)  
        cts = null;  
}  
```  
  
 Dans `AccessTheWebAsync`, apportez les modifications suivantes.  
  
-   Ajoutez un paramètre pour accepter le jeton d'annulation en provenance de `StartButton_Click`.  
  
-   Utilisez la méthode <xref:System.Net.Http.HttpClient.GetAsync%2A> pour télécharger les sites Web car `GetAsync` accepte un argument <xref:System.Threading.CancellationToken>.  
  
-   Avant d'appeler `DisplayResults` pour afficher les résultats de chaque site Web téléchargé, vérifiez `ct` pour vous assurer que l'opération en cours n'a pas été annulée.  
  
 Le code suivant illustre ces modifications, marquées par des astérisques.  
  
```csharp  
// *** Provide a parameter for the CancellationToken from StartButton_Click.  
async Task AccessTheWebAsync(CancellationToken ct)  
{  
    // Declare an HttpClient object.  
    HttpClient client = new HttpClient();  
  
    // Make a list of web addresses.  
    List<string> urlList = SetUpURLList();  
  
    var total = 0;  
    var position = 0;  
  
    foreach (var url in urlList)  
    {  
        // *** Use the HttpClient.GetAsync method because it accepts a   
        // cancellation token.  
        HttpResponseMessage response = await client.GetAsync(url, ct);  
  
        // *** Retrieve the website contents from the HttpResponseMessage.  
        byte[] urlContents = await response.Content.ReadAsByteArrayAsync();  
  
        // *** Check for cancellations before displaying information about the   
        // latest site.   
        ct.ThrowIfCancellationRequested();  
  
        DisplayResults(url, urlContents, ++position);  
  
        // Update the total.  
        total += urlContents.Length;  
    }  
  
    // Display the total count for all of the websites.  
    ResultsTextBox.Text +=  
        string.Format("\r\n\r\nTOTAL bytes returned:  {0}\r\n", total);  
}     
```  
  
 Si vous choisissez le bouton **Démarrer** plusieurs fois pendant l’exécution de cette application, les résultats produits doivent ressembler à la sortie suivante.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               122505  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Pour éliminer les listes partielles, supprimez les commentaires de la première ligne de code dans `StartButton_Click` pour effacer la zone de texte chaque fois que l'utilisateur redémarre l'opération.  
  
###  <a name="BKMK_RunMultipleOperations"></a> Exécuter plusieurs opérations et mettre la sortie en file d’attente  
 Ce troisième exemple est le plus compliqué, car l’application démarre une autre opération asynchrone chaque fois que l’utilisateur choisit le bouton **Démarrer**, et toutes les opérations s’exécutent jusqu’à leur achèvement. Toutes les opérations demandées téléchargent des sites web de la liste de façon asynchrone, mais la sortie des opérations est présentée séquentiellement. Autrement dit, l’activité de téléchargement réelle est entrelacée, comme le montre la sortie dans [Identification de la réentrance](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), mais la liste des résultats de chaque groupe est présentée séparément.  
  
 Les opérations partagent un <xref:System.Threading.Tasks.Task> global, `pendingWork`, qui sert d'opérateur de contrôle d'appels pour le processus d'affichage.  
  
 Vous pouvez exécuter cet exemple en collant les modifications dans le code indiqué dans [Génération de l’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), ou vous pouvez suivre les instructions données dans [Téléchargement de l’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) pour télécharger l’exemple, puis exécuter le projet QueueResults.  
  
 La sortie suivante montre le résultat obtenu si l’utilisateur choisit le bouton **Démarrer** une seule fois. L’étiquette A indique que le résultat part de la première fois que le bouton **Démarrer** est choisi. Les numéros indiquent l'ordre des URL dans la liste des cibles de téléchargement.  
  
```  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               209858  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
A-7. msdn.microsoft.com                                            53266  
A-8. msdn.microsoft.com/library/ff730837.aspx               148020  
  
TOTAL bytes returned:  918876  
  
#Group A is complete.  
```  
  
 Si l’utilisateur choisit le bouton **Démarrer** trois fois, l’application produit une sortie semblable aux lignes suivantes. Les lignes d'information qui commencent par un signe dièse (#) suivent la progression de l'application.  
  
```  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71259  
A-6. msdn.microsoft.com/library/ms404677.aspx               199185  
  
#Starting group B.  
#Task assigned for group B.  
  
A-7. msdn.microsoft.com                                            53266  
  
#Starting group C.  
#Task assigned for group C.  
  
A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916095  
  
B-1. msdn.microsoft.com/library/hh191443.aspx                87389  
B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
  
#Group A is complete.  
  
B-7. msdn.microsoft.com                                            53266  
B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916097  
  
C-1. msdn.microsoft.com/library/hh191443.aspx                87389  
C-2. msdn.microsoft.com/library/aa578028.aspx               207089  
  
#Group B is complete.  
  
C-3. msdn.microsoft.com/library/jj155761.aspx                30870  
C-4. msdn.microsoft.com/library/hh290140.aspx               119027  
C-5. msdn.microsoft.com/library/hh524395.aspx                72765  
C-6. msdn.microsoft.com/library/ms404677.aspx               199186  
C-7. msdn.microsoft.com                                            56190  
C-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  920526  
  
#Group C is complete.  
```  
  
 Les groupes B et C démarrent avant que le groupe A ait terminé, mais la sortie de chaque groupe apparaît séparément. Toute la sortie du groupe A apparaît en premier, suivie de toute la sortie du groupe B, puis de toute la sortie du groupe C. L’application affiche toujours les groupes dans l’ordre et, pour chaque groupe, elle affiche toujours les informations sur les sites web, dans l’ordre où les URL apparaissent dans la liste des URL.  
  
 Toutefois, vous ne pouvez pas prévoir l'ordre dans lequel les téléchargements se produisent réellement. Après le démarrage de plusieurs groupes, les tâches de téléchargement qu'ils génèrent sont toutes actives. Vous ne pouvez pas supposer que A-1 sera téléchargé avant B-1 ni que A-1 sera téléchargé avant A-2.  
  
#### <a name="global-definitions"></a>Définitions globales  
 L'exemple de code contient les deux déclarations globales suivantes qui sont visibles à partir de toutes les méthodes.  
  
```csharp  
public partial class MainWindow : Window  // Class MainPage in Windows Store app.  
{  
    // ***Declare the following variables where all methods can access them.   
    private Task pendingWork = null;     
    private char group = (char)('A' - 1);  
```  
  
 La variable `Task`, `pendingWork`, supervise le processus d'affichage et empêche tout groupe d'interrompre l'opération d'affichage d'un autre groupe. La variable de caractère `group`, étiquette la sortie de différents groupes pour vérifier que les résultats apparaissent dans l'ordre attendu.  
  
#### <a name="the-click-event-handler"></a>Gestionnaire d'événements Click  
 Le gestionnaire d’événements, `StartButton_Click`, incrémente la lettre du groupe chaque fois que l’utilisateur choisit le bouton **Démarrer**. Ensuite, le gestionnaire appelle `AccessTheWebAsync` pour exécuter l'opération de téléchargement.  
  
```csharp  
private async void StartButton_Click(object sender, RoutedEventArgs e)  
{  
    // ***Verify that each group's results are displayed together, and that  
    // the groups display in order, by marking each group with a letter.  
    group = (char)(group + 1);  
    ResultsTextBox.Text += string.Format("\r\n\r\n#Starting group {0}.", group);  
  
    try  
    {  
        // *** Pass the group value to AccessTheWebAsync.  
        char finishedGroup = await AccessTheWebAsync(group);  
  
        // The following line verifies a successful return from the download and  
        // display procedures.   
        ResultsTextBox.Text += string.Format("\r\n\r\n#Group {0} is complete.\r\n", finishedGroup);  
    }  
    catch (Exception)  
    {  
        ResultsTextBox.Text += "\r\nDownloads failed.";  
    }  
}  
```  
  
#### <a name="the-accessthewebasync-method"></a>Méthode AccessTheWebAsync  
 Cet exemple fractionne `AccessTheWebAsync` en deux méthodes. La première méthode, `AccessTheWebAsync`, démarre toutes les tâches de téléchargement d'un groupe et configure `pendingWork` pour contrôler le processus d'affichage. La méthode utilise une requête LINQ (Language Integrated Query) et <xref:System.Linq.Enumerable.ToArray%2A> pour démarrer toutes les tâches de téléchargement en même temps.  
  
 `AccessTheWebAsync` appelle ensuite `FinishOneGroupAsync` pour attendre la fin de chaque téléchargement et en afficher la longueur.  
  
 `FinishOneGroupAsync` retourne une tâche assignée à `pendingWork` dans `AccessTheWebAsync`. Cette valeur empêche toute interruption par une autre opération avant que la tâche ne soit terminée.  
  
```csharp  
private async Task<char> AccessTheWebAsync(char grp)  
{  
    HttpClient client = new HttpClient();  
  
    // Make a list of the web addresses to download.  
    List<string> urlList = SetUpURLList();  
  
    // ***Kick off the downloads. The application of ToArray activates all the download tasks.  
    Task<byte[]>[] getContentTasks = urlList.Select(url => client.GetByteArrayAsync(url)).ToArray();  
  
    // ***Call the method that awaits the downloads and displays the results.  
    // Assign the Task that FinishOneGroupAsync returns to the gatekeeper task, pendingWork.  
    pendingWork = FinishOneGroupAsync(urlList, getContentTasks, grp);  
  
    ResultsTextBox.Text += string.Format("\r\n#Task assigned for group {0}. Download tasks are active.\r\n", grp);  
  
    // ***This task is complete when a group has finished downloading and displaying.  
    await pendingWork;  
  
    // You can do other work here or just return.  
    return grp;  
}  
```  
  
#### <a name="the-finishonegroupasync-method"></a>Méthode FinishOneGroupAsync  
 Cette méthode parcourt les tâches de téléchargement dans un groupe, en attendant chacune d’elles, en affichant la longueur du site web téléchargé et en ajoutant la longueur au total.  
  
 La première instruction dans `FinishOneGroupAsync` utilise `pendingWork` pour vérifier que l’entrée de la méthode n’interfère pas avec une opération qui est déjà dans le processus d’affichage ou qui est déjà en train d’attendre. Si une telle opération est en cours, l'opération d'entrée doit attendre son tour.  
  
```csharp  
private async Task FinishOneGroupAsync(List<string> urls, Task<byte[]>[] contentTasks, char grp)  
{  
    // ***Wait for the previous group to finish displaying results.  
    if (pendingWork != null) await pendingWork;  
  
    int total = 0;  
  
    // contentTasks is the array of Tasks that was created in AccessTheWebAsync.  
    for (int i = 0; i < contentTasks.Length; i++)  
    {  
        // Await the download of a particular URL, and then display the URL and  
        // its length.  
        byte[] content = await contentTasks[i];  
        DisplayResults(urls[i], content, i, grp);  
        total += content.Length;  
    }  
  
    // Display the total count for all of the websites.  
    ResultsTextBox.Text +=  
        string.Format("\r\n\r\nTOTAL bytes returned:  {0}\r\n", total);  
}  
```  
  
 Vous pouvez exécuter cet exemple en collant les modifications dans le code indiqué dans [Génération de l’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), ou vous pouvez suivre les instructions données dans [Téléchargement de l’application](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) pour télécharger l’exemple, puis exécuter le projet QueueResults.  
  
#### <a name="points-of-interest"></a>Points d'intérêt  
 Les lignes d'information qui commencent par un signe dièse (#) dans la sortie clarifient le fonctionnement de cet exemple.  
  
 La sortie affiche les modèles suivants.  
  
-   Un groupe peut être démarré pendant qu'un groupe précédent affiche sa sortie, mais l'affichage de la sortie du groupe précédent n'est pas interrompu.  
  
    ```  
    #Starting group A.  
    #Task assigned for group A. Download tasks are active.  
  
    A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
    A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
    A-4. msdn.microsoft.com/library/hh290140.aspx               119037  
    A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
  
    A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    A-7. msdn.microsoft.com                                            53078  
    A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915919  
  
    B-1. msdn.microsoft.com/library/hh191443.aspx                87388  
    B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
  
    #Group A is complete.  
  
    B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
    B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
    B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    B-7. msdn.microsoft.com                                            53078  
    B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915908  
    ```  
  
-   La tâche `pendingWork` est Null au début de `FinishOneGroupAsync` uniquement pour le groupe A, qui a démarré en premier. Le groupe A n'a pas encore terminé une expression await quand il atteint `FinishOneGroupAsync`. Par conséquent, le contrôle n'a pas retourné à `AccessTheWebAsync`, et la première assignation à `pendingWork` ne s'est pas produite.  
  
-   Les deux lignes suivantes apparaissent toujours ensemble dans la sortie. Le code n'est jamais interrompu entre le démarrage d'une opération de groupe dans `StartButton_Click` et l'affectation d'une tâche pour le groupe à `pendingWork`.  
  
    ```  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
    ```  
  
     Une fois qu'un groupe entre `StartButton_Click`, l'opération ne termine pas une expression await tant que l'opération n'entre pas `FinishOneGroupAsync`. Par conséquent, aucune autre opération ne peut obtenir le contrôle au cours de ce segment de code.  
  
##  <a name="BKMD_SettingUpTheExample"></a> Examen et exécution de l’exemple d’application  
 Pour mieux comprendre l’exemple d’application, vous pouvez le télécharger, le créer vous-même ou passer en revue le code à la fin de cette rubrique sans implémenter l’application.  
  
> [!NOTE]
>  Pour exécuter l’exemple comme une application de bureau WPF, Visual Studio version 2012, ou une version ultérieure, et .NET Framework version 4.5, ou une version ultérieure, doivent être installés sur votre ordinateur.  
  
###  <a name="BKMK_DownloadingTheApp"></a> Téléchargement de l’application  
  
1.  Téléchargez le fichier compressé dans la rubrique [Exemples Async : la réentrance dans les applications de bureau .NET](http://go.microsoft.com/fwlink/?LinkId=266571).  
  
2.  Décompressez le fichier que vous avez téléchargé, puis démarrez Visual Studio.  
  
3.  Dans la barre de menus, choisissez **Fichier**, **Ouvrir**, **Projet/Solution**.  
  
4.  Accédez au dossier qui contient l’exemple de code décompressé, puis ouvrez le fichier solution (.sln).  
  
5.  Dans l’**Explorateur de solutions**, ouvrez le menu contextuel du projet à modifier, puis choisissez **Définir comme StartUpProject**.  
  
6.  Appuyez sur les touches CTRL+F5 pour générer et exécuter le projet.  
  
###  <a name="BKMK_BuildingTheApp"></a> Génération de l’application  
 La section suivante fournit le code pour générer l’exemple comme une application WPF.  
  
##### <a name="to-build-a-wpf-app"></a>Pour générer une application WPF  
  
1.  Démarrez Visual Studio.  
  
2.  Dans la barre de menus, sélectionnez **Fichier**, **Nouveau**, **Projet**.  
  
     La boîte de dialogue **Nouveau projet** s'affiche.  
  
3.  Dans le volet **Modèles installés**, développez **Visual C#**, puis développez **Windows**.  
  
4.  Dans la liste des types de projets, choisissez **Application WPF**.  
  
5.  Nommez le projet `WebsiteDownloadWPF`, puis cliquez sur le bouton **OK**.  
  
     Le nouveau projet s’affiche dans l’**Explorateur de solutions**.  
  
6.  Dans l'éditeur de code Visual Studio, choisissez l'onglet **MainWindow.xaml** .  
  
     Si l’onglet n’est pas visible, ouvrez le menu contextuel de MainWindow.xaml dans l’**Explorateur de solutions**, puis choisissez **Afficher le code**.  
  
7.  Dans la vue **XAML** de MainWindow.xaml, remplacez le code par le code suivant.  
  
    ```csharp  
    <Window x:Class="WebsiteDownloadWPF.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:local="using:WebsiteDownloadWPF"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
        mc:Ignorable="d">  
  
        <Grid Width="517" Height="360">  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="-1,0,0,0" VerticalAlignment="Top" Click="StartButton_Click" Height="53" Background="#FFA89B9B" FontSize="36" Width="518"  />  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" Margin="-1,53,0,-36" TextWrapping="Wrap" VerticalAlignment="Top" Height="343" FontSize="10" ScrollViewer.VerticalScrollBarVisibility="Visible" Width="518" FontFamily="Lucida Console" />  
        </Grid>  
    </Window>  
    ```  
  
     Une fenêtre simple contenant une zone de texte et un bouton apparaît dans la vue **Design** de MainWindow.xaml.  
  
8.  Ajoutez une référence pour <xref:System.Net.Http>.  
  
9. Dans l’**Explorateur de solutions**, ouvrez le menu contextuel pour MainWindow.xaml.cs, puis choisissez **Afficher le code**.  
  
10. Dans MainWindow.xaml.cs, remplacez le code par le code suivant.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Data;  
    using System.Windows.Documents;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    using System.Windows.Media.Imaging;  
    using System.Windows.Navigation;  
    using System.Windows.Shapes;  
  
    // Add the following using directives, and add a reference for System.Net.Http.  
    using System.Net.Http;  
    using System.Threading;  
  
    namespace WebsiteDownloadWPF  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            private async void StartButton_Click(object sender, RoutedEventArgs e)  
            {  
                // This line is commented out to make the results clearer in the output.  
                //ResultsTextBox.Text = "";  
  
                try  
                {  
                    await AccessTheWebAsync();  
                }  
                catch (Exception)  
                {  
                    ResultsTextBox.Text += "\r\nDownloads failed.";  
                }  
            }  
  
            private async Task AccessTheWebAsync()  
            {  
                // Declare an HttpClient object.  
                HttpClient client = new HttpClient();  
  
                // Make a list of web addresses.  
                List<string> urlList = SetUpURLList();  
  
                var total = 0;  
                var position = 0;  
  
                foreach (var url in urlList)  
                {  
                    // GetByteArrayAsync returns a task. At completion, the task  
                    // produces a byte array.  
                    byte[] urlContents = await client.GetByteArrayAsync(url);  
  
                    DisplayResults(url, urlContents, ++position);  
  
                    // Update the total.  
                    total += urlContents.Length;  
                }  
  
                // Display the total count for all of the websites.  
                ResultsTextBox.Text +=  
                    string.Format("\r\n\r\nTOTAL bytes returned:  {0}\r\n", total);  
            }  
  
            private List<string> SetUpURLList()  
            {  
                List<string> urls = new List<string>   
                {   
                    "http://msdn.microsoft.com/library/hh191443.aspx",  
                    "http://msdn.microsoft.com/library/aa578028.aspx",  
                    "http://msdn.microsoft.com/library/jj155761.aspx",  
                    "http://msdn.microsoft.com/library/hh290140.aspx",  
                    "http://msdn.microsoft.com/library/hh524395.aspx",  
                    "http://msdn.microsoft.com/library/ms404677.aspx",  
                    "http://msdn.microsoft.com",  
                    "http://msdn.microsoft.com/library/ff730837.aspx"  
                };  
                return urls;  
            }  
  
            private void DisplayResults(string url, byte[] content, int pos)  
            {  
                // Display the length of each website. The string format is designed  
                // to be used with a monospaced font, such as Lucida Console or   
                // Global Monospace.  
  
                // Strip off the "http://".  
                var displayURL = url.Replace("http://", "");  
                // Display position in the URL list, the URL, and the number of bytes.  
                ResultsTextBox.Text += string.Format("\n{0}. {1,-58} {2,8}", pos, displayURL, content.Length);  
            }  
        }  
    }  
    ```  
  
11. Appuyez sur les touches CTRL+F5 pour exécuter le programme, puis choisissez le bouton **Démarrer** plusieurs fois.  
  
12. Apportez les modifications indiquées dans [Désactiver le bouton Démarrer](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), [Annuler et redémarrer l’opération](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) ou [Exécuter plusieurs opérations et mettre la sortie en file d’attente](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) pour gérer la réentrance.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédure pas à pas : accès au web avec Async et Await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)  
 [Programmation asynchrone avec Async et Await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)
