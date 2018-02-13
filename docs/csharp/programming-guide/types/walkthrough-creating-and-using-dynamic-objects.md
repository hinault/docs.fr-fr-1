---
title: "Procédure pas à pas : création et utilisation d'objets dynamiques (C# et Visual Basic)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dynamic objects [Visual Basic]
- dynamic objects
- dynamic objects [C#]
ms.assetid: 568f1645-1305-4906-8625-5d77af81e04f
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: eca6da96d3bf9c5c25216e442999be77a332b5c9
ms.sourcegitcommit: 70dcc89737127e4d5f20500242409b687e51b07e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2018
---
# <a name="walkthrough-creating-and-using-dynamic-objects-c-and-visual-basic"></a>Procédure pas à pas : création et utilisation d'objets dynamiques (C# et Visual Basic)

Les objets dynamiques exposent des membres tels que les propriétés et les méthodes au moment de l’exécution et non lors de la compilation. Cela vous permet de créer des objets utilisables avec des structures qui ne correspondent pas à un type ou un format statique. Par exemple, vous pouvez utiliser un objet dynamique pour référencer le modèle DOM (Document Object Model) HTML, qui peut contenir n’importe quelle combinaison d’attributs et d’éléments de balisage HTML valides. Étant donné que chaque document HTML est unique, les membres d’un document HTML particulier sont déterminés au moment de l’exécution. L’une des méthodes courantes pour référencer un attribut d’un élément HTML consiste à passer le nom de l’attribut à la méthode `GetProperty` de l’élément. Pour référencer l’attribut `id` de l’élément HTML `<div id="Div1">`, vous obtenez d’abord une référence à l’élément `<div>`, puis utilisez `divElement.GetProperty("id")`. Si vous utilisez un objet dynamique, vous pouvez référencer l’attribut `id` comme `divElement.id`.  
  
 Les objets dynamiques permettent également d’accéder facilement aux langages dynamiques comme IronPython et IronRuby. Vous pouvez utiliser un objet dynamique pour faire référence à un script dynamique qui est interprété au moment de l’exécution.  
  
 Vous référencez un objet dynamique à l’aide de la liaison tardive. En C#, vous spécifiez le type d’un objet à liaison tardive comme `dynamic`. En [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], vous spécifiez le type d’un objet à liaison tardive comme `Object`. Pour plus d’informations, consultez [dynamic](../../../csharp/language-reference/keywords/dynamic.md) et [Liaison anticipée et liaison tardive](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md).  
  
 Vous pouvez créer des objets dynamiques personnalisés en utilisant les classes contenues dans l’espace de noms <xref:System.Dynamic?displayProperty=nameWithType>. Par exemple, vous pouvez créer un <xref:System.Dynamic.ExpandoObject> et spécifier les membres de cet objet au moment de l’exécution. Vous pouvez aussi créer votre propre type qui hérite de la classe <xref:System.Dynamic.DynamicObject>. Vous pouvez ensuite substituer les membres de la classe <xref:System.Dynamic.DynamicObject> pour fournir des fonctionnalités dynamiques au moment de l’exécution.  
  
 Dans cette procédure pas à pas, vous exécuterez les tâches suivantes :  
  
-   Créer un objet personnalisé qui expose dynamiquement le contenu d’un fichier texte comme propriétés d’un objet.  
  
-   Créer un projet qui utilise une bibliothèque `IronPython`.  
  
## <a name="prerequisites"></a>Prérequis  
Pour effectuer cette procédure pas à pas, vous devez utiliser [IronPython](http://ironpython.net/) pour .NET. Accédez à la [page de téléchargement](http://ironpython.net/download/) pour obtenir la version la plus récente.
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-a-custom-dynamic-object"></a>Création d’un objet dynamique personnalisé  
 Le premier projet que vous créez dans cette procédure pas à pas définit un objet dynamique personnalisé qui recherche dans le contenu d’un fichier texte. Le texte à rechercher est spécifié par le nom d’une propriété dynamique. Par exemple, si le code appelant spécifie `dynamicFile.Sample`, la classe dynamique retourne une liste générique de chaînes qui contient toutes les lignes du fichier qui commencent par « Sample ». La recherche respecte la casse. La classe dynamique prend également en charge deux arguments facultatifs. Le premier argument est une valeur enum de l’option de recherche qui spécifie que la classe dynamique doit rechercher des correspondances en début de ligne, en fin de ligne, ou n’importe où dans la ligne. Le deuxième argument spécifie que la classe dynamique doit supprimer des espaces à gauche et à droite dans chaque ligne avant d’effectuer la recherche. Par exemple, si le code appelant spécifie `dynamicFile.Sample(StringSearchOption.Contains)`, la classe dynamique recherche le terme « Sample » n’importe où dans une ligne. Si le code appelant spécifie `dynamicFile.Sample(StringSearchOption.StartsWith, false)`, la classe dynamique recherche le terme « Sample » au début de chaque ligne et ne supprime ni les espaces à droite, ni les espaces à gauche. Le comportement par défaut de la classe dynamique consiste à rechercher une correspondance au début de chaque ligne et à supprimer les espaces à gauche et à droite.  
  
#### <a name="to-create-a-custom-dynamic-class"></a>Pour créer une classe dynamique personnalisée  
  
1.  Démarrez [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)].  
  
2.  Dans le menu **Fichier** , pointez sur **Nouveau** , puis cliquez sur **Projet**.  
  
3.  Dans la boîte de dialogue **Nouveau projet**, dans le volet **Types de projets**, vérifiez que **Windows** est sélectionné. Sélectionnez **Application console** dans le volet **Modèles**. Dans la zone **Nom**, tapez `DynamicSample`, puis cliquez sur **OK**. Le nouveau projet est créé.  
  
4.  Cliquez avec le bouton droit sur le projet DynamicSample, pointez sur **Ajouter**, puis cliquez sur **Classe**. Dans la zone **Nom**, tapez `ReadOnlyFile`, puis cliquez sur **OK**. Un nouveau fichier contenant la classe ReadOnlyFile est ajouté.  
  
5.  En haut du fichier ReadOnlyFile.cs ou ReadOnlyFile.vb, ajoutez le code suivant pour importer les espaces de noms <xref:System.IO?displayProperty=nameWithType> et <xref:System.Dynamic?displayProperty=nameWithType>.  
  
     [!code-csharp[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_1.cs)]

     [!code-vb[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_1.vb)]  
  
6.  L’objet dynamique personnalisé utilise un enum pour déterminer les critères de recherche. Avant l’instruction de classe, ajoutez la définition d’enum suivante.  
  
     [!code-csharp[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_2.cs)]

     [!code-vb[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_2.vb)]  
  
7.  Mettez à jour l’instruction de classe de façon à hériter de la classe `DynamicObject`, comme indiqué dans l’exemple de code suivant.  
  
     [!code-csharp[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_3.cs)]

     [!code-vb[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_3.vb)]  
  
8.  Ajoutez le code suivant à la classe `ReadOnlyFile` afin de définir un champ privé pour le chemin du fichier et un constructeur pour la classe `ReadOnlyFile`.  
  
     [!code-csharp[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_4.cs)]
     
     [!code-vb[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_4.vb)]  
  
9. Ajoutez la méthode `GetPropertyValue` suivante à la classe `ReadOnlyFile`. La méthode `GetPropertyValue` prend les critères de recherche comme paramètre d’entrée et retourne les lignes d’un fichier texte qui correspondent aux critères de recherche. Les méthodes dynamiques fournies par la classe `ReadOnlyFile` appellent la méthode `GetPropertyValue` pour récupérer leurs résultats respectifs.  
  
     [!code-csharp[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_5.cs)]
     
     [!code-vb[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_5.vb)]  
  
10. Après la méthode `GetPropertyValue`, ajoutez le code suivant pour substituer la méthode <xref:System.Dynamic.DynamicObject.TryGetMember%2A> de la classe <xref:System.Dynamic.DynamicObject>. La méthode <xref:System.Dynamic.DynamicObject.TryGetMember%2A> est appelée quand un membre d’une classe dynamique est demandé et qu’aucun argument n’est spécifié. L’argument `binder` contient les informations relatives au membre référencé et l’argument `result` référence le résultat retourné pour le membre spécifié. La méthode <xref:System.Dynamic.DynamicObject.TryGetMember%2A> retourne une valeur booléenne qui retourne `true` si le membre demandé existe ; sinon, elle retourne la valeur `false`.  
  
     [!code-csharp[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_6.cs)]
     
     [!code-vb[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_6.vb)]  
  
11. Après la méthode `TryGetMember`, ajoutez le code suivant pour substituer la méthode <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> de la classe <xref:System.Dynamic.DynamicObject>. La méthode <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> est appelée quand un membre d’une classe dynamique est demandé avec des arguments. L’argument `binder` contient les informations relatives au membre référencé et l’argument `result` référence le résultat retourné pour le membre spécifié. L’argument `args` contient un tableau des arguments passés au membre. La méthode <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> retourne une valeur booléenne qui retourne `true` si le membre demandé existe ; sinon, elle retourne la valeur `false`.  
  
     La version personnalisée de la méthode `TryInvokeMember` s’attend à ce que le premier argument soit une valeur de l’enum `StringSearchOption` que vous avez défini dans une étape précédente. La méthode `TryInvokeMember` s’attend à ce que le deuxième argument soit une valeur booléenne. Si l’un des arguments ou les deux arguments sont des valeurs valides, ils sont passés à la méthode `GetPropertyValue` pour récupérer les résultats.  
  
     [!code-csharp[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_7.cs)]
     
     [!code-vb[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_7.vb)]  
  
12. Enregistrez et fermez le fichier.  
  
#### <a name="to-create-a-sample-text-file"></a>Pour créer un exemple de fichier texte  
  
1.  Cliquez avec le bouton droit sur le projet DynamicSample, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**. Dans le volet **Modèles installés**, sélectionnez **Général**, puis sélectionnez le modèle **Fichier texte**. Laissez le nom par défaut TextFile1.txt dans la zone **Nom**, puis cliquez sur **Ajouter**. Un nouveau fichier texte est ajouté au projet.  
  
2.  Copiez le texte suivant dans le fichier TextFile1.txt.  
  
    ```  
    List of customers and suppliers  
  
    Supplier: Lucerne Publishing (http://www.lucernepublishing.com/)  
    Customer: Preston, Chris  
    Customer: Hines, Patrick  
    Customer: Cameron, Maria  
    Supplier: Graphic Design Institute (http://www.graphicdesigninstitute.com/)   
    Supplier: Fabrikam, Inc. (http://www.fabrikam.com/)   
    Customer: Seubert, Roxanne  
    Supplier: Proseware, Inc. (http://www.proseware.com/)   
    Customer: Adolphi, Stephan  
    Customer: Koch, Paul  
    ```  
  
3.  Enregistrez et fermez le fichier.  
  
#### <a name="to-create-a-sample-application-that-uses-the-custom-dynamic-object"></a>Pour créer un exemple d’application qui utilise l’objet dynamique personnalisé  
  
1.  Dans l’**Explorateur de solutions**, double-cliquez sur le fichier Module1.vb si vous utilisez [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] ou sur le fichier Program.cs si vous utilisez Visual C#.  
  
2.  Ajoutez le code suivant à la procédure Main pour créer une instance de la classe `ReadOnlyFile` pour le fichier TextFile1.txt. Le code utilise la liaison tardive pour appeler des membres dynamiques et récupérer des lignes de texte qui contiennent la chaîne « Customer ».  
  
     [!code-csharp[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_8.cs)]
     
     [!code-vb[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_8.vb)]  
  
3.  Enregistrez le fichier et appuyez sur CTRL+F5 pour générer et exécuter l’application.  
  
## <a name="calling-a-dynamic-language-library"></a>Appel d’une bibliothèque dynamique de langage  

Le projet suivant que vous créez dans cette procédure pas à pas permet d’accéder à une bibliothèque qui est écrite dans le langage dynamique IronPython.
  
#### <a name="to-create-a-custom-dynamic-class"></a>Pour créer une classe dynamique personnalisée  
  
1.  Dans [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)], dans le menu **Fichier**, pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
2.  Dans la boîte de dialogue **Nouveau projet**, dans le volet **Types de projets**, vérifiez que **Windows** est sélectionné. Sélectionnez **Application console** dans le volet **Modèles**. Dans la zone **Nom**, tapez `DynamicIronPythonSample`, puis cliquez sur **OK**. Le nouveau projet est créé.  
  
