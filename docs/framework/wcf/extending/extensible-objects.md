---
title: Objets extensibles
ms.date: 03/30/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: article
helpviewer_keywords: extensible objects [WCF]
ms.assetid: bc88cefc-31fb-428e-9447-6d20a7d452af
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a1bb341d9e164b1ce232f238f8ddf4a0cf807363
ms.sourcegitcommit: c1904b0437605a90e5aa65b4abd7e048000e349d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2018
---
# <a name="extensible-objects"></a>Objets extensibles
Le modèle d’objet extensible est utilisé pour étendre des classes d’exécution existantes à l’aide de nouvelles fonctionnalités ou ajouter un nouvel état à un objet. Les extensions, attachées à l’un des objets extensibles, permettent aux comportements à des étapes différentes du traitement, d’accéder à l’état partagé et aux fonctionnalités attachés à un objet extensible commun qui leur est accessible.  
  
## <a name="the-iextensibleobjectt-pattern"></a>Le IExtensibleObject\<T > modèle  
 Le modèle d'objet extensible contient trois interfaces : <xref:System.ServiceModel.IExtensibleObject%601>, <xref:System.ServiceModel.IExtension%601> et <xref:System.ServiceModel.IExtensionCollection%601>.  
  
 L'interface <xref:System.ServiceModel.IExtensibleObject%601> est implémentée par les types qui permettent aux objets <xref:System.ServiceModel.IExtension%601> de personnaliser leurs fonctionnalités.  
  
 Les objets extensibles permettent le regroupement dynamique des objets <xref:System.ServiceModel.IExtension%601>. Les objets <xref:System.ServiceModel.IExtension%601> sont caractérisés par l'interface suivante :  
  
```  
public interface IExtension<T>  
where T : IExtensibleObject<T>  
{  
    void Attach(T owner);  
    void Detach(T owner);  
}  
```  
  
 La restriction de type garantit que les extensions ne peuvent être définies que pour les classes <xref:System.ServiceModel.IExtensibleObject%601>. <xref:System.ServiceModel.IExtension%601.Attach%2A> et <xref:System.ServiceModel.IExtension%601.Detach%2A> fournissent une notification de l'agrégation ou de la désagrégation.  
  
 Il est valide pour les implémentations d'appliquer des restrictions lorsqu'elles peuvent être ajoutées et supprimées d'un propriétaire. Par exemple, vous pouvez complètement interdire la suppression en interdisant l'ajout ou la suppression des extensions lorsque le propriétaire ou l'extension est dans un certain état, interdire l'ajout simultané à plusieurs propriétaires ou autoriser uniquement un ajout unique suivi par une suppression unique.  
  
 <xref:System.ServiceModel.IExtension%601> n'implique pas d'interactions avec d'autres interfaces standard managées. Plus précisément, la méthode <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> sur l'objet de propriétaire ne détache pas normalement ses extensions.  
  
 Lorsqu'une extension est ajoutée à la collection, <xref:System.ServiceModel.IExtension%601.Attach%2A> est appelé avant d'entrer dans la collection. Lorsqu'une extension est supprimée de la collection, <xref:System.ServiceModel.IExtension%601.Detach%2A> est appelée après sa suppression. Cela signifie (en supposant une synchronisation correcte) qu'une extension ne peut figurer dans la collection que si elle se situe entre <xref:System.ServiceModel.IExtension%601.Attach%2A> et <xref:System.ServiceModel.IExtension%601.Detach%2A>.  
  
 L'objet passé à <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> ou <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> n'a pas besoin d'être <xref:System.ServiceModel.IExtension%601> (par exemple, vous pouvez passer tout objet), mais l'extension retournée est un <xref:System.ServiceModel.IExtension%601>.  
  
 Si aucune extension dans la collection est un <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> retourne la valeur null, et <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> retourne une collection vide. Si plusieurs extensions implémentent <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> retourne l'une d'entre elle. La valeur retournée par <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> est un instantané.
  
 Il y a deux scénarios principaux. Le premier scénario utilise la propriété <xref:System.ServiceModel.IExtensibleObject%601.Extensions%2A> comme un dictionnaire basé sur un type pour insérer l'état sur un objet pour permettre à un autre composant de le rechercher à l'aide du type.  
  
 Le deuxième scénario utilise les propriétés <xref:System.ServiceModel.IExtension%601.Attach%2A> et <xref:System.ServiceModel.IExtension%601.Detach%2A> pour permettre à un objet de participer à un comportement personnalisé, tel que l'inscription aux événements, l'observation des transitions d'état, etc.  
  
 L'interface <xref:System.ServiceModel.IExtensionCollection%601> est une collection d'objets <xref:System.ServiceModel.IExtension%601> qui permet la récupération de <xref:System.ServiceModel.IExtension%601> par son type. <xref:System.ServiceModel.IExtensionCollection%601.Find%2A?displayProperty=nameWithType> retourne l'objet récemment ajouté dans un <xref:System.ServiceModel.IExtension%601> de ce type.  
  
### <a name="extensible-objects-in-windows-communication-foundation"></a>Objets extensibles dans Windows Communication Foundation  
 Il existe quatre objets extensibles dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] :  
  
-   <xref:System.ServiceModel.ServiceHostBase> - Il s'agit de la classe de base pour l'hôte du service.  Les extensions de cette classe peuvent être utilisées pour étendre le comportement du <xref:System.ServiceModel.ServiceHostBase> lui-même ou pour stocker l'état pour chaque service.  
  
-   <xref:System.ServiceModel.InstanceContext> - Cette classe connecte une instance du type du service à l'exécution du service.  Elle contient des informations sur l'instance et une référence au <xref:System.ServiceModel.InstanceContext> qui contient <xref:System.ServiceModel.ServiceHostBase>. Les extensions de cette classe peuvent être utilisées pour étendre le comportement du <xref:System.ServiceModel.InstanceContext> ou pour stocker l'état pour chaque service.  
  
-   <xref:System.ServiceModel.OperationContext> - Cette classe représente les informations d'opération que l'exécution rassemble pour chaque opération.  Cela inclut des informations telles que les en-têtes de message entrant, les propriétés de message entrant, l'identité de sécurité entrante et d'autres informations.  Les extensions de cette classe peuvent étendre le comportement de <xref:System.ServiceModel.OperationContext> ou stocker l'état pour chaque opération.  
  
-   <xref:System.ServiceModel.IContextChannel> - Cette interface tient compte de l'inspection de chaque état pour les canaux et les proxys construits par l'exécution [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Les extensions de cette classe peuvent étendre le comportement de <xref:System.ServiceModel.IClientChannel> ou peuvent l'utiliser pour stocker l'état pour chaque canal.  
  
-  
  
 L'exemple de code suivant montre l'utilisation d'une simple extension pour assurer le suivi des objets <xref:System.ServiceModel.InstanceContext>.  
  
 [!code-csharp[IInstanceContextInitializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/iinstancecontextinitializer/cs/initializer.cs#1)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.IExtensibleObject%601>  
 <xref:System.ServiceModel.IExtension%601>  
 <xref:System.ServiceModel.IExtensionCollection%601>
