---
title: "Prise en charge d'UI Automation pour le type de contrôle TreeItem"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- control types, Tree Item
- Tree Item control type
- UI Automation, Tree Item control type
ms.assetid: 229f341a-477f-434e-b877-4db9973068eb
caps.latest.revision: "22"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: cafc47d168e46eb0ab99ee988ea6f0c6c3f80b1e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="ui-automation-support-for-the-treeitem-control-type"></a>Prise en charge d’UI Automation pour le type de contrôle TreeItem
> [!NOTE]
>  Cette documentation s'adresse aux développeurs .NET Framework qui souhaitent utiliser les classes [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] managées définies dans l'espace de noms <xref:System.Windows.Automation>. Pour obtenir les dernières informations sur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consultez [API Windows Automation : UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Cette rubrique fournit des informations sur la prise en charge de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] pour le type de contrôle TreeItem. Dans [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], un type de contrôle est un ensemble de conditions qu’un contrôle doit réunir pour pouvoir utiliser la propriété <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> . Les conditions incluent des indications spécifiques pour l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , les valeurs de propriété [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] et les modèles de contrôle.  
  
 Le contrôle de type TreeItem représente un nœud dans un conteneur d’arborescence. Chaque nœud peut contenir d’autres nœuds, appelés nœuds enfants. Vous pouvez afficher les nœuds parents, ou nœuds qui contiennent des nœuds enfants, sous forme développée ou réduite.  
  
 Les sections suivantes définissent l’arborescence, les propriétés, les modèles de contrôle et les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] nécessaires pour le type de contrôle TreeItem. Les exigences [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] s’appliquent à tous les contrôles d’élément d’arborescence, qu’il s’agisse de [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]ou [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>Arborescence UI Automation obligatoire  
 Le tableau suivant représente l’affichage de contrôle et l’affichage du contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relative aux contrôles d’élément d’arborescence. En outre, il décrit ce que peut contenir chaque affichage. Pour plus d’informations sur l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , consultez [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Affichage de contrôle|Affichage de contenu|  
|------------------|------------------|  
|TreeItem<br /><br /> -Case à cocher (0 ou 1)<br />-Image (0 ou 1)<br />-Bouton (0 ou 1)<br />-TreeItem (0 ou plus)|TreeItem<br /><br /> -TreeItem (0 ou plus)|  
  
 Les contrôles d’élément d’arborescence peuvent comporter zéro ou plusieurs enfants d’élément d’arborescence dans l’affichage du contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . Si le contrôle d’élément d’arborescence a d’autres fonctionnalités que celles exposées dans les modèles de contrôle répertoriés ci-dessous, le contrôle doit être basé sur le type de contrôle DataItem.  
  
 Les éléments d’arborescence réduits n’apparaissent pas dans l’affichage de contrôle ou l’affichage du contenu tant qu’ils ne sont pas développés et visibles (ou tant qu’ils ne peuvent pas être l’objet d’un défilement).  
  
 L’affichage de contrôle peut contenir des détails supplémentaires pour un contrôle, notamment une image ou un bouton associé. Par exemple, un élément en mode Plan peut contenir une image, ainsi qu’un bouton pour développer ou réduire le plan. Ces objets de détail n’apparaissent pas dans l’affichage du contenu, car les informations sont déjà représentées par l’élément d’arborescence parent. Les éléments d’arborescence qui défilent au-delà de l’écran apparaissent dans les affichages de contrôle et du contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . En outre, <xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> doit avoir la valeur true.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>Propriétés UI Automation requises  
 Le tableau suivant répertorie les propriétés [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] dont la valeur ou la définition est particulièrement pertinente pour les contrôles de liste. Pour plus d’informations sur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] propriétés, consultez [propriétés UI Automation pour les Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Propriété[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] |Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Consultez les notes.|La valeur de cette propriété doit être unique dans tous les contrôles d’une application.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Consultez les notes.|Rectangle externe qui contient l’ensemble du contrôle.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Consultez les notes.|Cette propriété doit retourner un emplacement de l’élément qui oblige ce dernier à changer d’état de sélection ou à prendre le focus.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|TreeItem|Cette valeur est identique pour toutes les infrastructures d’interface utilisateur.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Le contrôle de liste est toujours inclus dans l’affichage de contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Le contrôle de liste est toujours inclus dans l’affichage de contrôle de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Consultez les notes.|Cette propriété est définie pour indiquer le moment où un contrôle d’élément d’arborescence défile au-delà de l’écran.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Consultez les remarques.|Si le contrôle peut recevoir le focus clavier, il doit prendre en charge cette propriété.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|Consultez les notes.|Si le contrôle d’élément d’arborescence utilise une icône visuelle pour indiquer qu’il s’agit d’un type d’objet particulier, cette propriété doit être prise en charge et indiquer à quoi correspond l’objet.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Les contrôles d’élément d’arborescence créent eux-mêmes leurs étiquettes.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"élément d’arborescence"|Chaîne localisée correspondant au type de contrôle TreeItem.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Consultez les notes.|Cette propriété expose le texte affiché pour chaque contrôle d’élément d’arborescence.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>Modèles de contrôle UI Automation obligatoires  
 Le tableau suivant répertorie les modèles de contrôle [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par les contrôles de liste. Pour plus d’informations sur les modèles de contrôle, consultez [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Modèle de contrôle/Propriété de modèle|Prise en charge/Valeur|Notes|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Selon le cas|Implémentez ce modèle de contrôle si l’élément d’arborescence dispose d’une commande distincte pouvant être actionnée.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Oui|Tous les éléments d’arborescence peuvent être développés ou réduits.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider.ExpandCollapseState%2A>|Nœud développé, réduit ou terminal|Les éléments d’arborescence sont des nœuds terminaux quand ils ne sont pas développés ou réduits.|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|Selon le cas|Implémentez ce modèle de contrôle si le conteneur d’arborescence prend en charge le modèle de contrôle Scroll.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Selon le cas|Implémentez ce modèle de contrôle s’il est possible de conserver une sélection active quand l’utilisateur retourne au conteneur d’arborescence.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider.SelectionContainer%2A>|Oui|Cette propriété expose le même conteneur pour tous les éléments du conteneur.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|Selon le cas|Implémentez ce modèle de contrôle si une case à cocher est associée à l’élément d’arborescence.|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>Événements UI Automation requis  
 Le tableau suivant répertorie les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par tous les contrôles d’élément d’arborescence. Pour plus d’informations sur les événements, consultez [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Événement[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] |Assistance|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> |Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> .|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> .|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty> .|Selon le cas|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> |Obligatoire|Aucun.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obligatoire|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> |Obligatoire|Aucun.|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|Selon le cas|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> .|Selon le cas|Aucun.|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Selon le cas|Aucun.|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Selon le cas|Aucun.|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Selon le cas|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> |Selon le cas|Aucun.|  
|Événement de modification de propriété<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> |Selon le cas|Aucun.|  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Automation.ControlType.TreeItem>  
 [Vue d’ensemble des types de contrôle UI Automation](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)  
 [Vue d’ensemble d’UI Automation](../../../docs/framework/ui-automation/ui-automation-overview.md)
