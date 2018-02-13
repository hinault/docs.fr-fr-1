---
title: "Outils .NET Core supplémentaires"
description: "Vue d’ensemble des outils supplémentaires qui prennent en charge et étendent les fonctionnalités de .NET Core."
author: mlacouture
manager: wpickett
ms.author: johalex
ms.date: 01/19/2018
ms.topic: article
ms.prod: .net-core
ms.custom: mvc
ms.openlocfilehash: 21fcc1190ee4586a8d7eb6fb8d63a7c312e63825
ms.sourcegitcommit: c1904b0437605a90e5aa65b4abd7e048000e349d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2018
---
# <a name="net-core-additional-tools"></a>Outils .NET Core supplémentaires

Cette section dresse une liste des outils qui prennent en charge et étendent les fonctionnalités de .NET Core, en plus des outils d’[interface de ligne de commande (CLI) .NET Core](..\tools\index.md).

## <a name="wcf-web-service-reference-toolwcf-web-service-reference-guidemd"></a>[Outil WCF Web Service Reference](wcf-web-service-reference-guide.md)

WCF Web Service Reference est un fournisseur de services connectés Visual Studio qui a fait son apparition dans [Visual Studio 2017 version 15.5](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#WCFTools). Cet outil récupère les métadonnées d’un service web dans la solution actuelle sur un emplacement réseau ou dans un fichier WSDL, puis génère un fichier source compatible .NET Core contenant du code de proxy client WCF (Windows Communication Foundation) que vous pouvez utiliser pour accéder au service web.

## <a name="xml-serializer-generatorxml-serializer-generatormd"></a>[Générateur de sérialiseur XML](xml-serializer-generator.md)

Comme le [Générateur de sérialiseur XML (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) pour le .NET Framework, le [package NuGet Microsoft.XmlSerializer.Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) est la solution pour les bibliothèques .NET Core et .NET Standard. Il crée un assembly de sérialisation XML pour les types contenus dans un assembly afin d’améliorer les performances de démarrage de la sérialisation XML pendant la sérialisation ou la désérialisation des objets de ces types avec <xref:System.Xml.Serialization.XmlSerializer>.