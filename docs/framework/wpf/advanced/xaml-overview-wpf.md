---
title: "Vue d’ensemble du langage XAML (WPF)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user interfaces [XAML]
- classes [XAML]
- root element [XAML]
- XAML [WPF], about XAML
- base classes [XAML]
- routed events [WPF]
- code-behind files [WPF], XAML
- collection properties [XAML]
- events [XAML]
- property element [XAML]
- content models [XAML]
- Extensible Application Markup Language (see XAML)
- attribute syntax [XAML]
ms.assetid: a80db4cd-dd0f-479f-a45f-3740017c22e4
caps.latest.revision: "57"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ce83713d2483320569bde0d5c9a677f0b357ebf2
ms.sourcegitcommit: c3ebb11a66e85a465c9ba2c42592222630b7ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="xaml-overview-wpf"></a>Vue d’ensemble du langage XAML (WPF)
Cette rubrique décrit les fonctionnalités du langage XAML et montre comment utiliser XAML pour écrire des applications [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]. Cette rubrique décrit en particulier le langage XAML tel qu’il est implémenté par [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Le XAML lui-même est un concept de langage plus vaste que [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
  
  
<a name="what_is_xaml"></a>   
## <a name="what-is-xaml"></a>Qu’est-ce que XAML ?  
 XAML est un langage de balisage déclaratif. Appliqué au modèle de programmation [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)], le langage XAML simplifie la création d’une [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] pour une application [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]. Vous pouvez créer les éléments [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] visibles dans le balisage XAML déclaratif, puis séparer la logique de la définition de l’interface [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] au moment de l’exécution, en utilisant les fichiers code-behind joints au balisage par le biais de définitions de classe partielle. XAML représente directement l’instanciation d’objets dans un ensemble spécifique de types de stockage définis dans des assemblys. C’est ce qui le différencie de la plupart des autres langages de balisage, qui sont en général des langages interprétés sans un lien aussi direct à un système de type de stockage. XAML permet un flux de travail dans lequel des parties distinctes peuvent travailler sur l’interface [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] et la logique d’une application avec des outils pouvant être différents.  
  
 Représentés sous forme de texte, les fichiers XAML sont des fichiers XML qui ont généralement l’extension `.xaml`. Les fichiers peuvent être encodés par un encodage XML, même si UTF-8 est l’encodage classique.  
  
 L’exemple suivant montre comment vous pouvez créer un bouton dans une [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]. Cet exemple est uniquement destiné à vous donner une idée de la manière dont le XAML représente les métaphores de programmation courantes de l’interface [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] (ce n’est pas un exemple exhaustif).  
  
 [!code-xaml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
<a name="xaml_syntax_in_brief"></a>   
## <a name="xaml-syntax-in-brief"></a>Syntaxe XAML en bref  
 Les sections suivantes expliquent les bases de la syntaxe XAML et donnent un court exemple de balisage. Ces sections ne visent pas à fournir des informations complètes sur toutes les formes de syntaxe, telles que représentées dans le système de types de stockage. Pour plus d’informations sur les spécificités de la syntaxe XAML propres à chacune des formes syntaxiques présentées dans cette rubrique, consultez [Syntaxe XAML en détail](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 La plupart des informations présentées dans les sections suivantes peuvent vous paraître élémentaires si vous connaissez déjà le langage XML. C’est une conséquence d’un des principes de base de la conception du langage XAML.  Le langage XAML définit ses propres concepts, mais ces concepts fonctionnent dans le format de langue et le balisage XML.  
  
### <a name="xaml-object-elements"></a>Éléments objet XAML  
 Un élément objet déclare généralement une instance d’un type. Ce type est défini dans les assemblys qui fournissent les types de stockage d’une technologie utilisant le XAML comme langage.  
  
 La syntaxe d’un élément objet commence toujours par un signe « inférieur à » (\<). Le nom du type dans lequel vous souhaitez créer une instance suit. (Le nom peut comporter éventuellement un préfixe, concept expliqué plus tard.) Ensuite, vous pouvez le cas échéant déclarer des attributs sur l’élément objet. Pour terminer la balise de l’élément objet, finissez par un signe « supérieur à » (>). Sinon, vous pouvez utiliser une forme de fermeture automatique sans contenu en ajoutant à la balise une barre oblique suivie d’un signe « supérieur à » (/>). Par exemple, réexaminez l’extrait de code de balisage présenté précédemment :  
  
 [!code-xaml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
 Deux éléments objet sont spécifiés : `<StackPanel>` (avec du contenu et suivi d’une balise de fermeture) et `<Button .../>` (avec plusieurs attributs et la forme de fermeture automatique). Les éléments objet `StackPanel` et `Button` mappent chacun au nom d’une classe qui est définie par [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] et qui fait partie des assemblys [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Lorsque vous spécifiez une balise d’élément objet, vous créez une instruction de traitement XAML qui crée une nouvelle instance. Chaque instance est créée en appelant le constructeur par défaut du type sous-jacent lors de l’analyse et du chargement du code XAML.  
  
### <a name="attribute-syntax-properties"></a>Syntaxe d’attribut (Propriétés)  
 Les propriétés d’un objet peuvent souvent être exprimées en tant qu’attributs de l’élément objet. Une syntaxe d’attribut nomme la propriété qui est définie dans la syntaxe d’attribut et la fait suivre de l’opérateur d’assignation (=). La valeur d’un attribut est toujours spécifiée sous la forme d’une chaîne comprise entre guillemets.  
  
 La syntaxe d’attribut est la syntaxe de définition de propriétés la plus simple et la plus intuitive pour les développeurs ayant déjà utilisé des langages de balisage. Par exemple, le balisage suivant crée un bouton qui se compose d’un texte en rouge et d’un arrière-plan bleu, en plus du texte d’affichage spécifié comme `Content`.  
  
 [!code-xaml[XAMLOvwSupport#BlueRedButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbutton)]  
  
### <a name="property-element-syntax"></a>Syntaxe des éléments de propriété  
 Pour certaines propriétés d’un élément objet, la syntaxe d’attribut n’est pas possible parce que l’objet ou les informations nécessaires pour fournir la valeur de propriété ne peuvent pas être correctement exprimés dans les guillemets et les restrictions de chaîne de la syntaxe d’attribut. Pour ces cas particuliers, vous pouvez utiliser une autre syntaxe appelée syntaxe des éléments de propriété.  
  
 La syntaxe de la balise de début de l’élément de propriété est `<` *nomType*`.`*nomPropriété*`>`. En règle générale, le contenu de cette balise est un élément objet du type que la propriété prend comme valeur. Après avoir spécifié le contenu, vous devez fermer l’élément de propriété avec une balise de fin. La syntaxe de la balise de fin est `</` *nomType*`.`*nomPropriété*`>`.  
  
 Si une syntaxe d’attribut est possible, son utilisation est généralement plus pratique et permet un balisage plus compact, mais il s’agit souvent d’une simple question de style et non d’une restriction technique. L’exemple suivant montre les mêmes propriétés définies comme dans l’exemple de la syntaxe d’attribut précédent, mais cette fois-ci la syntaxe des éléments de propriété est utilisée pour toutes les propriétés de `Button`.  
  
 [!code-xaml[XAMLOvwSupport#BlueRedButtonPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbuttonpe)]  
  
### <a name="collection-syntax"></a>Syntaxe des collections  
 Le langage XAML offre quelques optimisations qui permettent une meilleure lecture des balises. Par exemple, si une propriété particulière utilise un type de collection, les éléments que vous déclarez dans le balisage en tant qu’éléments enfants dans cette valeur de propriété deviennent partie intégrante de la collection. Dans ce cas, une collection d’éléments objet enfants est la valeur définie pour la propriété de collection.  
  
 L’exemple suivant montre la syntaxe de collection pour définir les valeurs de la <xref:System.Windows.Media.GradientBrush.GradientStops%2A> propriété :  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <!-- no explicit new GradientStopCollection, parser knows how to find or create -->  
    <GradientStop Offset="0.0" Color="Red" />  
    <GradientStop Offset="1.0" Color="Blue" />  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
### <a name="xaml-content-properties"></a>Propriétés de contenu XAML  
 XAML spécifie une fonctionnalité de langage dans laquelle une classe peut désigner précisément une de ses propriétés comme étant la propriété de contenu XAML. Les éléments enfants de cet élément objet sont utilisés pour définir la valeur de cette propriété de contenu. En d’autres termes, pour la propriété de contenu uniquement, vous pouvez omettre un élément de propriété lors de la définition de cette propriété dans le balisage XAML et produire une métaphore parent/enfant plus visible dans le balisage.  
  
 Par exemple, <xref:System.Windows.Controls.Border> spécifie une propriété de contenu de <xref:System.Windows.Controls.Decorator.Child%2A>. Les deux <xref:System.Windows.Controls.Border> éléments sont traités de façon identique. Le premier tire parti de la syntaxe de la propriété de contenu et omet l’élément de propriété `Border.Child`. Le deuxième affiche `Border.Child` explicitement.  
  
```xaml  
<Border>  
  <TextBox Width="300"/>  
</Border>  
<!--explicit equivalent-->  
<Border>  
  <Border.Child>  
    <TextBox Width="300"/>  
  </Border.Child>  
</Border>  
```  
  
 En tant que règle du langage XAML, la valeur d’une propriété de contenu XAML doit figurer soit entièrement avant soit entièrement après tous les autres éléments de propriété sur cet élément objet. Par exemple, le balisage suivant n’est pas compilé :  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 Pour plus d’informations concernant cette restriction sur les propriétés de contenu XAML, consultez la section « Propriétés de contenu XAML » dans [Syntaxe XAML en détail](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
### <a name="text-content"></a>Contenu textuel  
 Un petit nombre d’éléments XAML peuvent traiter directement du texte comme étant leur contenu. Pour ce faire, un des cas suivants doit se vérifier :  
  
-   La classe doit déclarer une propriété de contenu, et cette propriété de contenu doit être d’un type assignable à une chaîne (le type peut être <xref:System.Object>). Par exemple, tout <xref:System.Windows.Controls.ContentControl> utilise <xref:System.Windows.Controls.ContentControl.Content%2A> en tant que propriété de contenu et il est le type <xref:System.Object>, et cela prend en charge l’utilisation suivante sur une pratique <xref:System.Windows.Controls.ContentControl> comme un <xref:System.Windows.Controls.Button>: `<Button>Hello</Button>`.  
  
-   Le type doit déclarer un convertisseur de type, auquel cas le contenu de texte est utilisé comme texte d’initialisation pour ce convertisseur de type. Par exemple, `<Brush>Blue</Brush>`. Ce cas est moins courant dans la pratique.  
  
-   Le type doit être une primitive de langage XAML connue.  
  
### <a name="content-properties-and-collection-syntax-combined"></a>Combinaison des propriétés de contenu et de la syntaxe des collections  
 Considérez cet exemple :  
  
```xaml  
<StackPanel>  
  <Button>First Button</Button>  
  <Button>Second Button</Button>  
</StackPanel>  
```  
  
 Ici, chaque <xref:System.Windows.Controls.Button> est un élément enfant de <xref:System.Windows.Controls.StackPanel>. Il s’agit d’un balisage simple et intuitif qui omet deux balises pour deux raisons différentes.  
  
-   **Élément de propriété StackPanel.Children omis :** <xref:System.Windows.Controls.StackPanel> dérive <xref:System.Windows.Controls.Panel>. <xref:System.Windows.Controls.Panel>définit <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=nameWithType> comme son XAML propriété de contenu.  
  
-   **Élément objet UIElementCollection omis :** le <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=nameWithType> propriété prend le type <xref:System.Windows.Controls.UIElementCollection>, qui implémente <xref:System.Collections.IList>. Balise d’élément de la collection peut être omis, selon les règles XAML pour le traitement des collections telles que <xref:System.Collections.IList>. (Dans ce cas, <xref:System.Windows.Controls.UIElementCollection> réellement ne peut pas être instancié, car elle n’expose pas un constructeur par défaut, et c’est pourquoi le <xref:System.Windows.Controls.UIElementCollection> élément objet est indiqué comme commenté).  
  
```xaml  
<StackPanel>  
  <StackPanel.Children>  
    <!--<UIElementCollection>-->  
    <Button>First Button</Button>  
    <Button>Second Button</Button>  
    <!--</UIElementCollection>-->  
  </StackPanel.Children>  
</StackPanel>  
```  
  
### <a name="attribute-syntax-events"></a>Syntaxe des attributs (événements)  
 La syntaxe des attributs peut également servir pour les membres qui sont des événements plutôt que des propriétés. Dans ce cas, le nom de l’attribut est le nom de l’événement. Dans l’implémentation WPF d’événements pour XAML, la valeur de l’attribut est le nom d’un gestionnaire qui implémente le délégué de l’événement. Par exemple, le balisage suivant assigne un gestionnaire pour le <xref:System.Windows.Controls.Primitives.ButtonBase.Click> événement à un <xref:System.Windows.Controls.Button> créé dans la balise :  
  
 [!code-xaml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 Il existe plus d’événements et de code XAML dans WPF que cet exemple de syntaxe des attributs. Par exemple, vous vous demandez peut-être ce que le `ClickHandler` référencé ici représente et comment il est défini. C’est expliqué dans la section [Événements et code-behind XAML](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md#events_and_xaml_codebehind), plus loin dans cette rubrique.  
  
<a name="case_and_whitespace_in_xaml"></a>   
## <a name="case-and-whitespace-in-xaml"></a>Casse et espaces blancs en XAML  
 En général, XAML respecte la casse. Pour la résolution des types de stockage, XAML WPF respecte la casse en suivant les mêmes règles que celles que respecte le CLR. Les éléments objet, les éléments de propriété et les noms d’attribut doivent tous être spécifiés en respectant la casse quand leurs noms sont comparés au type sous-jacent dans l’assembly ou à un membre d’un type. Les primitives et les mots clés du langage XAML respectent également la casse. Par contre, les valeurs ne respectent pas toujours la casse. Pour les valeurs, le respect de la casse varie selon le comportement du convertisseur de type associé à la propriété qui prend la valeur ou le type de valeur de la propriété. Par exemple, les propriétés qui prennent le <xref:System.Boolean> type peut également accepter soit `true` ou `True` en tant que valeurs équivalentes, mais uniquement parce que la conversion de chaîne de type de l’analyseur XAML WPF natif <xref:System.Boolean> autorise déjà en tant qu’équivalents.  
  
 Les sérialiseurs et les processeurs XAML WPF doivent ignorer ou supprimer tous les espaces blancs non significatifs et normaliser tout espace blanc significatif. Cette pratique est conforme aux recommandations du comportement par défaut des espaces blancs dans la spécification XAML. Ce comportement ne porte généralement à conséquence que lorsque vous spécifiez des chaînes dans les propriétés de contenu XAML. Dit plus simplement, le XAML convertit espaces, sauts de ligne et tabulations en espaces, puis conserve un seul espace trouvé aux extrémités d’une chaîne contiguë. L’explication complète de la gestion des espaces blancs en XAML n’est pas couverte dans cette rubrique. Pour plus d’informations, consultez [Traitement des espaces blancs en XAML](../../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>Extensions de balisage  
 Les extensions de balisage forment un concept de langage XAML. Lorsqu’elles sont utilisées pour fournir la valeur d’une syntaxe d’attributs, les accolades (`{` et `}`) indiquent une extension de balisage. Cette utilisation ordonne au traitement XAML de se soustraire au traitement général des valeurs d’attribut, soit en tant que chaîne littérale, soit en tant que valeur convertible en chaîne.  
  
 Les extensions de balisage les plus courantes qui sont utilisées dans la programmation d’applications [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sont [Binding](../../../../docs/framework/wpf/advanced/binding-markup-extension.md), utilisée pour les expressions de liaison de données, et les références aux ressources [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) et [DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md). Grâce aux extensions de balisage, vous pouvez utiliser la syntaxe d’attributs pour fournir des valeurs aux propriétés, même si en général cette propriété ne prend pas en charge cette syntaxe. Les extensions de balisage utilisent souvent des types d’expression intermédiaires pour activer des fonctionnalités, telles que le traitement différé des valeurs ou le référencement d’autres objets qui sont uniquement présents au moment de l’exécution.  
  
 Par exemple, le balisage suivant définit la valeur de la <xref:System.Windows.FrameworkElement.Style%2A> propriété à l’aide de la syntaxe d’attribut. Le <xref:System.Windows.FrameworkElement.Style%2A> propriété utilise une instance de la <xref:System.Windows.Style> (classe), qui par défaut n’a pas pu être instancié par une chaîne de syntaxe d’attribut. Dans ce cas, par contre, l’attribut fait référence à une extension de balisage particulière, [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md). Lorsque cette extension de balisage est traitée, elle retourne une référence à un style qui a été instancié précédemment en tant que ressource indexée dans un dictionnaire de ressources.  
  
 [!code-xaml[FEResourceSH_snip#XAMLOvwShortResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources)]  
[!code-xaml[FEResourceSH_snip#XAMLOvwShortResources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources2)]  
[!code-xaml[FEResourceSH_snip#XAMLOvwShortResources3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources3)]  
  
 Pour obtenir la liste de référence de toutes les extensions de balisage XAML spécifiquement implémentées dans WPF, consultez [Extensions XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md). Pour une liste de référence des extensions de balisage définies par System.Xaml et faciles à se procurer pour les implémentations XAML .NET Framework, consultez [Fonctionnalités de langage pour les espace de noms XAML (x:)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md). Pour plus d’informations sur les concepts d’extension de balisage, consultez [Extensions de balisage et XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
<a name="type_converters"></a>   
## <a name="type-converters"></a>Convertisseurs de type  
 La section [Syntaxe XAML en bref](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md#xaml_syntax_in_brief) indique que la valeur d’attribut doit pouvoir être définie par une chaîne. La gestion native de base de la conversion des chaînes en d’autres types d’objets ou les valeurs primitives repose sur le <xref:System.String> type lui-même, en plus du traitement natif pour certains types tels que <xref:System.DateTime> ou <xref:System.Uri>. Cependant, plusieurs types [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ou membres de ces types étendent le comportement de traitement des attributs de chaîne de base, de telle sorte que les instances de types d’objets plus complexes peuvent être spécifiées comme des chaînes et des attributs.  
  
 Le <xref:System.Windows.Thickness> structure est un exemple d’un type qui a une conversion de type activée pour les utilisations de code XAML. <xref:System.Windows.Thickness>Indique des dimensions dans un rectangle imbriqué et est utilisé comme valeur pour les propriétés telles que <xref:System.Windows.FrameworkElement.Margin%2A>. En plaçant un convertisseur de type sur <xref:System.Windows.Thickness>, toutes les propriétés qui utilisent un <xref:System.Windows.Thickness> sont plus faciles à spécifier en XAML, car elles peuvent être spécifiées en tant qu’attributs. L’exemple suivant utilise une syntaxe d’attribut et de conversion de type pour fournir une valeur pour un <xref:System.Windows.FrameworkElement.Margin%2A>:  
  
 [!code-xaml[XAMLOvwSupport#MarginTCE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#margintce)]  
  
 L’exemple de syntaxe d’attribut précédent est équivalent à ce qui suit exemple de syntaxe plus complet, où le <xref:System.Windows.FrameworkElement.Margin%2A> est définie à la place via la syntaxe d’élément propriété contenant un <xref:System.Windows.Thickness> élément objet. Les quatre propriétés de clé de <xref:System.Windows.Thickness> sont définies en tant qu’attributs sur l’instance de :  
  
 [!code-xaml[XAMLOvwSupport#MarginVerbose](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#marginverbose)]  
  
> [!NOTE]
>  Il existe également un nombre limité d’objets pour lesquels la conversion de type est la seule manière publique de définir une propriété pour le type voulu, sans impliquer une sous-classe, car le type lui-même n’a pas de constructeur par défaut. Par exemple <xref:System.Windows.Input.Cursor>.  
  
 Pour plus d’informations sur la prise en charge de la conversion de type et de son utilisation avec la syntaxe d’attributs, consultez [TypeConverters et XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md).  
  
<a name="xaml_root_elements_and_xaml_namespaces"></a>   
## <a name="xaml-root-elements-and-xaml-namespaces"></a>Éléments racines  XAML et espaces de noms XAML  
 Un fichier XAML ne doit avoir qu’un seul élément racine afin d’être à la fois un fichier [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] correctement structuré et un fichier XAML valide. Pour des scénarios types WPF, vous utilisez un élément racine significatif dans le modèle d’application WPF (par exemple, <xref:System.Windows.Window> ou <xref:System.Windows.Controls.Page> pour une page, <xref:System.Windows.ResourceDictionary> pour un dictionnaire externe ou <xref:System.Windows.Application> pour la définition d’application). L’exemple suivant montre l’élément racine d’un fichier de type XAML pour un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] page, avec l’élément racine de <xref:System.Windows.Controls.Page>.  
  
 [!code-xaml[XAMLOvwSupport#RootOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly)]  
[!code-xaml[XAMLOvwSupport#RootOnly2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly2)]  
  
 L’élément racine contient également les attributs `xmlns` et `xmlns:x`. Ces attributs indiquent à un processeur XAML les espaces de noms XAML contenant les définitions de types pour les types de stockage qui vont être référencés en tant qu’éléments par le balisage. L’attribut `xmlns` indique explicitement l’espace de noms XAML par défaut. Dans l’espace de noms XAML par défaut, les éléments objet dans le balisage peuvent être spécifiés sans préfixe. Pour la plupart des scénarios d’application[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] et pour presque tous les exemples donnés dans les sections [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] du [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)], l’espace de noms XAML par défaut est mappé à l’espace de noms [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)]. L’attribut `xmlns:x` indique un espace de noms XAML supplémentaire qui mappe l’espace de noms du langage XAML [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)].  
  
 Cette utilisation de `xmlns` pour définir une étendue de l’utilisation et le mappage d’une portée de nom est conforme à la spécification XML 1.0. Les portées de nom XAML se distinguent des portées de nom XML uniquement parce qu’elles renseignent aussi sur la façon dont les éléments de la portée de nom sont stockés par les types lors d’une résolution de type et d’une analyse du code XAML.  
  
 Notez que les attributs `xmlns` ne sont strictement nécessaires que sur l’élément racine de chaque fichier XAML. Les définitions `xmlns` s’appliquent à tous les éléments descendants de l’élément racine (ce comportement est encore une fois conforme à la spécification XML 1.0 pour `xmlns`), tandis que les attributs `xmlns` sont également autorisés sur d’autres éléments situés sous la racine et s’appliquent à tous les éléments descendants de l’élément de définition. Toutefois, si vous définissez/redéfinissez fréquemment les espaces de noms XAML, le style de balisage XAML peut devenir difficile à lire.  
  
 L’implémentation [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de son processeur XAML inclut une infrastructure qui a connaissance des assemblys principaux WPF. Les assemblys principaux [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sont connus pour contenir les types qui prennent en charge les mappages [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] à l’espace de noms XAML par défaut. Cette option est activée par le biais de la configuration faisant partie du fichier de build de votre projet et des systèmes de projet et de build WPF. Par conséquent, déclarer l’espace de noms XAML par défaut comme `xmlns` par défaut est la seule chose à faire pour référencer les éléments XAML provenant des assemblys [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### <a name="the-x-prefix"></a>Le préfixe x:  
 Dans l’exemple d’élément racine précédent, le préfixe `x:` a été utilisé pour mapper l’espace de noms XAML [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)], qui est l’espace de noms XAML dédié prenant en charge les constructions du langage XAML. Ce préfixe `x:` est utilisé pour mapper cet espace de noms XAML dans les modèles de projets, les exemples et dans la documentation de ce [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)]. L’espace de noms XAML du langage XAML contient plusieurs constructions de programmation que vous allez être amené à utiliser très fréquemment dans votre XAML. Voici une liste de constructions de programmation avec le préfixe `x:` parmi les plus courantes que vous allez utiliser :  
  
-   [x : Key](../../../../docs/framework/xaml-services/x-key-directive.md): définit une clé unique pour chaque ressource dans un <xref:System.Windows.ResourceDictionary> (ou les concepts de dictionnaire semblables dans d’autres infrastructures). `x:Key` représente probablement 90 % des utilisations de `x:` que vous pouvez voir dans le balisage classique d’une application WPF.  
  
-   [x:Class](../../../../docs/framework/xaml-services/x-class-directive.md) : spécifie l’espace de noms [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] et le nom de la classe qui fournit le code-behind pour une page XAML. Vous devez disposer d’une telle classe pour prendre en charge le code-behind selon le modèle de programmation WPF, et c’est la raison pour laquelle vous voyez presque toujours `x:` mappé, même s’il n’ y a aucune ressource.  
  
-   [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) : spécifie un nom d’objet d’exécution pour l’instance qui existe dans le code d’exécution après le traitement d’un élément objet. En général, vous êtes amené à utiliser fréquemment une propriété équivalente définie par WPF pour [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md). Ces propriétés mappent spécifiquement à une propriété de stockage CLR et sont donc plus pratiques pour la programmation d’applications, où vous utilisez fréquemment du code d’exécution pour rechercher les éléments nommés à partir du XAML initialisé. La plus courante de ces propriétés sont <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=nameWithType>. Vous pouvez encore utiliser [x : Name](../../../../docs/framework/xaml-services/x-name-directive.md) lors de l’équivalent niveau infrastructure WPF <xref:System.Windows.FrameworkElement.Name%2A> propriété n’est pas prise en charge dans un type particulier. Ce cas se présente dans certains scénarios d’animation.  
  
-   [x:Static](../../../../docs/framework/xaml-services/x-static-markup-extension.md) : active une référence qui retourne une valeur statique qui, sinon, n’est pas une propriété compatible XAML.  
  
-   [x : Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md): construit une <xref:System.Type> référence basée sur un nom de type. Cela permet de spécifier des attributs qui prennent <xref:System.Type>, tel que <xref:System.Windows.Style.TargetType%2A?displayProperty=nameWithType>, bien que la fréquence à laquelle la propriété a chaîne native-à-<xref:System.Type> conversion de manière qui le [x : Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md) est de l’extension de balisage facultatif.  
  
 Il existe d’autres constructions de programmation dans l’espace de noms XAML à préfixe `x:` qui ne sont pas aussi courantes. Pour plus d’informations, consultez [Fonctionnalités de langage pour les espaces de noms XAML (x:)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md).  
  
<a name="custom_prefixes_and_custom_types_in_xaml"></a>   
## <a name="custom-prefixes-and-custom-types-in-xaml"></a>Préfixes personnalisés et types personnalisés en XAML  
 Pour vos propres assemblys personnalisés ou pour des assemblys hors du noyau WPF de PresentationCore, PresentationFramework et WindowsBase, vous pouvez spécifier l’assembly en question dans le cadre d’un mappage `xmlns` personnalisé. Vous pouvez ensuite référencer des types depuis cet assembly dans votre XAML à partir du moment où le type voulu est correctement implémenté pour prendre en charge les utilisations XAML que vous essayez.  
  
 Voici un exemple très simple de fonctionnement des préfixes personnalisés dans le balisage XAML. Le préfixe `custom` est défini dans la balise d’élément racine et mappé à un assembly spécifique qui est empaqueté et disponible avec l’application. Cet assembly contient un type `NumericUpDown`, qui est implémenté pour prendre en charge l’utilisation générale de XAML ainsi que l’utilisation d’un héritage de classe, autorisant son insertion à ce stade dans un modèle de contenu XAML WPF. Une instance de ce contrôle `NumericUpDown` est déclaré comme élément objet en utilisant le préfixe afin qu’un analyseur XAML identifie quel espace de noms XAML contient le type et par conséquent l’emplacement de l’assembly de stockage contenant la définition de type.  
  
```  
<Page  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"   
    xmlns:custom="clr-namespace:NumericUpDownCustomControl;assembly=CustomLibrary"  
    >  
  <StackPanel Name="LayoutRoot">  
    <custom:NumericUpDown Name="numericCtrl1" Width="100" Height="60"/>  
...  
  </StackPanel>  
</Page>  
```  
  
 Pour plus d’informations sur les types personnalisés en XAML, consultez [XAML et les classes personnalisées pour WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md).  
  
 Pour plus d’informations sur la relation entre les espaces de noms du code de stockage dans les assemblys et les espaces de noms XML, consultez [Espaces de noms XAML et mappage d’espaces de noms pour XAML WPF](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
<a name="events_and_xaml_codebehind"></a>   
## <a name="events-and-xaml-code-behind"></a>Événements et code-Behind XAML  
 La plupart des applications [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] se composent de balises XAML et de code-behind. Dans un projet, le code XAML est écrit sous la forme d’un fichier `.xaml` et d’un langage [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], si bien que [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] ou [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] est utilisé pour écrire un fichier code-behind. Lors de la compilation du balisage d’un fichier XAML comme partie intégrante des modèles de programmation et d’application WPF, l’emplacement du fichier code-behind XAML pour un fichier XAML est identifié en spécifiant un espace de noms et une classe en tant qu’attribut `x:Class` de l’élément racine du XAML.  
  
 Jusqu’ici dans les exemples étudiés, vous avez vu plusieurs boutons, mais aucun d’eux n’avait encore de comportement logique qui lui était associé. Au niveau de l’application, le mécanisme principal permettant d’ajouter un comportement à un élément objet consiste à utiliser un événement existant de la classe élément et à écrire un gestionnaire spécifique pour cet événement qui est appelé lorsque l’événement est déclenché au moment de l’exécution. Le nom de l’événement et celui du gestionnaire à utiliser sont spécifiés dans le balisage, tandis que le code qui implémente le gestionnaire est défini dans le fichier code-behind.  
  
 [!code-xaml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 [!code-csharp[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml.cs#buttonwithcodebehindhandler)]
 [!code-vb[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#buttonwithcodebehindhandler)]  
  
 Notez que le fichier code-behind utilise l’espace de noms CLR `ExampleNamespace` et déclare `ExamplePage` comme une classe partielle dans cet espace de noms. Cela correspond à la valeur d’attribut `x:Class` de `ExampleNamespace`.`ExamplePage` qui a été fournie dans la racine de la balise. Le compilateur de balisage WPF crée une classe partielle pour tout fichier XAML compilé, en dérivant une classe à partir du type d’élément racine. Lorsque vous fournissez le code-behind qui définit également la même classe partielle, le code résultant est combiné dans le même espace de noms et la même classe de l’application compilée.  
  
 Pour plus d’informations sur la configuration requise liée à la programmation de code-behind dans WPF, consultez la section « Exigences concernant le code-behind, le gestionnaire d’événements et les classes partielles » dans [Code-Behind et XAML dans WPF](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md).  
  
 Si vous ne souhaitez pas créer de fichier code-behind distinct, vous pouvez également incorporer votre code dans un fichier XAML. Toutefois, le code incorporé est une technique moins flexible qui présente des limitations importantes. Pour plus d’informations, consultez [Code-behind et XAML dans WPF](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md).  
  
### <a name="routed-events"></a>Événements routés  
 Un événement routé est une fonctionnalité d’événement particulière qui est fondamentale pour [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Les événements routés permettent à un élément de gérer un événement déclenché par un élément différent, tant que ces éléments sont connectés via une relation d’arborescence. Lorsque vous spécifiez la gestion des événements avec un attribut XAML, vous pouvez écouter et géré l’événement routé sur n’importe quel élément, notamment les éléments qui ne listent pas cet événement particulier dans la table des membres de la classe. Pour cela, vous devez qualifier l’attribut de nom d’événement avec le nom de la classe propriétaire. Par exemple, le parent `StackPanel` dans le cours `StackPanel`  /  `Button` exemple peut enregistrer un gestionnaire pour du bouton élément enfant <xref:System.Windows.Controls.Primitives.ButtonBase.Click> événement en spécifiant l’attribut `Button.Click` sur la `StackPanel` élément de l’objet, avec le nom de votre gestionnaire comme valeur d’attribut. Pour plus d’informations sur les événements routés, consultez [Vue d’ensemble des événements routés](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
<a name="x_name_and_xaml_named_elements"></a>   
## <a name="xaml-named-elements"></a>Éléments nommés XAML  
 Par défaut, l’instance d’objet qui est créée par le traitement d’un élément objet XAML dans un graphique d’objet n’a pas d’identificateur unique ni de référence d’objet. En revanche, si vous appelez un constructeur dans le code, vous utilisez presque toujours le résultat du constructeur pour définir une variable sur l’instance construite, afin de pouvoir référencer l’instance ultérieurement dans votre code. Pour fournir un accès standardisé aux objets créés via une définition de balise, XAML définit l’[attribut x:Name](../../../../docs/framework/xaml-services/x-name-directive.md). Vous pouvez définir la valeur de l’attribut `x:Name` sur n’importe quel élément objet. Dans votre code-behind, l’identificateur que vous choisissez équivaut à une variable d’instance qui fait référence à l’instance construite. Dans tous les cas, les éléments nommés fonctionnent comme s’ils étaient des instances d’objet (le nom fait référence à cette instance) et votre code-behind peut référencer les éléments nommés pour gérer les interactions au moment de l’exécution dans l’application. Cette connexion entre instances et variables est accomplie par le compilateur de balisage XAML WPF, et implique plus spécifiquement des fonctionnalités et des modèles tels que <xref:System.Windows.Markup.IComponentConnector.InitializeComponent%2A> qui ne seront pas abordés en détail dans cette rubrique.  
  
 Les éléments XAML de niveau infrastructure WPF héritent un <xref:System.Windows.FrameworkElement.Name%2A> propriété, qui est équivalente au code XAML défini `x:Name` attribut. Certaines autres classes fournissent également des équivalents de niveau propriété pour `x:Name`, qui est aussi généralement défini en tant que propriété `Name`. En règle générale, si vous ne trouvez pas une propriété `Name` dans la table des membres pour votre élément/type choisi, utilisez `x:Name` à la place. Le `x:Name` valeurs fourniront un identificateur à un élément XAML qui peut servir à l’exécution, par les sous-systèmes spécifiques ou par les méthodes utilitaire telles que <xref:System.Windows.FrameworkElement.FindName%2A>.  
  
 L’exemple suivant définit <xref:System.Windows.FrameworkElement.Name%2A> sur un <xref:System.Windows.Controls.StackPanel> élément. Ensuite, un gestionnaire d’un <xref:System.Windows.Controls.Button> dans ce <xref:System.Windows.Controls.StackPanel> références le <xref:System.Windows.Controls.StackPanel> via sa référence d’instance `buttonContainer` comme défini par <xref:System.Windows.FrameworkElement.Name%2A>.  
  
 [!code-xaml[XAMLOvwSupport#NamedE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede)]  
[!code-xaml[XAMLOvwSupport#NamedE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede2)]  
  
 [!code-csharp[XAMLOvwSupport#NameCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml.cs#namecode)]
 [!code-vb[XAMLOvwSupport#NameCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#namecode)]  
  
 Tout comme une variable, le nom XAML d’une instance est régi par un concept de portée afin que les noms puissent être appliqués pour être uniques dans une certaine étendue qui est prévisible. La balisage principal qui définit une page désigne une portée de nom XAML unique, avec pour élément racine de cette page, les limites de portée de nom XAML. Toutefois, d’autres sources de balisage peuvent interagir avec une page au moment de l’exécution, telles que les styles ou les modèles dans les styles, et ces sources possèdent souvent leur propre portée de nom XAML qui ne se connecte pas nécessairement à la portée de nom XAML de la page. Pour plus d’informations sur `x:Name` et portées de nom XAML, consultez <xref:System.Windows.FrameworkElement.Name%2A>, [Directive x : Name](../../../../docs/framework/xaml-services/x-name-directive.md), ou [portées de nom XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md).  
  
<a name="attached_properties_and_attached_events"></a>   
## <a name="attached-properties-and-attached-events"></a>Propriétés jointes et événements attachés  
 Le langage XAML comporte une fonctionnalité de langage qui permet à certaines propriétés ou événements d’être spécifiés sur n’importe quel élément, et cela même si la propriété ou l’événement existe dans les définitions de type pour l’élément sur lequel il est défini. La version des propriétés de cette fonctionnalité est appelée une propriété jointe, et la version des événements, un événement attaché. D’un point de vue conceptuel, vous pouvez considérer les propriétés jointes et les événements attachés comme des membres globaux pouvant être définis sur n’importe quelle instance d’élément ou d’objet XAML. Toutefois, cet élément/cette classe ou une infrastructure plus importante doit prendre en charge une banque de propriétés de stockage pour les valeurs attachées.  
  
 Les propriétés jointes en XAML sont généralement utilisées dans la syntaxe d’attributs. Dans la syntaxe d’attributs, vous spécifiez une propriété jointe sous la forme *typePropriétaire*.*nomPropriété*.  
  
 En apparence, cela ressemble à une utilisation d’élément de propriété, mais dans ce cas le *typePropriétaire* que vous spécifiez est toujours un type différent de l’élément objet dans lequel la propriété jointe est définie. *typePropriétaire* est le type qui fournit les méthodes d’accesseur demandées par un processeur XAML pour obtenir ou définir la valeur de propriété jointe.  
  
 Le scénario le plus courant pour les propriétés jointes consiste à permettre aux éléments enfants de signaler une valeur de propriété à leur élément parent.  
  
 L’exemple suivant illustre le <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> propriété jointe. Le <xref:System.Windows.Controls.DockPanel> classe définit les accesseurs de <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> et par conséquent possède la propriété jointe. Le <xref:System.Windows.Controls.DockPanel> classe inclut également une logique qui itère au sein de ses éléments enfants et spécifiquement vérifie chaque élément pour une valeur définie de <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>. Si une valeur est trouvée, cette valeur est utilisée au cours de la disposition pour positionner les éléments enfants. Utilisation de la <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> propriété jointe et cette fonctionnalité de positionnement est en fait le scénario motivant pour la <xref:System.Windows.Controls.DockPanel> classe.  
  
 [!code-xaml[XAMLOvwSupport#DockAP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#dockap)]  
  
 Dans [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la plus grande partie ou la totalité des propriétés jointes sont également implémentées en tant que propriétés de dépendance. Pour plus d’informations, consultez [Vue d’ensemble des propriétés jointes](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
 Les événements attachés utilisent une forme *typePropriétaire*. *nomÉvénement* similaire à la syntaxe d’attributs. À l’instar des événements non attachés, la valeur d’attribut d’un événement attaché en XAML spécifie le nom de la méthode de gestionnaire qui est appelée lorsque l’événement est géré sur l’élément. Les utilisations d’événements attachés en XAML WPF sont moins courantes. Pour plus d’informations, consultez [Vue d’ensemble des événements attachés](../../../../docs/framework/wpf/advanced/attached-events-overview.md).  
  
<a name="base_classes_and_xaml"></a>   
## <a name="base-types-and-xaml"></a>Types de base et XAML  
 Le XAML WPF sous-jacent et son espace de noms XAML représentent une collection de types correspondant aux objets [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] auxquels s’ajoutent des éléments de balisage pour XAML. Cela étant, toutes les classes ne peuvent pas être mappées aux éléments. Classes abstraites, telles que <xref:System.Windows.Controls.Primitives.ButtonBase>, et certaines classes de base non abstraites sont utilisés pour l’héritage dans le [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] modèle d’objets. Les classes de base, y compris abstraites, sont toujours importantes pour le développement en XAML, car chacun des éléments XAML concrets hérite de membres provenant d’une classe de base dans sa hiérarchie. Ces membres incluent souvent des propriétés qui peuvent être définies en tant qu’attributs sur l’élément, ou comme événements qui peuvent être gérés. <xref:System.Windows.FrameworkElement>est la base concrète [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] classe de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] au niveau de l’infrastructure WPF. Lors de la conception [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], vous allez utiliser diverses forme, panneau de configuration, decorator ou dérivent de classes de contrôle, dont toutes les <xref:System.Windows.FrameworkElement>. Une classe de base connexe <xref:System.Windows.FrameworkContentElement>, prend en charge des éléments orientés document qui fonctionnent bien pour une présentation de disposition de flux, à l’aide de [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] qui reflètent délibérément la [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] dans <xref:System.Windows.FrameworkElement>. La combinaison d’attributs au niveau de l’élément et d’un modèle d’objet [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] vous fournit un ensemble de propriétés communes qui peuvent être définies sur les éléments XAML les plus concrets, quel que soit l’élément XAML spécifique et son type sous-jacent.  
  
<a name="xaml_security"></a>   
## <a name="xaml-security"></a>Sécurité XAML  
 Le XAML est un langage de balisage qui représente directement l’instanciation d’objets et leur exécution. Ainsi, les éléments créés en XAML ont la même capacité d’interagir avec les ressources système (accès réseau, e/s de système de fichiers, par exemple) que le code généré équivalent.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] prend en charge le framework de sécurité [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] [!INCLUDE[TLA#tla_cas](../../../../includes/tlasharptla-cas-md.md)]. Cela signifie que le contenu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] en cours d’exécution dans la zone Internet dispose d’autorisations d’exécution réduites. Le « XAML libre » (pages de code XAML non compilé, interprétées au moment du chargement par une visionneuse XAML) et [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] sont généralement exécutés dans cette zone internet et utilisent le même jeu d’autorisations.  Toutefois, le XAML chargé dans une application d’un niveau de confiance totale dispose du même accès aux ressources système que l’application d’hébergement. Pour plus d’informations, consultez [Sécurité de confiance partielle de WPF](../../../../docs/framework/wpf/wpf-partial-trust-security.md).  
  
<a name="loading_xaml_from_code"></a>   
## <a name="loading-xaml-from-code"></a>Chargement de XAML à partir du code  
 Vous utilisez XAML pour définir l’ensemble de l’interface utilisateur, mais il est parfois également judicieux de ne définir qu’une partie de l’interface utilisateur en XAML. Vous pouvez vous servir de cette fonctionnalité pour activer la personnalisation partielle, un stockage local des informations, et utiliser XAML pour fournir un objet métier ou une variété de scénarios possibles. La clé de ces scénarios est la <xref:System.Windows.Markup.XamlReader> classe et ses <xref:System.Windows.Markup.XamlReader.Load%2A> (méthode). L’entrée est un fichier XAML, et la sortie un objet représentant l’intégralité de l’arborescence d’exécution des objets qui a été créée à partir de ce balisage. Vous pouvez ensuite insérer l’objet pour qu’il soit une propriété d’un autre objet existant déjà dans l’application. Tant que la propriété est une propriété appropriée dans le modèle de contenu, qui a des capacités d’affichage final et informe le moteur d’exécution de l’ajout de nouveau contenu à l’application, vous pouvez modifier très facilement un contenu d’application en cours d’exécution par le chargement en XAML. Notez que cette fonctionnalité n’est généralement disponible que dans les applications dotées d’un niveau de confiance totale, en raison des implications évidentes en matière de sécurité du chargement de fichiers dans des applications en cours d’exécution.  
  
<a name="whats_next"></a>   
## <a name="whats-next"></a>Étapes suivantes  
 Cette rubrique présente une introduction générale de la terminologie et des concepts de la syntaxe XAML, tels qu’ils s’appliquent à WPF. Pour plus d’informations sur les termes utilisés ici, consultez [Syntaxe XAML en détail](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 Si vous ne le n'avez pas déjà fait, essayez les exercices de la rubrique du didacticiel [procédure pas à pas : Ma première application de bureau WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md). En créant l’application centrée sur le balisage qui est décrite dans le didacticiel, vous renforcez l’assimilation de la plupart des concepts décrits dans cette rubrique.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]utilise un modèle d’application particulier qui est basé sur la <xref:System.Windows.Application> classe. Pour plus d’informations, consultez [Vue d’ensemble de la gestion d’applications](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
 [Génération d’une application WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md) vous donne plus de détails sur la création d’applications XAML inclusives à partir de la ligne de commande et avec [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)].  
  
 [Vue d’ensemble des propriétés de dépendance](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md) vous renseigne davantage sur la polyvalence des propriétés dans [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] et présente le concept des propriétés de dépendance.  
  
## <a name="see-also"></a>Voir aussi  
 [Syntaxe XAML en détail](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)  
 [XAML et classes personnalisées pour WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)  
 [Fonctionnalités de langage pour les espaces de noms XAML (x:)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)  
 [Extensions XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)  
 [Vue d’ensemble des éléments de base](../../../../docs/framework/wpf/advanced/base-elements-overview.md)  
 [Arborescences dans WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)
