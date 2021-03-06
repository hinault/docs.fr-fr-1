---
title: "Génération d’une bibliothèque de classes avec Visual Basic et .NET Core dans Visual Studio 2017"
description: "Découvrez comment créer une bibliothèque de classes écrite en Visual Basic à l’aide de Visual Studio 2017"
keywords: ".NET Core, bibliothèque de classes .NET Standard, Visual Studio 2017, Visual Basic"
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-vb
dev_langs: vb
ms.workload: dotnetcore
ms.openlocfilehash: b8d87e3a97e2ffeb8e8712bfa5d178bb855f402d
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="building-a-class-library-with-visual-basic-and-net-core-in-visual-studio-2017"></a>Génération d’une bibliothèque de classes avec Visual Basic et .NET Core dans Visual Studio 2017

Une *bibliothèque de classes* définit des types et des méthodes qui peuvent être appelés par une application. Une bibliothèque de classes qui cible .NET Standard 2.0 permet à votre bibliothèque d’être appelée par n’importe quelle implémentation .NET qui prend en charge cette version de .NET Standard. Quand vous avez terminé votre bibliothèque de classes, vous pouvez décider de la distribuer ou non comme un composant tiers, ou de l’inclure ou non dans un composant groupé avec une ou plusieurs applications.

> [!NOTE]
> Pour obtenir la liste des versions de .NET Standard et des plateformes prises en charge, consultez [.NET Standard](../../standard/net-standard.md).

Dans cette rubrique, vous créez une bibliothèque d’utilitaire simple qui contient une seule méthode de gestion de chaîne. Vous l’implémentez en tant que [méthode d’extension](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md), pour pouvoir l’appeler comme s’il s’agissait d’un membre de la classe <xref:System.String>.

## <a name="creating-a-class-library-solution"></a>Création d'une solution de bibliothèque de classes

Commencez par créer une solution pour votre projet de bibliothèque de classes et ses projets connexes. Une solution Visual Studio sert simplement de conteneur pour un ou plusieurs projets. Pour créer la solution :

1. Dans la barre de menus de Visual Studio, choisissez **Fichier** > **Nouveau** > **Projet**.

1. Dans la boîte de dialogue **Nouveau projet**, développez le nœud **Autres types de projets** et sélectionnez **Solutions Visual Studio**. Nommez la solution « ClassLibraryProjects » puis sélectionnez le bouton **OK**.

   ![Boîte de dialogue Nouveau projet](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a>Création du projet de bibliothèque de classes

Créez votre projet de bibliothèque de classes :

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur la solution **ClassLibraryProjects** et, dans le menu contextuel, sélectionnez **Ajouter** > **Nouveau projet**.

1. Dans la boîte de dialogue **Ajouter un nouveau projet**, développez le nœud **Visual Basic**, puis sélectionnez le nœud **.NET Standard** et choisissez le modèle de projet **Bibliothèque de classes (.NET Standard)**. Dans la zone de texte **Nom**, entrez « StringLibrary » comme nom de projet. Sélectionnez **OK** pour créer le projet de bibliothèque de classes.

   ![Boîte de dialogue Ajouter un nouveau projet](./media/vb-library-with-visual-studio/libproject.png)

   Ensuite, la fenêtre de code s’ouvre dans l’environnement de développement Visual Studio. 
 
   ![Fenêtre d’application Visual Studio montrant le code du modèle de bibliothèque de classes par défaut](./media/vb-library-with-visual-studio/stringlibrary.png)

1. Vérifiez que notre bibliothèque cible la version appropriée de .NET Standard. Dans la fenêtre **Explorateur de solutions**, cliquez avec le bouton droit sur le projet de bibliothèque, puis sélectionnez **Propriétés**. La zone de texte **framework cible** indique que nous ciblons .NET Standard 2.0.

   ![Propriétés de projet pour la bibliothèque de classes](./media/library-with-visual-studio/properties.png)

1. Dans la boîte de dialogue **Propriétés**, effacez le texte de la zone de texte **Espace de noms racine**. Pour chaque projet, Visual Basic crée automatiquement un espace de noms qui correspond au nom du projet, et tous les espaces de noms définis dans les fichiers de code source sont des parents de cet espace de noms. Nous souhaitons définir un espace de noms de niveau supérieur à l’aide du mot clé [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md).
  
1. Remplacez le code de la fenêtre de code par le code suivant et enregistrez le fichier :

  [!CODE-vb[ClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/stringlibrary.vb)]

   La bibliothèque de classes, `UtilityLibraries.StringLibrary`, contient une méthode nommée `StartsWithUpper`, qui retourne une valeur <xref:System.Boolean> qui indique si l’instance actuelle de la chaîne commence par une majuscule. La norme Unicode distingue les caractères minuscules des caractères majuscules. La méthode <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> retourne `true` si un caractère est en majuscule.

1. Dans la barre de menus, sélectionnez **Générer** > **Générer la solution**. Le projet devrait être compilé sans erreur.

   ![Volet de sortie indiquant que la génération a réussi](./media/library-with-visual-studio/buildsucceeds.png)



## <a name="next-step"></a>Étape suivante

Vous avez créé la bibliothèque correctement. Comme vous n’avez appelé aucune de ses méthodes, vous ne savez pas si elle fonctionne comme prévu. L’étape suivante du développement de votre bibliothèque consiste à la tester en utilisant un [Projet de test unitaire](testing-library-with-visual-studio.md).
