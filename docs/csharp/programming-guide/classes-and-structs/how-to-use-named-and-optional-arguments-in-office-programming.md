---
title: "Guide pratique pour utiliser des arguments nommés et facultatifs dans la programmation Office (Guide de programmation C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- named and optional arguments [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
caps.latest.revision: "34"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: fc3c0f6910238ba20582280426b4a40e68b95dd8
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-use-named-and-optional-arguments-in-office-programming-c-programming-guide"></a>Guide pratique pour utiliser des arguments nommés et facultatifs dans la programmation Office (Guide de programmation C#)
Les arguments nommés et les arguments facultatifs, qui ont été introduits avec [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)], rendent la programmation en C# plus pratique, plus souple et plus lisible. De plus, ces fonctionnalités facilitent considérablement l’accès aux interfaces COM, telles que les API Microsoft Office Automation.  
  
 Dans l’exemple suivant, la méthode [ConvertToTable](https://msdn.microsoft.com/library/bb216993.aspx) a seize paramètres qui représentent les caractéristiques d’une table, comme le nombre de colonnes et de lignes, la mise en forme, les bordures, les polices et les couleurs. Ces seize paramètres sont facultatifs, car la plupart du temps, il n’est pas nécessaire de spécifier des valeurs pour chacun d’eux. Toutefois, en l’absence d’arguments nommés et facultatifs, une valeur ou une valeur d’espace réservé doit être fournie pour chaque paramètre. Avec les arguments nommés et facultatifs, vous spécifiez des valeurs uniquement pour les paramètres qui sont nécessaires à votre projet.  
  
 Pour que vous puissiez effectuer ces procédures, Microsoft Office Word doit être installé sur votre ordinateur.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-new-console-application"></a>Pour créer une application console  
  
1.  Démarrez Visual Studio.  
  
2.  Dans le menu **Fichier** , pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
3.  Dans le volet **Catégories de modèles**, développez **Visual C#**, puis cliquez sur **Windows**.  
  
4.  Regardez en haut du volet **Modèles** pour vérifier que **.NET Framework 4**, ou version ultérieure, apparaît dans la zone **Framework cible**.  
  
5.  Dans le volet **Modèles**, cliquez sur **Application console**.  
  
6.  Attribuez un nom à votre projet dans le champ **Nom**.  
  
7.  Cliquez sur **OK**.  
  
     Le nouveau projet s’affiche dans l’**Explorateur de solutions**.  
  
### <a name="to-add-a-reference"></a>Pour ajouter une référence  
  
1.  Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nom de votre projet, puis cliquez sur **Ajouter une référence**. La boîte de dialogue **Ajouter une référence** s’affiche.  
  
2.  Dans la page **.NET**, sélectionnez **Microsoft.Office.Interop.Word** dans la liste **Nom du composant**.  
  
3.  Cliquez sur **OK**.  
  
### <a name="to-add-necessary-using-directives"></a>Pour ajouter les directives using nécessaires  
  
1.  Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le fichier **Program.cs**, puis cliquez sur **Afficher le code**.  
  
2.  Ajoutez les directives `using` suivantes en début du fichier de code.  
  
     [!code-csharp[csProgGuideNamedAndOptional#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_1.cs)]  
  
### <a name="to-display-text-in-a-word-document"></a>Pour afficher du texte dans un document Word  
  
1.  Dans la classe `Program` du fichier Program.cs, ajoutez la méthode suivante pour créer une application Word et un document Word. La méthode [Add](https://msdn.microsoft.com/library/microsoft.office.interop.word.documents.add.aspx) comprend quatre paramètres facultatifs. Cet exemple utilise leurs valeurs par défaut. Par conséquent, aucun argument n’est nécessaire dans l’instruction appelante.  
  
     [!code-csharp[csProgGuideNamedAndOptional#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_2.cs)]  
  
2.  Ajoutez le code suivant à la fin de la méthode pour définir l’emplacement d’affichage du texte dans le document, ainsi que le texte à afficher.  
  
     [!code-csharp[csProgGuideNamedAndOptional#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_3.cs)]  
  
### <a name="to-run-the-application"></a>Pour exécuter l’application  
  
1.  Ajoutez l’instruction suivante à Main.  
  
     [!code-csharp[csProgGuideNamedAndOptional#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_4.cs)]  
  
2.  Appuyez sur CTRL+F5 pour exécuter le projet. Un document Word contenant le texte spécifié s’affiche.  
  
### <a name="to-change-the-text-to-a-table"></a>Pour convertir le texte en tableau  
  
1.  Utilisez la méthode `ConvertToTable` pour inclure le texte dans un tableau. La méthode comprend seize paramètres facultatifs. IntelliSense place les paramètres facultatifs entre crochets, comme illustré dans l’exemple suivant.  
  
     ![Liste des paramètres de la méthode ConvertToTable.](../../../csharp/programming-guide/classes-and-structs/media/convert_tableparameters.png "Convert_TableParameters")  
Paramètres ConvertToTable  
  
     Les arguments nommés et facultatifs permettent de spécifier des valeurs uniquement pour les paramètres que vous voulez modifier. Ajoutez le code suivant à la fin de la méthode `DisplayInWord` pour créer un tableau simple. L’argument spécifie que les virgules présentes dans le texte de la chaîne comprise dans `range` séparent les cellules du tableau.  
  
     [!code-csharp[csProgGuideNamedAndOptional#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_5.cs)]  
  
     Dans les versions antérieures du langage C#, l’appel de `ConvertToTable` nécessite un argument de référence pour chaque paramètre, comme indiqué dans le code suivant.  
  
     [!code-csharp[csProgGuideNamedAndOptional#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_6.cs)]  
  
2.  Appuyez sur CTRL+F5 pour exécuter le projet.  
  
### <a name="to-experiment-with-other-parameters"></a>Pour tester d’autres paramètres  
  
1.  Pour modifier le tableau de sorte qu’il comporte une colonne et trois lignes, remplacez la dernière ligne de `DisplayInWord` par l’instruction suivante, puis appuyez sur CTRL+F5.  
  
     [!code-csharp[csProgGuideNamedAndOptional#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_7.cs)]  
  
2.  Pour spécifier un format prédéfini pour le tableau, remplacez la dernière ligne de `DisplayInWord` par l’instruction suivante, puis appuyez sur CTRL + F5. Le format peut être n’importe quelle constante [WdTableFormat](https://msdn.microsoft.com/library/microsoft.office.interop.word.wdtableformat.aspx).  
  
     [!code-csharp[csProgGuideNamedAndOptional#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_8.cs)]  
  
## <a name="example"></a>Exemple  
 Le code suivant contient l’exemple complet.  
  
 [!code-csharp[csProgGuideNamedAndOptional#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_9.cs)]  
  
## <a name="see-also"></a>Voir aussi  
 [Arguments nommés et facultatifs](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)