3.  Si vous utilisez [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], cliquez avec le bouton droit sur le projet DynamicIronPythonSample, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Références**. Cliquez sur le bouton **Ajouter**. Si vous utilisez Visual C#, dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le dossier **Références**, puis cliquez sur **Ajouter une référence**.  
  
4.  Sous l’onglet **Parcourir**, naviguez jusqu’au dossier dans lequel sont installées les bibliothèques IronPython. Par exemple, C:\Program Files\IronPython 2.6 pour .NET 4.0. Sélectionnez les bibliothèques **IronPython.dll**, **IronPython.Modules.dll**, **Microsoft.Scripting.dll** et **Microsoft.Dynamic.dll**. Cliquez sur **OK**.  
  
5.  Si vous utilisez [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], modifiez le fichier Module1.vb. Si vous utilisez Visual C#, modifiez le fichier Program.cs.  
  
6.  En haut du fichier, ajoutez le code suivant pour importer les espaces de noms `Microsoft.Scripting.Hosting` et `IronPython.Hosting` depuis les bibliothèques IronPython.  
  
     [!code-csharp[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_9.cs)]
     
     [!code-vb[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_9.vb)]  
  
7.  Dans la méthode Main, ajoutez le code suivant pour créer un objet `Microsoft.Scripting.Hosting.ScriptRuntime` pour héberger les bibliothèques IronPython. L’objet `ScriptRuntime` charge le module de bibliothèque IronPython random.py.  
  
     [!code-csharp[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_10.cs)]
     
     [!code-vb[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_10.vb)]  
  
8.  Une fois que le code a chargé le module random.py, ajoutez le code suivant pour créer un tableau d’entiers. Le tableau est passé à la méthode `shuffle` du module random.py, qui trie aléatoirement les valeurs dans le tableau.  
  
     [!code-csharp[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_11.cs)]
     
     [!code-vb[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_11.vb)]  
  
9. Enregistrez le fichier et appuyez sur CTRL+F5 pour générer et exécuter l’application.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Dynamic?displayProperty=nameWithType>  
 <xref:System.Dynamic.DynamicObject?displayProperty=nameWithType>  
 [Utilisation du type dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)  
 [Liaison anticipée et liaison tardive](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)  
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)  
 [Implémentation des interfaces dynamiques (PDF téléchargeable à partir de Microsoft TechNet)](http://download.microsoft.com/download/5/4/B/54B83DFE-D7AA-4155-9687-B0CF58FF65D7/implementing-dynamic-interfaces.pdf)
