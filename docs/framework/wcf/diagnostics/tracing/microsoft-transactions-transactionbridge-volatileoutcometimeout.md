---
title: Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2dbe34c5-57c7-4b64-9257-63021911d03c
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1385995165308cb1c2f2e6bd6c8a800a88b7b79e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="microsofttransactionstransactionbridgevolatileoutcometimeout"></a>Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
Le service du protocole WS-AT a dépassé le délai spécifié lors de l'attente d'une réponse à un message de résultat provenant d'un participant volatil. Le résultat de la transaction peut s’avérer incertain si le participant retourne.  
  
## <a name="description"></a>Description  
 Suivi lorsqu'un participant volatil a décidé de valider ou d'abandonner mais n'a pas répondu à une demande de validation ou de restauration dans un délai donné.  
  
## <a name="troubleshooting"></a>Résolution des problèmes  
 Assurez-vous que tous les participants volatils sont en mesure de répondre dans le délai imparti. Le délai par défaut est de 180 secondes.  S'il est insuffisant, augmentez le délai du minuteur `VolatileOutcomeDelay` de WS-AT.  
  
## <a name="see-also"></a>Voir aussi  
 [Suivi](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [Utilisation du suivi pour résoudre les problèmes posés par votre application](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)  
 [Administration et diagnostics](../../../../../docs/framework/wcf/diagnostics/index.md)
