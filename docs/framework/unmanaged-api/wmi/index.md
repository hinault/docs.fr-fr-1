---
title: "WMI et les compteurs de Performance (référence des API non managées)"
description: "Résume le .NET Framework API non managée pour des informations sur les compteurs de performance ou WMI."
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.date: 11/06/2017
ms.topic: reference
ms.prod: .net-framework
ms.devlang: cpp
ms.workload:
- dotnet
ms.openlocfilehash: c7959d6b6b7bafd728db5a579ff1376e686c5b74
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="windows-management-instrumentation-wmi-and-performance-counters-unmanaged-api-reference"></a>Windows Management Instrumentation (WMI) et les compteurs de Performance (référence des API non managées)

L’API non managée .NET Framework WMI et les compteurs de Performance se compose d’un ensemble de fonctions qui encapsulent les appels à la [natif Windows Management Instrumentation API](https://msdn.microsoft.com/library/aa389276(v=vs.85).aspx). Il vous permet de développer des outils et bibliothèques de gérer et surveiller des ordinateurs distants.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
L’API comprend les fonctions suivantes :

| Fonction | Description |
|---------|---------|
| [BeginEnumeration, fonction](beginenumeration.md) | Rétablit l’énumérateur au début d’une énumération de propriétés de l’objet WMI. |
| [BeginMethodEnumeration, fonction](beginmethodenumeration.md) |  Commence une énumération des méthodes disponibles pour un objet. |
| [BlessIWbemServices, fonction](blessiwbemservices.md) | Indique si les informations d’identification utilisateur autorisent l’accès à une classe IWbemServices spécifiée. |
| [BlessIWbemServicesObject, fonction](blessiwbemservicesobject.md) | Indique si les informations d’identification autorisent l’accès à un objet de service IWbem spécifié. |
| [Clone, fonction](clone.md) | Retourne un nouvel objet qui est un clone complet de l’objet actuel. |
| [CloneEnumWbemClassObject, fonction](cloneenumwbemclassobject.md) | Effectue une copie logique d’un énumérateur, en conservant sa position actuelle dans une énumération. |
| [CompareTo, fonction](compareto.md) | Compare un objet à un autre objet de gestion de Windows. |
| [ConnectServerWmi (fonction)](connectserverwmi.md) | Crée une connexion via DCOM à un espace de noms WMI sur un ordinateur spécifié. |
| [CreateClassEnumWmi (fonction)](createclassenumwmi.md) | Retourne un énumérateur pour toutes les classes qui répondent aux critères de sélection spécifiés. |
| [CreateInstanceEnumWmi (fonction)](createinstanceenumwmi.md) | Retourne un énumérateur qui retourne les instances d’une classe spécifiée qui répondent aux critères de sélection spécifiés. |
| [Delete, fonction](delete.md) | Supprime une propriété spécifiée à partir d’une définition de classe et tous ses qualificateurs. |
| [DeleteMethod, fonction](deletemethod.md) | Supprime une méthode spécifiée à partir d’une définition de classe CIM. |
| [EndEnumeration, fonction](endenumeration.md) | Met fin à une séquence d’énumération. | 
| [EndMethodEnumeration, fonction](endmethodenumeration.md) | Met fin à une séquence d’énumération lancée en appelant le [BeginMethodEnumeration fonction](beginmethodenumeration.md). |
| [ExecNotificationQueryWmi, fonction](execnotificationquerywmi.md) | Exécute une requête pour recevoir les événements. |
| [ExecQueryWmi, fonction](execquerywmi.md) | Exécute une requête pour récupérer des objets. |
| [FormatFromRawValue, fonction](formatfromrawvalue.md) | Convertit une valeur de données de performances brutes au format spécifié, ou les deux valeurs de données de performances brutes si la conversion de format est basé sur le temps. | 
| [Get, fonction](get.md) | Récupère une valeur de propriété spécifiée si elle existe. |
| [GetCurrentApartmentType (fonction)](getcurrentapartmenttype.md) | Récupère le type de cloisonnement dans lequel l’appelant s’exécute. |
| [GetDemultiplexedStub (fonction)](getdemultiplexedstub.md) | Crée un récepteur de redirecteur d’objet pour aider un client lors de la réception des appels asynchrones de la gestion de Windows. |
| [GetErrorInfo (fonction)](geterrorinfo.md) | Récupère les informations d’erreur à partir de l’appel de fonction précédente. | 
| [GetMethod, fonction](getmethod.md) | Récupère des informations sur la méthode spécifiée. | 
| [GetMethodOrigin, fonction](getmethodorigin.md) | Détermine la classe dans laquelle une méthode est déclarée. |
| [GetMethodQualifierSet, fonction](getmethodqualifierset.md) | Récupère le qualificateur défini pour une méthode particulière. |
| [GetNames, fonction](getnames.md) | Récupère un sous-ensemble ou tous les noms des propriétés d’un objet. |
| [GetObjectText, fonction](getobjecttext.md) | Retourne un rendu de texte d’un objet dans la syntaxe MOF. | 
| [GetPropertyHandle, fonction](getpropertyhandle.md) | Retourne un identificateur unique qui identifie une propriété. |
| [GetPropertyOrigin, fonction](getpropertyorigin.md) | Détermine la classe dans laquelle une propriété est déclarée. |
| [GetPropertyQualifierSet (fonction)](getpropertyqualifierset.md) | Récupère le qualificateur définie pour une propriété particulière.  |
| [GetQualifierSet (fonction)](getqualifierset.md) | Récupère le qualificateur définie pour une instance de classe ou une définition de classe. |
| [InheritsFrom (fonction)](inheritsfrom.md) | Détermine si l’instance ou la classe actuelle dérive d’une classe parente spécifiée. |
| [Initialiser (fonction)](initialize.md) | Effectue l’initialisation de WMI. |
| [Fonction Next](next.md) | Récupère la propriété suivante dans une énumération. | 
| [NextMethod (fonction)](nextmethod.md) | Récupère la méthode suivante dans une énumération. |
| [Fonction Put](put.md) | Définit une propriété nommée par une nouvelle valeur. |
| [PutClassWmi (fonction)](putclasswmi.md) | Crée une nouvelle classe, ou met à jour un existant. |
| [PutInstanceWmi (fonction)](putinstancewmi.md) | Crée ou met à jour une instance d’une classe existante. L’instance est écrit dans le référentiel WMI. |
| [PutMethod (fonction)](putmethod.md) | Crée une méthode. |
| [QualifierSet_BeginEnumeration (fonction)](qualifierset-beginenumeration.md) | Réinitialise l’énumérateur des qualificateurs d’un objet au début de l’énumération. |
| [QualifierSet_Delete (fonction)](qualifierset-delete.md) | Supprime un qualificateur spécifié par nom.  |
| [QualifierSet_EndEnumeration (fonction)](qualifierset-endenumeration.md) | Met fin à l’énumération commencée avec un appel à la `QualifierSet_BeginEnumeration` (fonction). |
| [QualifierSet_Get (fonction)](qualifierset-get.md) | Obtient le qualificateur nommé spécifié.  |
| [QualifierSet_GetNames (fonction)](qualifierset-getnames.md) | Récupère les noms de tous les qualificateurs ou des qualificateurs spécifiés qui sont disponibles à partir de l’objet en cours ou de la propriété. |
| [QualifierSet_Next (fonction)](qualifierset-next.md) | Récupère le qualificateur suivant dans une énumération démarrée avec un appel à la [QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) (fonction). |
| [QualifierSet_Put (fonction)](qualifierset-put.md) | Écrit la valeur et le qualificateur nommé. |
| [ResetSecurity (fonction)](resetsecurity.md) | Assigne le jeton d’emprunt d’identité fournie pour le thread actuel. |
| [SetSecurity (fonction)](setsecurity.md) | Récupère le jeton d’emprunt d’identité associé au thread actuel. |
| [SpawnDerivedClass (fonction)](spawnderivedclass.md) | Crée un objet de classe qui vient d’être dérivée d’un objet spécifié. | 
| [SpawnInstance (fonction)](spawninstance.md) | Crée une nouvelle instance d’une classe. |   
| [VerifyClient (fonction)](verifyclientkey.md) | Garantit que la clé du client dispose de la sécurité appropriée. |
| [WritePropertyValue (fonction)](writepropertyvalue.md) | Écrit un nombre spécifié d’octets à une propriété identifiée par un descripteur de propriété. |

 ## <a name="see-also"></a>Voir aussi
[Référence des API non managées](../index.md) 
