---
title: "Prise en charge d'UI Automation pour le type de contrôle Table"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TableControl type
- control types, Table
- UI Automation, Table control type
ms.assetid: 9050dde5-6469-4c83-abb7-f861c24ff985
caps.latest.revision: "21"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 29f74ef6faf97cc9049211c70748e68592cc7d4b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="ui-automation-support-for-the-table-control-type"></a>Prise en charge d'UI Automation pour le type de contrôle Table
> [!NOTE]
>  Cette documentation s'adresse aux développeurs .NET Framework qui souhaitent utiliser les classes [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] managées définies dans l'espace de noms <xref:System.Windows.Automation>. Pour obtenir les dernières informations sur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consultez [API Windows Automation : UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Cette rubrique fournit des informations sur la prise en charge d’ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] pour le type de contrôle Table. Dans [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], un type de contrôle est un ensemble de conditions qu’un contrôle doit réunir pour pouvoir utiliser la propriété <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> . Les conditions incluent des indications spécifiques pour l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , les valeurs de propriété [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] et les modèles de contrôle.  
  
 Les contrôles Table contiennent des lignes et des colonnes de texte et, éventuellement, des en-têtes de lignes et des en-têtes de colonnes.  
  
 Les sections suivantes définissent l’arborescence, les propriétés, les modèles de contrôle et les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] requis pour le type de contrôle Table. Les exigences [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] s’appliquent à tous les contrôles de table, qu’il s’agisse de [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], de [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]ou de [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>Arborescence UI Automation obligatoire  
 Le tableau suivant illustre la vue de contrôle et la vue de contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relative aux contrôles de table, et décrit ce que peut contenir chaque vue. Pour plus d’informations sur l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , consultez [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Affichage de contrôle|Affichage de contenu|  
|------------------|------------------|  
|Table<br /><br /> -Header (0 ou 1)<br />-Texte (0 ou 1)<br />-Divers contrôles (0 ou plus)|Table<br /><br /> -Texte (0 ou plus)<br />-Divers contrôles (0 ou plus)|  
  
 Si un contrôle de table possède des en-têtes de lignes ou de colonnes, ceux-ci doivent être exposés dans la vue de contrôle de l’arborescence UI Automation. La vue de contenu n’a pas besoin d’exposer ces informations car elles sont accessibles à l’aide de TablePattern.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>Propriétés UI Automation requises  
 Le tableau suivant répertorie les propriétés [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] dont la valeur ou la définition est particulièrement pertinente pour les contrôles Table. Pour plus d’informations sur les propriétés [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , consultez [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Propriété[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] |Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Consultez les notes.|La valeur de cette propriété doit être unique dans tous les contrôles d’une application.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Consultez les notes.|Rectangle externe qui contient l’ensemble du contrôle.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Consultez les notes.|Pris en charge s’il existe un rectangle englobant. Si les points du rectangle englobant ne sont pas tous interactifs et que vous effectuez un test de positionnement spécialisé, vous devez remplacer et fournir un point interactif.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Consultez les notes.|Si le contrôle peut recevoir le focus clavier, il doit prendre en charge cette propriété.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Consultez les notes.|Le contrôle de table tire généralement son nom d’une étiquette de texte statique. En l’absence d’étiquette de texte statique, vous devez affecter une propriété Name qui doit toujours être disponible pour expliquer l’objectif de la table.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Consultez les notes.|S’il existe une étiquette de texte statique, cette propriété doit exposer une référence à l’élément Automation du contrôle.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Table|Cette valeur est la même pour toutes les infrastructures d’interface utilisateur.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|« table »|Chaîne localisée correspondant au type de contrôle Table.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Consultez les notes.|Des détails supplémentaires sur l’objectif de la table doivent être exposés via cette propriété si elle n’est pas suffisamment expliquée par l’accès à NameProperty.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Le contrôle de table doit toujours être du contenu.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Le contrôle de table doit toujours être un contrôle.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>Modèles de contrôle UI Automation requis  
 Le tableau suivant répertorie les modèles de contrôle [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par les contrôles Table. Pour plus d’informations sur les modèles de contrôle, consultez [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Modèle de contrôle|Assistance|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|Oui|Le contrôle de table prend toujours en charge ce modèle de contrôle car les éléments qu’il contient possèdent des données présentées dans une grille.|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|Oui (requise avec les objets enfants)|Les objets internes d’une table doivent prendre en charge les modèles de contrôle GridItem et TableItem. La table elle-même n’a pas besoin de prendre en charge les modèles de contrôle GridItem et TableItem, à moins que la table fasse partie d’une autre table.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|Oui|Le contrôle de table a toujours la possibilité d’utiliser des en-têtes associés au contenu.|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider>|Oui (requise avec les objets enfants)|Les objets internes d’une table doivent prendre en charge les modèles de contrôle GridItem et TableItem. La table elle-même n’a pas besoin de prendre en charge les modèles de contrôle GridItem et TableItem, à moins que la table fasse partie d’une autre table.|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>Événements UI Automation requis  
 Le tableau suivant répertorie les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par tous les contrôles de table. Pour plus d’informations sur les événements, consultez [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Événement[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] |Assistance|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> .|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> .|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> .|Obligatoire|Aucun.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obligatoire|Aucun.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obligatoire|Aucun.|  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Automation.ControlType.Table>  
 [Vue d’ensemble des types de contrôle UI Automation](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)  
 [Vue d’ensemble d’UI Automation](../../../docs/framework/ui-automation/ui-automation-overview.md)
