---
title: -langversion (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /langversion
helpviewer_keywords:
- /langversion compiler option [C#]
- -langversion compiler option [C#]
- langversion compiler option [C#]
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
caps.latest.revision: "33"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 11aab223ee70ff69d8c3470e747738bfe44540ea
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-langversion-c-compiler-options"></a>-langversion (Options du compilateur C#)
Force le compilateur à accepter uniquement la syntaxe incluse dans la spécification choisie du langage C#.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-langversion:option  
```  
  
## <a name="arguments"></a>Arguments  
 `option`  
 Les valeurs suivantes sont valides :  
  
|Option|Signification|  
|------------|-------------|  
|default|Le compilateur accepte toute la syntaxe de langage valide qu’il peut prendre en charge. <sup id="TDefault">[Default](#FDefault)</sup>| 
|ISO-1|Le compilateur accepte uniquement la syntaxe qui est incluse dans ISO/IEC 23270:2003 C# (1.0/1.1) <sup id="TISO1">[ISO1](#FISO1)</sup>|  
|ISO-2|Le compilateur accepte uniquement la syntaxe qui est incluse dans ISO/IEC 23270:2006 C# (2.0) <sup id="TISO2">[ISO2](#FISO2)</sup>|
|3|Le compilateur accepte uniquement la syntaxe qui est incluse dans C# version 3.0 ou inférieure <sup id="TCS3">[CS3](#FCS3)</sup>|
|4|Le compilateur accepte uniquement la syntaxe qui est incluse dans C# version 4.0 ou inférieure <sup id="TCS4">[CS4](#FCS4)</sup>|
|5|Le compilateur accepte uniquement la syntaxe qui est incluse dans C# version 5.0 ou inférieure <sup id="TCS5">[CS5](#FCS5)</sup>|
|6|Le compilateur accepte uniquement la syntaxe qui est incluse dans C# version 6.0 ou inférieure <sup id="TCS6">[CS6](#FCS6)</sup>|
|7|Le compilateur accepte uniquement la syntaxe qui est incluse dans C# version 7.0 ou inférieure <sup id="TCS7">[CS7](#FCS7)</sup>|
|latest|Le compilateur accepte toute la syntaxe de langage valide qu’il peut prendre en charge. <sup id="TLatest">[Latest](#FLatest)</sup>|
<!--- Uncomment and move these above
|latest| once they're officially released
|7.1|The compiler accepts only syntax that is included in C# 7.1 or lower <sup id="TCS71">[CS71](#FCS71)</sup>|
|7.2|The compiler accepts only syntax that is included in C# 7.2 or lower <sup id="TCS71">[CS72](#FCS72)</sup>|
|8|The compiler accepts only syntax that is included in C# 8 or lower <sup id="TCS71">[CS8](#FCS8)</sup>|
-->

  
## <a name="remarks"></a>Notes  
 Les métadonnées référencées par votre application C# ne sont pas visées par l’option de compilateur **-langversion**.  
  
 Sachant que chaque version du compilateur C# contient des extensions de la spécification du langage, **-langversion** ne vous offre pas les fonctionnalités équivalentes d’une version antérieure du compilateur.  
 
 De plus, alors que les mises à jour de la version de C# coïncident généralement avec la publication des principales versions du .NET Framework, la nouvelle syntaxe et les nouvelles fonctionnalités ne sont pas nécessairement liées à cette version spécifique du framework. Alors que les nouvelles fonctionnalités nécessiteront certainement une nouvelle mise à jour du compilateur qui sera publiée en même temps que la révision de C#, chaque fonctionnalité spécifique exigera une configuration minimale pour les API .NET ou le common language runtime qui pourra lui permettre de s’exécuter sur des frameworks de bas niveau moyennant des packages NuGet ou d’autres bibliothèques.
  
 Quel que soit le paramètre **-langversion** que vous utiliserez, vous vous servirez de la version active du common language runtime pour créer votre fichier .exe ou .dll. Les assemblys friend et [-moduleassemblyname (Option du compilateur C#)](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md), qui fonctionnent sous **-langversion:ISO-1**, représentent la seule exception.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ouvrez la page **Propriétés** du projet.  
  
2.  Cliquez sur la page de propriétés **Générer**.  
  
3.  Cliquez sur le bouton **Avancées** .  
  
4.  Modifiez la propriété **Version du langage**.  
  
 Pour plus d'informations sur la façon de définir cette option du compilateur par programme, consultez <xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>.  
    
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)  
 
### <a name="c-language-specification"></a>Spécification du langage C#
 [Informations de référence sur la spécification du langage C#](../../../csharp/language-reference/language-specification/index.md) : .NET Foundation  
 C# 1.0/1.1 [ISO/IEC 23270 : 2003](https://www.iso.org/standard/36768.html) Technologies de l’information -- Spécification du langage C# : Catalogue ISO  
 C# 2.0 [ISO/IEC 23270 : 2006](https://www.iso.org/standard/42926.html) Technologies de l’information -- Spécification du langage C# : Catalogue ISO  
 C# 2.0 [c042926_ISO_IEC_23270_2006(E).zip](http://standards.iso.org/ittf/PubliclyAvailableStandards/c042926_ISO_IEC_23270_2006(E).zip) ISO/IEC 23270:2006 au format PDF : Normes ISO disponibles gratuitement  
 C# 3.0 [CSharp Language Specification.doc](http://download.microsoft.com/download/3/8/8/388e7205-bc10-4226-b2a8-75351c669b09/CSharp%20Language%20Specification.doc) Spécification du langage C# version 3.0 : Microsoft Corporation  
 C# 4.0 [Ecma-334.pdf](https://www.ecma-international.org/publications/files/ECMA-ST/Ecma-334.pdf) Norme ECMA-334 4e édition    
 C# 5.0 [CSharp Language Specification.docx](https://www.microsoft.com/download/details.aspx?id=7029) Spécification du langage C# version 5.0 : Microsoft Corporation  
 C# 6.0 [README.md](https://github.com/dotnet/csharplang/blob/master/spec/README.md) Spécification du langage C# version 6 - Ébauche non officielle : .NET Foundation  
 C# 7.0 (actuellement non disponible)  

<!--- Uncomment and add to the above when they become officially released
 C# 7.1 (spec is not yet finished)  
 C# 7.2 (spec is not yet finished)  
 C# 8.0 (spec is not yet finished)  
-->

### <a name="minimum-compiler-version-needed-to-support-all-language-features"></a>Version minimale obligatoire du compilateur pour une prise en charge de toutes les fonctionnalités du langage   
[↩](#TDefault)<a name="FDefault">Default</a>, <a name="FISO1">ISO1</a> : Microsoft Visual Studio/Build Tools .Net 2002 ou compilateur .Net Framework 1.0 intégré     
[↩](#TISO2)<a name="FISO2">ISO2</a> : Microsoft Visual Studio/Build Tools 2005 ou compilateur .Net Framework 2.0 intégré    
[↩](#TCS3)<a name="FCS3">CS3</a> : Microsoft Visual Studio/Build Tools 2008 ou compilateur .Net Framework 3.5 intégré    
[↩](#TCS4)<a name="FCS4">CS4</a> : Microsoft Visual Studio/Build Tools 2010 ou compilateur .Net Framework 4.0 intégré    
[↩](#TCS5)<a name="FCS5">CS5</a> : Microsoft Visual Studio/Build Tools 2012 ou compilateur .Net Framework 4.5 intégré    
[↩](#TCS6)<a name="FCS6">CS6</a> : Microsoft Visual Studio/Build Tools 2015    
[↩](#TCS7)<a name="FCS7">CS7</a>, <a name="FLatest">Latest</a> : Microsoft Visual Studio/Build Tools 2017   

<!--- Uncomment and add to the above when they become officially released
[↩](#TCS71)<a name="FCS71">CS71</a>: Microsoft Visual Studio/Build Tools 20??    
[↩](#TCS72)<a name="FCS72">CS72</a>: Microsoft Visual Studio/Build Tools 20??    
[↩](#TCS8)<a name="FCS71">CS8</a>: Microsoft Visual Studio/Build Tools 20??    
-->
