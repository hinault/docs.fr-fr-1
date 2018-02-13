---
title: Utilisation de Microsoft XML Serializer Generator sur .NET Core
description: "Vue d’ensemble de Microsoft XML Serializer Generator."
author: mlacouture
manager: wpickett
ms.author: johalex
ms.date: 01/19/2017
ms.topic: tutorial
ms.prod: .net-core
ms.custom: mvc
ms.openlocfilehash: b2f52a068d128b2eb978c9e086508bd87e103ebc
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="using-microsoft-xml-serializer-generator-on-net-core"></a>Utilisation de Microsoft XML Serializer Generator sur .NET Core

Ce didacticiel montre comment utiliser Microsoft XML Serializer Generator dans une application C# .NET Core. Au cours de ce didacticiel, vous apprenez à :

> [!div class="checklist"]
> * Créer une application .NET Core
> * Ajouter une référence au package Microsoft.XmlSerializer.Generator
> * Modifier votre fichier MyApp.csproj pour ajouter des dépendances
> * Ajouter une classe et un XmlSerializer
> * Générer et exécuter l’application 

Comme l’outil [XML Serializer Generator (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) pour le .NET Framework, le [package NuGet Microsoft.XmlSerializer.Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) est l’équivalent pour les projets .NET Core et .NET Standard. Il crée un assembly de sérialisation XML pour les types contenus dans un assembly afin d’améliorer les performances de démarrage de la sérialisation XML pendant la sérialisation ou la désérialisation des objets de ces types avec <xref:System.Xml.Serialization.XmlSerializer>.

## <a name="prerequisites"></a>Prérequis

Pour suivre ce didacticiel :

* Installez le [SDK .NET Core 2.1.3 ou version ultérieure](https://www.microsoft.com/net/download).
* Installez votre éditeur de code favori, si ce n’est pas déjà fait.

> [!TIP]
> Vous avez besoin d’installer un éditeur de code ? Essayez [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) !
  
## <a name="use-microsoft-xml-serializer-generator-in-a-net-core-console-application"></a>Utiliser Microsoft XML Serializer Generator dans une application console .NET Core 

Les instructions suivantes montrent comment utiliser XML Serializer Generator dans une application console .NET Core.

### <a name="create-a-net-core-console-application"></a>Créer une application console .NET Core

Ouvrez une invite de commandes et créez un dossier nommé *MyApp*. Accédez au dossier créé et tapez la commande suivante :

```console
dotnet new console
```

### <a name="add-a-reference-to-the-microsoftxmlserializergenerator-package-in-the-myapp-project"></a>Ajouter une référence au package Microsoft.XmlSerializer.Generator dans le projet MyApp

Utilisez la commande [`dotnet add package`](../tools//dotnet-add-package.md) pour ajouter la référence dans votre projet. 

Type :
 
 ```console
 dotnet add package Microsoft.XmlSerializer.Generator -v 1.0.0
 ```
 
### <a name="verify-changes-to-myappcsproj-after-adding-the-package"></a>Vérifier les modifications apportées à MyApp.csproj après l’ajout du package

Ouvrez votre éditeur de code et c’est parti ! Nous travaillons encore à partir du répertoire *MyApp* dans lequel nous avons créé l’application.

Ouvrez *MyApp.csproj* dans votre éditeur de texte.

Après l’exécution de la commande [`dotnet add package`](../tools//dotnet-add-package.md), les lignes suivantes sont ajoutées à votre fichier projet *MyApp.csproj* :

 ```xml
 <ItemGroup>
    <PackageReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```
 
### <a name="add-another-itemgroup-section-for-net-core-cli-tool-support"></a>Ajouter une autre section ItemGroup pour la prise en charge de l’outil d’interface CLI .NET Core
 
 Ajoutez les lignes suivantes après la section `ItemGroup` que nous avons inspectée :
 
 ```xml
 <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```
 
### <a name="add-a-class-in-the-application"></a>Ajouter une classe dans l’application

Ouvrez *Program.cs* dans votre éditeur de texte. Ajoutez la classe nommée *MyClass* dans *Program.cs*.

```csharp
public class MyClass
{
   public int Value;
}
```

### <a name="create-an-xmlserializer-for-myclass"></a>Créer un `XmlSerializer` pour MyClass

Ajoutez la ligne suivante à l’intérieur de *Main* pour créer un `XmlSerializer` pour MyClass :

```csharp
var serializer = new System.Xml.Serialization.XmlSerializer(typeof(MyClass));
```

### <a name="build-and-run-the-application"></a>Générez et exécutez l'application.

Toujours dans le dossier *MyApp*, exécutez l’application avec [`dotnet run`](../tools/dotnet-run.md). Elle se charge automatiquement et utilise les sérialiseurs prégénérés au moment de l’exécution.

Tapez la commande suivante dans la fenêtre de console :

 ```console
 $ dotnet run
 ```
> [!NOTE]
> [`dotnet run`](../tools/dotnet-run.md) appelle [`dotnet build`](../tools/dotnet-build.md) pour garantir que les cibles de génération ont été générées, puis appelle `dotnet <assembly.dll>` pour exécuter l’application cible.

> [!IMPORTANT]
> Les commandes et les étapes indiquées dans ce didacticiel pour exécuter votre application sont utilisées uniquement au moment du développement. Une fois que vous êtes prêt à déployer votre application, consultez les différentes [stratégies de déploiement](../deploying/index.md) pour les applications .NET Core et la commande [`dotnet publish`](../tools/dotnet-publish.md).

Si tout fonctionne, un assembly nommé *MyApp.XmlSerializers.dll* est généré dans le dossier de sortie. 



Félicitations ! Vous venez de :
> [!div class="checklist"]
> * Créer une application .NET Core
> * Ajouter une référence au package Microsoft.XmlSerializer.Generator
> * Modifier votre fichier MyApp.csproj pour ajouter des dépendances
> * Ajouter une classe et un XmlSerializer
> * Générer et exécuter l’application 

## <a name="related-resources"></a>Ressources connexes

* [Introduction à la sérialisation XML](../../standard/serialization/introducing-xml-serialization.md)
* [Guide pratique pour sérialiser à l’aide de XmlSerializer (C#)](../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
* [Guide pratique pour sérialiser à l’aide de XmlSerializer (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
