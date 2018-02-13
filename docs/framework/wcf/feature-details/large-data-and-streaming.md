---
title: "Données volumineuses et diffusion en continu"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab2851f5-966b-4549-80ab-c94c5c0502d2
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e9551fcf4f302be899dcee8737b3bcfad15f1210
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="large-data-and-streaming"></a>Données volumineuses et diffusion en continu
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] est une infrastructure de communications basées sur XML. Étant donné que les données XML sont souvent codées au format texte standard défini dans le [spécification XML 1.0](http://go.microsoft.com/fwlink/?LinkId=94838)et connectées, les architectes et développeurs de systèmes sont généralement concerne l’encombrement du câble (ou taille) de messages envoyés entre le réseau et l’encodage de texte XML pose des défis particuliers pour le transfert efficace de données binaires.  
  
## <a name="basic-considerations"></a>Considérations de base  
 Pour fournir des informations générales à propos des informations suivantes pour [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], cette section souligne quelques préoccupations et considérations générales pour les encodages, les données binaires et la diffusion en continu qui s'appliquent généralement aux infrastructures des systèmes connectés.  
  
### <a name="encoding-data-text-vs-binary"></a>Encodage de données : texte et Binaire  
 Les préoccupations couramment exprimées par les développeurs incluent l’idée que le XML possède une charge mémoire considérable par rapport aux formats binaires en raison de la nature répétitive des étiquettes de début et de fin, que l’encodage de valeurs numériques est considéré comme nettement plus volumineux parce qu’elles sont exprimées en valeurs texte, et que ces données binaires ne peuvent pas être exprimées efficacement parce qu’elles doivent être encodées spécialement à des fins d’incorporation dans un format texte.  
  
 Même si de nombreuses préoccupations comme celle-ci ainsi que d'autres sont justifiées, la différence réelle entre les messages à encodage texte XML dans un environnement de services Web XML et les messages à encodage binaire dans un environnement d'appel de procédure distante (RPC) hérité est souvent beaucoup moins importante que la considération initiale peut le suggérer.  
  
 Alors que les messages à encodage texte XML sont transparents et lisibles par l'utilisateur, les messages binaires sont souvent assez opaques en comparaison et difficiles à décoder sans outils. Cette différence de lisibilité amène à négliger le fait que ces messages binaires comportent aussi souvent des métadonnées inline dans la charge utile, ce qui ajoute une charge mémoire tout comme avec les messages texte XML. Ceci s'avère particulièrement vrai pour les formats binaires qui ont pour but de fournir des fonctionnalités de couplage faible et d'appel dynamique.  
  
 Toutefois, les formats binaires comportent généralement ces métadonnées descriptives dans un « en-tête », qui déclare également le format de données pour les enregistrements de données suivants. La charge utile suit ensuite cette déclaration de blocs de métadonnées communes avec une charge mémoire supplémentaire minime. Par opposition, le XML englobe chaque élément de données dans un élément ou attribut afin que les métadonnées englobantes soient incluses de façon répétitive pour chaque objet de charge utile sérialisé. En conséquence, la taille d'un objet de charge utile sérialisé unique est semblable si vous comparez les représentations texte et binaires étant donné que des métadonnées descriptives doivent être exprimées pour les deux, mais le format binaire tire parti de la description des métadonnées partagées avec chaque objet de charge utile supplémentaire transféré en raison d'une charge mémoire totale inférieure.  
  
 Pourtant, pour certains types de données, tels que les nombres, il peut exister un inconvénient à l'utilisation de représentations numériques binaires à taille fixe, telles qu'un type décimal de 128 bits au lieu du texte brut, car la représentation de texte brut peut être inférieure de plusieurs octets. Les données texte peuvent également présenter des avantages de taille par rapport au choix de l'encodage basé sur le texte XML en général plus flexible, alors que certains formats binaires peuvent être par défaut des formats Unicode à 16 bits ou même 32 bits, qui ne s'appliquent pas au format XML binaire .NET.  
  
 Par conséquent, pour choisir le format texte ou le format binaire, il ne suffit pas de partir du principe que les messages binaires sont toujours plus petits que les messages texte XML.  
  
 Un avantage net des messages texte XML est qu'ils sont basés sur des normes et qu'ils offrent le choix le plus large d'options d'interopérabilité et de prise en charge de plateformes. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la section « Encodages » plus loin dans cette rubrique.  
  
### <a name="binary-content"></a>Contenu binaire  
 Un domaine dans lequel les encodages binaires sont supérieurs aux encodages basés sur le texte en termes de taille des messages obtenus concerne les éléments de données binaires volumineux tels que les photos, vidéos, clips audio ou tout autre forme de données binaires et opaques qui doivent être échangées entre des services et leurs consommateurs. Pour adapter ces types de données au texte XML, l'approche courante consiste à les encoder à l'aide d'un encodage Base64.  
  
 Dans une chaîne encodée en Base64, chaque caractère représente 6 bits des données de 8 bits d'origine, ce qui donne un rapport encodage/charge mémoire de 4:3 pour Base64, en ne comptant pas les caractères de mise en forme supplémentaires (retour chariot/saut de ligne) habituellement ajoutés par convention. Alors que l'importance des différences entre les encodages XML et binaire dépend en général du scénario, un gain de taille de plus de 33 % lors d'une transmission d'une charge utile de 500 Mo n'est habituellement pas acceptable.  
  
 Pour éviter cette charge lié à l'encodage, la norme MTOM (Message Transmission Optimization Mechanism) tient compte de l'extériorisation des éléments de données volumineux contenus dans un message et de leur transport avec le message en tant que données binaires sans encodage spécial. Avec MTOM, les messages sont échangés de façon similaire aux messages de messagerie SMTP Simple Mail Transfer Protocol () avec les pièces jointes ou le contenu incorporé (images et autre contenu incorporé) ; Les messages MTOM sont empaquetés en tant que séquences MIME multipart/connexes avec la partie racine constituant le message SOAP réel.  
  
 Un message SOAP MTOM est modifié par rapport à sa version non encodée afin que les étiquettes d’éléments spéciales qui font référence aux parties MIME respectives prennent la place des éléments d’origine dans le message contenait des données binaires. En conséquence, le message SOAP fait référence au contenu binaire en pointant vers les parties MIME envoyées avec lui, mais sinon il transporte uniquement les données texte XML. Parce que ce modèle s'aligne étroitement sur le modèle SMTP bien établi, il existe une large prise en charge d'outils permettant d'encoder et de décoder les messages MTOM sur de nombreuses plateformes, ce qui en fait un choix extrêmement interopérable.  
  
 Pour autant, comme avec Base64, MTOM s'accompagne également d'une charge mémoire nécessaire pour le format MIME, de sorte que les avantages de l'utilisation de MTOM s'aperçoivent uniquement quand la taille d'un élément de données binaires dépasse 1 Ko environ. En raison de la charge mémoire, les messages encodés MTOM peuvent être plus volumineux que les messages qui utilisent l'encodage Base64 pour les données binaires, si la charge utile binaire reste sous ce seuil. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la section « Encodages » plus loin dans cette rubrique.  
  
### <a name="large-data-content"></a>Contenu de données volumineux  
 L'encombrement du câble mis de côté, la charge utile de 500 Mo précédemment mentionnée représente également un grand challenge local pour le service et le client. Par défaut, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] traite les messages dans *mode mémoire tampon*. Cela signifie que le contenu entier d'un message est présent en mémoire avant son envoi ou après sa réception. Alors qu’il s’agit d’une bonne stratégie pour la plupart des scénarios et qu’elle est nécessaire pour les fonctionnalités de messagerie telles que les signatures numériques et la remise fiable, les messages volumineux peuvent épuiser les ressources d’un système.  
  
 La stratégie permettant de gérer les grandes charges utiles est la diffusion en continu. Alors que les messages, surtout ceux exprimés en XML, sont généralement considérés comme des packages de données relativement compacts, un message peut avoir une taille de plusieurs giga-octets et ressembler à un flux de données continu plus qu'à un package de données. Lorsque les données sont transférées en mode de diffusion en continu plutôt qu'en mode mémoire tampon, l'expéditeur rend le contenu du corps du message disponible au destinataire sous la forme d'un flux, et l'infrastructure du message transfère en continu les données de l'expéditeur au destinataire au fur et à mesure de leur disponibilité.  
  
 Le scénario le plus courant dans lequel de tels transferts de contenu de données volumineux se produisent implique les transferts d'objets de données binaires qui :  
  
-   ne peuvent pas être facilement divisés en séquence de message ;  
  
-   doivent être remis de façon opportune ;  
  
-   ne sont pas disponibles dans leur intégralité lors de l'initialisation du transfert.  
  
 Pour les données qui ne présentent pas ces contraintes, il est en général préférable d'envoyer des séquences de messages au sein de la portée d'une session plutôt qu'un message volumineux. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la section « Diffusion en continu de données » plus loin dans cette rubrique.  
  
 Lors de l’envoi de grandes quantités de données, vous devez définir le `maxAllowedContentLength` le paramètre IIS (pour plus d’informations, consultez [configuration des limites des demandes IIS](http://go.microsoft.com/fwlink/?LinkId=253165)) et le `maxReceivedMessageSize` paramètre de liaison (par exemple [ System.ServiceModel.BasicHttpBinding.MaxReceivedMessageSize](xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A) ou <xref:System.ServiceModel.NetTcpBinding.MaxReceivedMessageSize%2A>). Le `maxAllowedContentLength` propriété par défaut 28,6 M et `maxReceivedMessageSize` propriété valeur par défaut est 64 Ko.  
  
## <a name="encodings"></a>Encodages  
 Un *codage* définit un ensemble de règles sur la façon de présenter des messages sur le câble. Un *encodeur* implémente un tel encodage et est responsable du côté expéditeur, pour activer un <xref:System.ServiceModel.Channels.Message> message en mémoire dans un flux d’octets ou de la mémoire tampon d’octets qui peut être envoyé sur le réseau. Du côté destinataire, l'encodeur transforme une séquence d'octets en un message en mémoire.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inclut trois encodeurs et vous permet d’écrire et incorporer vos propres encodeurs, si nécessaire.  
  
 Chacune des liaisons standard inclut un encodeur préconfiguré, selon lequel les liaisons avec le préfixe Net* utilisent l'encodeur binaire (en incluant la classe <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>) pendant que les classes <xref:System.ServiceModel.BasicHttpBinding> et <xref:System.ServiceModel.WSHttpBinding> utilisent l'encodeur de message texte par défaut (au moyen de la classe <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>).  
  
|Élément de liaison d'encodeur|Description|  
|-----------------------------|-----------------|  
|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>|L’encodeur de message texte constitue l’encodeur par défaut de toutes les liaisons HTTP et le choix approprié pour toutes les liaisons personnalisées où l’interopérabilité est la première préoccupation. Cet encodeur lit et écrit les messages texte SOAP 1.1/SOAP 1.2 standard sans gestion spéciale des données binaires. Si la <xref:System.ServiceModel.Channels.MessageVersion> d'un message a la valeur `None`, le wrapper d'enveloppe SOAP est omis à partir de la sortie et seul le contenu du corps du message est sérialisé.|  
|<xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>|L’encodeur de message MTOM est un encodeur de texte qui implémente une gestion spéciale pour les données binaires et qui n’est pas utilisé par défaut dans chacune des liaisons standard parce qu’il s’agit strictement d’un utilitaire d’optimisation au cas par cas. Si le message contient des données binaires qui dépassent un seuil auquel l'encodage MTOM apporte un avantage, les données sont externalisées dans une partie MIME qui suit l'enveloppe de message. Consultez le paragraphe Activation de MTOM plus loin dans cette section.|  
|<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>|L'encodeur de message binaire est l'encodeur par défaut pour les liaisons Net* et le choix approprié chaque fois que les deux parties qui communiquent sont basées sur [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. L'encodeur de message binaire utilise le format XML binaire .NET, une représentation binaire spécifique à Microsoft pour les jeux d'informations XML qui en général engendre un plus petit encombrement que la représentation XML 1.0 équivalente et qui encode les données binaires en un flux d'octets.|  
  
 L’encodage de message texte constitue en général le meilleur choix pour tout chemin de communication qui requiert une interopérabilité, alors que l’encodage de message binaire constitue le meilleur choix pour tous les autres chemins de communication. L'encodage de message binaire engendre généralement des tailles de message plus petites par rapport au texte d'un message unique et des tailles progressivement encore plus petites sur la durée d'une session de communication. À la différence de l'encodage de texte, l'encodage binaire ne doit pas utiliser une gestion spéciale pour les données binaires, telle que l'utilisation de Base64, mais il représente les octets comme des octets.  
  
 Si votre solution ne requiert pas une interopérabilité, mais que vous souhaitez quand même utiliser le transport HTTP, vous pouvez composer un <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> dans une liaison personnalisée qui utilise la classe <xref:System.ServiceModel.Channels.HttpTransportBindingElement> pour le transport. Si plusieurs clients sur votre service ont besoin d'interopérabilité, il est recommandé d'exposer des points de terminaison parallèles qui ont tous le transport approprié et le choix de l'encodage pour les clients respectifs activés.  
  
### <a name="enabling-mtom"></a>Activation de MTOM  
 Lorsque l'interopérabilité est une condition requise et que vous devez envoyer des données binaires volumineuses, l'encodage de message MTOM constitue la stratégie d'encodage alternative que vous pouvez activer sur les liaisons <xref:System.ServiceModel.BasicHttpBinding> ou <xref:System.ServiceModel.WSHttpBinding> standard en affectant à la propriété `MessageEncoding` respective la valeur <xref:System.ServiceModel.WSMessageEncoding.Mtom> ou en composant le <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> dans une <xref:System.ServiceModel.Channels.CustomBinding>. L’exemple de code suivant, extraite de la [encodage MTOM](../../../../docs/framework/wcf/samples/mtom-encoding.md) exemple illustre l’activation de MTOM dans la configuration.  
  
```xml  
<system.serviceModel>  
     …  
    <bindings>  
      <wsHttpBinding>  
        <binding name="ExampleBinding" messageEncoding="Mtom"/>  
      </wsHttpBinding>  
    </bindings>  
     …  
<system.serviceModel>  
```  
  
 Comme mentionné précédemment, la décision d'utiliser l'encodage MTOM dépend du volume des données que vous envoyez. En outre, parce que MTOM est activé au niveau de la liaison, l'activation de MTOM a des répercussions sur toutes les opérations sur un point de terminaison donné.  
  
 Étant donné que l'encodeur MTOM émet toujours un message MIME/multi-part encodé par MTOM, que les données binaires finissent par être externalisées ou non, vous devez en général activer MTOM uniquement pour les points de terminaison qui échangent des messages contenant plus de 1 Ko de données binaires. En outre, les contrats de service conçus pour une utilisation avec des points de terminaison activés pour MTOM doivent, lorsque cela est possible, être contraints à la spécification de telles opérations de transferts de données. Les fonctionnalités de contrôle associées doivent se trouver sur un contrat distinct. Cette règle « MTOM uniquement » s'applique uniquement aux messages envoyés via un point de terminaison activé pour MTOM. L'encodeur MTOM peut également décoder et analyser les messages non-MTOM entrants.  
  
 L'utilisation de l'encodeur MTOM est compatible avec toutes les autres fonctionnalités [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Notez qu'il peut ne pas être possible d'observer cette règle dans tous les cas, par exemple lorsque la prise en charge des sessions est requise.  
  
### <a name="programming-model"></a>Modèle de programmation  
 Quel que soit l'encodeur intégré que vous utilisiez dans votre application parmi les trois disponibles, l'expérience en matière de programmation est identique en ce qui concerne le transfert de données binaires. La différence réside dans la manière dont [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gère les données en fonction de leurs types.  
  
```  
[DataContract]  
class MyData  
{  
    [DataMember]  
    byte[] binaryBuffer;  
    [DataMember]  
    string someStringData;  
}   
```  
  
 Lors de l'utilisation de MTOM, le contrat de données précédent est sérialisé d'après les règles suivantes :  
  
-   Si `binaryBuffer` n'a pas la valeur `null` et contient individuellement assez de données pour justifier une charge mémoire d'externalisation MTOM (en-têtes MIME, et ainsi de suite) par rapport à un encodage Base64, les données sont externalisées et transportées avec le message en tant que partie MIME binaire. Si le seuil n'est pas dépassé, les données sont encodées en tant que Base64.  
  
-   La chaîne (et tous les autres types qui ne sont pas binaires) est toujours représentée comme une chaîne à l'intérieur du corps du message, indépendamment de sa taille.  
  
 L'effet sur l'encodage MTOM est le même, que vous utilisiez un contrat de données explicite, comme indiqué dans l'exemple précédent, une liste de paramètres dans une opération, des contrats de données imbriqués ou que vous transfériez un objet de contrat de données dans une collection. Les tableaux d'octets sont toujours des candidats à l'optimisation et sont optimisés si les seuils d'optimisation sont atteints.  
  
> [!NOTE]
>  Vous ne devez pas utiliser des types dérivés <xref:System.IO.Stream?displayProperty=nameWithType> dans les contrats de données. Les données de flux doivent être communiquées à l'aide du modèle de diffusion en continu, expliqué dans la section « Diffusion en continu de données » ci-après.  
  
## <a name="streaming-data"></a>Diffusion en continu de données  
 Lorsque vous avez une grande quantité de données à transférer, le mode de transfert par diffusion en continu dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] est une alternative possible au comportement par défaut de mise en mémoire tampon et de traitement des messages en mémoire dans leur intégralité.  
  
 Comme mentionné précédemment, activez uniquement la diffusion en continu pour les messages volumineux (avec un contenu texte ou binaire) si les données ne peuvent pas être segmentées, si le message doit être remis en temps voulu ou si les données ne sont pas encore complètement disponibles au moment où le transfert est initialisé.  
  
### <a name="restrictions"></a>Restrictions  
 Vous ne pouvez pas utiliser un grand nombre de fonctionnalités [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] lorsque la diffusion en continu est activée :  
  
-   Les signatures numériques pour le corps du message ne peuvent pas être effectuées parce qu'elles requièrent un calcul de hachage sur le contenu entier du message. Avec la diffusion en continu, le contenu n'est pas complètement disponible lorsque les en-têtes de message sont construits et envoyés et, par conséquent, une signature numérique ne peut pas être calculée.  
  
-   Le chiffrement dépend des signatures numériques pour vérifier que les données ont été reconstruites correctement.  
  
-   Les sessions fiables doivent mettre en mémoire tampon les messages envoyés sur le client à des fins de nouvelle livraison si un message se perd lors du transfert et elles doivent conserver les messages sur le service avant de les rendre à l'implémentation du service afin de conserver leur ordre s'ils ne sont pas reçus dans l'ordre.  
  
 En raison de ces contraintes fonctionnelles, vous pouvez uniquement utiliser des options de sécurité au niveau du transport pour diffuser en continu et vous ne pouvez pas activer de sessions fiables. La diffusion en continu est uniquement disponible avec les liaisons définies par le système suivantes :  
  
-   <xref:System.ServiceModel.BasicHttpBinding>  
  
-   <xref:System.ServiceModel.NetTcpBinding>  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>  
  
-   <xref:System.ServiceModel.WebHttpBinding>  
  
 Parce que les transports sous-jacents de <xref:System.ServiceModel.NetTcpBinding> et <xref:System.ServiceModel.NetNamedPipeBinding> prennent en charge la remise fiable inhérente et les sessions basées sur la connexion, contrairement à HTTP, ces deux liaisons sont uniquement affectées de manière minime par ces contraintes, dans la pratique.  
  
 La diffusion en continu n'est pas disponible avec le transport MSMQ (Message Queuing) et ne peut donc pas être utilisée avec <xref:System.ServiceModel.NetMsmqBinding> ou la classe <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>. Le transport Message Queuing prend uniquement en charge les transferts de données mises en mémoire tampon avec une taille contrainte, alors que tous les autres transports n'ont pas de limite de taille de message dans la grande majorité des scénarios.  
  
 La diffusion en continu n'est pas disponible non plus lors de l'utilisation du transport de canal homologue, elle n'est donc pas disponible avec <xref:System.ServiceModel.NetPeerTcpBinding>.  
  
#### <a name="streaming-and-sessions"></a>Sessions et diffusion en continu  
 Vous pouvez obtenir un comportement inattendu lors de la diffusion en continu des appels avec une liaison basée sur session. Tous les appels en streaming passent par un canal unique (le canal de datagramme) qui ne prend pas en charge les sessions même si la liaison utilisée est configurée pour utiliser des sessions. Si plusieurs clients effectuent des appels de diffusion en continu vers le même objet de service sur une liaison basée sur session, et si le mode d’accès concurrentiel de l’objet de service est configuré comme unique et son mode de contexte d’instance a la valeur PerSession, les appels généraux doivent traverser le canal de datagramme et un seul appel à la fois est traité. Un ou plusieurs clients peuvent ainsi être temporisés. Vous pouvez contourner ce problème en attribuant au mode de contexte d'instance de l'objet de service la valeur PerCall, ou au mode d'accès concurrentiel la valeur Multiple.  
  
> [!NOTE]
>  MaxConcurrentSessions n'a aucun effet dans ce cas parce qu'il n'y a qu'une seule « session » disponible.  
  
### <a name="enabling-streaming"></a>Activation de la diffusion en continu  
 Vous pouvez activer la diffusion en continu des manières suivantes :  
  
-   Envoyez et acceptez des demandes en mode de diffusion en continu, puis acceptez et renvoyez les réponses en mode mémoire tampon (<xref:System.ServiceModel.TransferMode.StreamedRequest>).  
  
-   Envoyez et acceptez des demandes en mode mémoire tampon, puis acceptez et renvoyez les réponses en mode de diffusion en continu (<xref:System.ServiceModel.TransferMode.StreamedResponse>).  
  
-   Envoyez et recevez des demandes et des réponses en mode de diffusion en continu dans les deux sens. (<xref:System.ServiceModel.TransferMode.Streamed>).  
  
 Vous pouvez désactiver la diffusion en continu en affectant au mode de transfert la valeur <xref:System.ServiceModel.TransferMode.Buffered>, ce qui correspond au paramètre par défaut sur toutes les liaisons. Le code suivant montre comment définir le mode de transfert dans la configuration.  
  
```xml  
<system.serviceModel>  
     …  
    <bindings>  
      <basicHttpBinding>  
        <binding name="ExampleBinding" transferMode="Streaming"/>  
      </basicHttpBinding>  
    </bindings>  
     …  
<system.serviceModel>  
```  
  
 Lorsque vous instanciez votre liaison dans le code, vous devez affecter à la propriété `TransferMode` respective de la liaison (ou à l'élément de la liaison de transport si vous composez une liaison personnalisée) l'une des valeurs mentionnées précédemment.  
  
 Vous pouvez activer la diffusion en continu pour les demandes et les réponses ou pour les deux sens de manière indépendante à l'un ou l'autre côté des parties communicantes sans affecter les fonctionnalités. Toutefois, vous devez toujours partir du principe que la taille des données transférées est si importante que l'activation de la diffusion en continu est justifiée sur les deux points de terminaison d'une liaison de communication. Pour la communication multiplateforme où l'un des points de terminaison n'est pas implémenté avec [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], la capacité d'utiliser la diffusion en continu dépend des fonctionnalités de diffusion en continu de la plateforme. Une autre exception rare peut impliquer un scénario piloté par la consommation de mémoire dans lequel un client ou service doit minimiser son jeu de travail et peut uniquement accepter de petites tailles de mémoire tampon.  
  
### <a name="enabling-asynchronous-streaming"></a>Activation de la diffusion en continu asynchrone  
 Pour activer la diffusion en continu asynchrone, ajoutez le comportement de point de terminaison <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> à l'hôte de service et affectez à sa propriété <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> la valeur `true`. Nous avons également ajouté la fonction de diffusion en continu asynchrone du côté expéditeur. Cela améliore l'extensibilité du service dans les scénarios où des messages sont diffusés en continu à plusieurs clients, dont certains sont lents dans la lecture ; probablement en raison de la congestion du réseau ou ne lisent pas du tout. Dans ces scénarios, nous ne bloquons plus les différents threads sur le service par client. Cela garantit que le service peut gérer beaucoup plus de clients fournissant ainsi l'extensibilité du service.  
  
### <a name="programming-model-for-streamed-transfers"></a>Modèle de programmation pour les transferts en continu  
 Le modèle de programmation pour la diffusion en continu est simple. Pour recevoir des données en continu, spécifiez un contrat d'opération qui possède un seul paramètre d'entrée <xref:System.IO.Stream> saisi. Pour renvoyer des données en continu, renvoyez une référence <xref:System.IO.Stream>.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IStreamedService  
{  
    [OperationContract]  
    Stream Echo(Stream data);  
    [OperationContract]  
    Stream RequestInfo(string query);  
    [OperationContract(OneWay=true)]  
    void ProvideInfo(Stream data);  
}  
```  
  
 L'opération `Echo` dans l'exemple précédent reçoit et renvoie un flux et doit donc être utilisée sur une liaison avec <xref:System.ServiceModel.TransferMode.Streamed>. Pour l'opération `RequestInfo`, <xref:System.ServiceModel.TransferMode.StreamedResponse> convient mieux, car seul un <xref:System.IO.Stream> est renvoyé. L'opération unidirectionnelle convient mieux à <xref:System.ServiceModel.TransferMode.StreamedRequest>.  
  
 Notez que l'ajout d'un deuxième paramètre à `Echo` ou aux opérations `ProvideInfo` suivantes engendre le retour du modèle de service à une stratégie de mise en mémoire tampon et l'utilisation de la représentation de sérialisation à l'exécution du flux. Seules les opérations avec un paramètre de flux d'entrée unique sont compatibles avec la diffusion en continu des demandes de bout en bout.  
  
 Cette règle s'applique de la même façon aux contrats de message. Comme indiqué dans le contrat de message suivant, votre contrat de message peut uniquement comporter un seul membre de corps qui est un flux. Si vous souhaitez communiquer des informations supplémentaires avec le flux, ces informations doivent être transmises dans des en-têtes de message. Le corps du message est exclusivement réservé au contenu de flux.  
  
```  
[MessageContract]  
public class UploadStreamMessage  
{  
   [MessageHeader]  
   public string appRef;  
   [MessageBodyMember]  
   public Stream data;  
}   
```  
  
 Les transferts en continu se terminent et le message est fermé lorsque le flux atteint la fin du fichier (EOF). Lors de l'envoi d'un message (retour d'une valeur ou appel d'une opération), vous pouvez passer un <xref:System.IO.FileStream> et l'infrastructure [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] extrait ensuite toutes les données de ce flux jusqu'à ce que le flux ait complètement été lu et qu'il ait atteint EOF. Pour transférer des données en continu pour la source pour laquelle aucune classe dérivée <xref:System.IO.Stream> pré-intégrée n'existe, construisez une telle classe, superposez-la sur votre source de flux et utilisez-la en tant qu'argument ou valeur de retour.  
  
 Lors de la réception d'un message, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] construit un flux sur le contenu du corps du message encodé en Base64 (ou la partie MIME respective en cas d'utilisation de MTOM) et le flux atteint EOF lorsque le contenu a été lu.  
  
 La diffusion en continu au niveau du transport fonctionne également avec tout autre type de contrat de message (listes de paramètres, arguments de contrat de données et contrat de message explicite), mais étant donné que la sérialisation et la désérialisation de tels messages requièrent une mise en mémoire tampon par le sérialiseur, l'utilisation de telles variantes de contrat n'est pas recommandée.  
  
### <a name="special-security-considerations-for-large-data"></a>Considérations spéciales en matière de sécurité pour les données volumineuses  
 Toutes les liaisons vous permettent de contraindre la taille des messages entrants afin d’empêcher des attaques par déni de service. Le <xref:System.ServiceModel.BasicHttpBinding>, par exemple, expose un [System.ServiceModel.BasicHttpBinding.MaxReceivedMessageSize](xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A) propriété limitant la taille du message entrant et donc également délimite la quantité maximale de mémoire qui est accessible lors du traitement du message. Cette unité est définie en octets et s'élève par défaut à 65 536 octets.  
  
 Une menace pour la sécurité, spécifique à la diffusion en continu de données volumineuses, engendre un déni de service en provoquant la mise en mémoire tampon des données lorsque le destinataire s'attend à ce qu'elles soient diffusées en continu. Par exemple, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] met toujours en mémoire tampon les en-têtes SOAP d'un message, et par conséquent, un intrus peut construire un message malveillant volumineux qui se compose entièrement d'en-têtes afin de forcer les données à être mises en mémoire tampon. Lorsque la diffusion en continu est activée, `MaxReceivedMessageSize` peut avoir une valeur extrêmement élevée, parce que le destinataire ne s'attend jamais à ce que le message entier soit mis en mémoire tampon en une seule fois. Si [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] est forcé à mettre le message en mémoire tampon, un dépassement de capacité de mémoire se produit.  
  
 Par conséquent, la restriction de la taille maximale des messages entrants n'est pas suffisante dans ce cas. La propriété `MaxBufferSize` est requise pour contraindre la mémoire que [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] met en tampon. Il est important d'affecter à cette propriété une valeur sûre (ou de conserver sa valeur par défaut) lors de la diffusion en continu. Par exemple, supposez que votre service doive recevoir des fichiers d'une taille allant jusqu'à 4 Go afin de les stocker sur le disque local. Supposez également que votre mémoire soit contrainte de sorte à ce que vous puissiez uniquement mettre en mémoire tampon 64 Ko de données à la fois. Vous devez alors affecter la valeur 4 Go à `MaxReceivedMessageSize` et la valeur 64 Ko à `MaxBufferSize`. En outre, dans votre implémentation de service, vous devez veiller à lire uniquement à partir du flux entrant par segment de 64 Ko et à ne pas lire le segment suivant avant que le précédent ne soit écrit sur le disque et qu'il soit effacé de la mémoire.  
  
 Il est également important de comprendre que ce quota limite uniquement la mise en mémoire tampon effectuée par [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] et qu'il ne vous protège pas contre toute mise en mémoire tampon que vous effectuez dans votre propre service ou implémentation cliente. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Considérations de sécurité supplémentaires, consultez [considérations de sécurité pour les données](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).  
  
> [!NOTE]
>  La décision d'utiliser des transferts mis en mémoire tampon ou diffusés en continu est une décision locale du point de terminaison. Pour les transports HTTP, le mode de transfert ne se propage pas sur une connexion ou sur des serveurs proxy et d'autres intermédiaires. La description de l'interface de service ne reflète pas le mode de transfert défini. Après avoir généré un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sur un service, vous devez modifier le fichier de configuration des services destinés à être utilisés avec des transferts en continu pour définir le mode. Pour les transports TCP et les transports de canal nommé, le mode de transfert est propagé sous forme d'assertion de stratégie.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide pratique pour activer le streaming](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md)
