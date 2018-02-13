---
title: "&lt;supportedRuntime&gt; élément"
ms.date: 10/17/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: article
ms.custom: updateeachrelease
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime
helpviewer_keywords:
- supportedRuntime element
- <supportedRuntime> element
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 4b0967790f2bbf8fa9a889c56fa9c5168f7523bd
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="ltsupportedruntimegt-element"></a>&lt;supportedRuntime&gt; élément

Spécifie quelles versions du Common Language Runtime sont prises en charge par l'application. Cet élément doit être utilisé par toutes les applications créées avec la version 1.1 ou ultérieure du .NET Framework.  
  
[\<configuration>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
&nbsp;&nbsp;[\<startup>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<supportedRuntime>**  
  
## <a name="syntax"></a>Syntaxe
  
```xml  
<supportedRuntime version="runtime version" sku="sku id"/>  
```  
  
## <a name="attributes"></a>Attributs
  
|Attribut|Description|  
|---------------|-----------------|  
|**version**|Attribut facultatif.<br /><br /> Valeur de chaîne qui spécifie la version du Common Language Runtime (CLR) prise en charge par cette application. Pour les valeurs valides de le `version` d’attribut, consultez la [les valeurs « version du runtime »](#version) section. **Remarque :** via le .NET Framework 3.5, le «*version du runtime*» valeur prend la forme *majeure*. *mineure*. *build*. Depuis [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], seuls les numéros de version principale et secondaire sont nécessaires (c'est-à-dire "v4.0" au lieu de "v4.0.30319"). La chaîne courte est recommandée.|  
|**sku**|Attribut facultatif.<br /><br /> Valeur de chaîne qui spécifie la référence (SKU), qui à son tour spécifie quelle version du .NET Framework cette application prend en charge.<br /><br /> En commençant par le .NET Framework 4.0, l’utilisation de la `sku` est recommandé d’attribut.  Quand il est présent, il indique la version du .NET Framework ciblée par l’application.<br /><br /> Pour les valeurs valides de l’attribut de référence (SKU), consultez le [les valeurs « id de référence (SKU) »](#sku) section.|  
  
## <a name="remarks"></a>Notes

Si le  **\<supportedRuntime >** élément n’est pas présent dans le fichier de configuration d’application, la version du runtime utilisée pour générer l’application est utilisée.  

Le  **\<supportedRuntime >** élément doit être utilisé par toutes les applications générées à l’aide de la version 1.1 ou ultérieure du runtime. Les applications générées pour prendre en charge uniquement la version 1.0 du runtime doivent utiliser le [ \<requiredRuntime >](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md) élément.  
  
> [!NOTE]
>  Si vous utilisez la [CorBindToRuntimeByCfg](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) de fonction pour spécifier le fichier de configuration, vous devez utiliser le `<requiredRuntime>` élément pour toutes les versions du runtime. Le `<supportedRuntime>` élément est ignoré lorsque vous utilisez [CorBindToRuntimeByCfg](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md).  
  
Pour les applications prenant en charge les versions du runtime du .NET Framework 1.1 à 3.5, quand plusieurs versions du runtime sont prises en charge, le premier élément doit spécifier la version du runtime préférée en premier tandis que le dernier élément doit spécifier la version préférée en dernier. Pour les applications qui prennent en charge le .NET Framework 4.0 ou versions ultérieures, le `version` attribut indique la version du CLR, ce qui est commune pour le .NET Framework 4 et versions ultérieures, et le `sku` attribut indique la version de .NET Framework unique que l’application cibles.  
  
> [!NOTE]
>  Si votre application utilise des chemins d’activation hérités, tels que les [fonction CorBindToRuntimeEx](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md), et vous souhaitez que ces chemins activent la version 4 du CLR au lieu d’une version antérieure, ou si votre application est générée avec la [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]mais a une dépendance sur un assembly en mode mixte généré avec une version antérieure du .NET Framework, il n’est pas suffisant pour spécifier le [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] dans la liste des runtimes pris en charge. En outre, dans le [ \<démarrage > élément](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) dans votre fichier de configuration, vous devez définir le `useLegacyV2RuntimeActivationPolicy` attribut `true`. Toutefois, l'affectation de la valeur `true` à cet attribut signifie que tous les composants générés avec des versions antérieures du .NET Framework sont exécutés à l'aide de [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] plutôt qu'à l'aide des runtimes avec lesquels ils ont été générés.  
  
Nous vous recommandons de tester les applications avec toutes les versions du .NET Framework sur lesquelles elles peuvent s'exécuter.  
  
<a name="version"></a>   
## <a name="runtime-version-values"></a>valeurs de "runtime version"  
Le `runtime` attribut spécifie la version du Common Language Runtime (CLR) qui est requise pour une application donnée. Notez que toutes les versions de .NET Framework 4.x spécifient le `v4.0` CLR. Le tableau suivant répertorie les valeurs valides pour le *version du runtime* valeur de la `version` attribut.  

|Version du .NET Framework|Attribut `version`|  
|----------------------------|-------------------------|  
|1.0|"v1.0.3705"|  
|1.1|"v1.1.4322"|  
|2.0|"v2.0.50727"|  
|3.0|"v2.0.50727"|  
|3.5|"v2.0.50727"|  
|4.0-4.7.1|"v4.0"|  

<a name="sku"></a>   
## <a name="sku-id-values"></a>valeurs de "sku id"

Le `sku` attribut utilise un moniker du framework cible (TFM) pour indiquer la version du .NET Framework que l’application cible et qu’il a besoin pour s’exécuter. Le tableau suivant répertorie les valeurs valides sont pris en charge par le `sku` attribut, en commençant par le .NET Framework 4.
  
|Version du .NET Framework|Attribut `sku`|  
|----------------------------|---------------------|  
|4.0|".NETFramework,Version=v4.0"|  
|4.0, Client Profile|".NETFramework,Version=v4.0,Profile=Client"|  
|4.0, Platform Update 1|.NETFramework,Version=v4.0.1|  
|4.0, Client Profile, Update 1|.NETFramework, Version=v4.0.1, Profile=Client|  
|4.0, Platform Update 2|.NETFramework,Version=v4.0.2|  
|4.0, Client Profile, Update 2|.NETFramework, Version=v4.0.2, Profile=Client|  
|4.0, Platform Update 3|.NETFramework,Version=v4.0.3|  
|4.0, Client Profile, Update 3|.NETFramework, Version=v4.0.3, Profile=Client|  
|4.5|".NETFramework,Version=v4.5"|  
|4.5.1|".NETFramework,Version=v4.5.1"|  
|4.5.2|".NETFramework,Version=v4.5.2"|  
|4.6|".NETFramework,Version=v4.6"|  
|4.6.1|".NETFramework,Version=v4.6.1"|  
|4.6.2|".NETFramework,Version=v4.6.2"|  
|4.7|".NETFramework,Version=v4.7"|
|4.7.1|".NETFramework,Version=v4.7.1"|

## <a name="example"></a>Exemple  
 L’exemple suivant montre comment spécifier la version du runtime prise en charge dans un fichier de configuration. Le fichier de configuration indique que l’application cible le 4.7 Framework .NET.  
  
```xml  
<configuration>  
   <startup>  
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />  
   </startup>  
</configuration>  
```  
  
## <a name="configuration-file"></a>fichier de configuration

Cet élément peut être utilisé dans le fichier de configuration de l'application.

## <a name="see-also"></a>Voir aussi

 [Schéma des paramètres de démarrage](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)  
 [Schéma des fichiers de configuration](../../../../../docs/framework/configure-apps/file-schema/index.md)  
 [Exécution côte à côte in-process](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)  
