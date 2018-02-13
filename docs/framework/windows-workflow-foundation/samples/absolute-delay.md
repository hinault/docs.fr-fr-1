---
title: Report absolu
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b483139a-39bb-4560-8003-8969a8fc2cd1
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 60e3b65851dba68b4d01d6e4195b5faf99b583de
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="absolute-delay"></a>Report absolu
Le principal scénario de cet exemple consiste à définir un report jusqu'à un <xref:System.DateTime> spécifié, à l'aide de minuteurs durables dans une application de workflow. Cette opération n'est pas comparable à l'utilisation de l'activité <xref:System.Activities.Statements.Delay> intégrée, dans la mesure où elle vous permet seulement de définir un report pour un <xref:System.TimeSpan> donné (ou nombre de minutes/secondes).  
  
 Voici quelques scénarios tirés de la vie réelle pour lesquels cette distinction peut être importante :  
  
1.  Vous souhaitez différer l'envoi d'un message électronique de 30 secondes afin de vous assurer que vous n'avez fait aucune erreur.  
  
2.  Vous faites des heures supplémentaires et souhaitez différer l'envoi de l'ensemble de vos messages électroniques en attendant les heures de bureau normales (8 heures du matin, par exemple).  
  
## <a name="demonstrates"></a>Démonstrations  
  
1.  <xref:System.Activities.Statements.DurableTimerExtension> pour implémenter un report absolu  
  
2.  Configuration de la persistance à l'aide de <xref:System.Activities.WorkflowApplication> pour les minuteurs durables  
  
3.  Utilisation de <xref:System.Activities.NativeActivity%601> pour le recours à des points d'extensibilité  
  
4.  Utilisation de <xref:System.Activities.CodeActivity%601> dans l'activité SendEmail  
  
5.  <xref:System.Activities.Statements.Delay>  
  
6.  Flux de travail XAML uniquement  
  
 Cet exemple montre comment créer une activité personnalisée qui a lieu à un <xref:System.DateTime> défini et utilise des minuteurs durables pour enregistrer la durée du report. Lors de l'utilisation de minuteurs durables, vous devez utiliser un <xref:System.Activities.NativeActivity> afin de créer un signet, car vous devrez enregistrer ce signet avec l'extension de minuterie. Dans cet exemple, lorsque le minuteur durable arrive à expiration, un appel à la méthode `OnTimerExpired` a lieu. Assurez-vous que vous ajoutez l'extension de minuterie dans l'événement <xref:System.Activities.NativeActivity%601.CacheMetadata%2A> pour fournir le runtime avec ces informations. Le seul autre détail d'implémentation consiste à implémenter une logique afin de convertir <xref:System.DateTime> en <xref:System.TimeSpan>, du fait que les minuteurs durables n'acceptent qu'un <xref:System.DateTime>. Notez une petite dégradation de la précision à cette occasion  
  
> [!NOTE]
>  Une petite dégradation de la précision est constatée lors de la conversion de <xref:System.DateTime> en <xref:System.TimeSpan>.  
  
 Cet exemple montre également comment activer la persistance pour un <xref:System.Activities.WorkflowApplication>. Dans cet exemple particulier, nous allons utiliser des minuteurs durables dans lesquels les données du flux de travail sont déchargées dans la base de données de persistance au cours de la période d'inactivité en attente de l'expiration du minuteur. Cette implémentation peut également servir à d'autres actions de persistance. Cet exemple montre comment configurer la chaîne de connexion de persistance avec SQL Server, et comment créer le magasin d'instances afin de rendre les données persistantes pour les instances du flux de travail. Une logique est fournie sur la manière de reprendre le flux de travail une fois qu'un événement rendant l'instance du flux de travail exécutable est généré.  
  
 À mesure que vous parcourez cet exemple, vous verrez le temps dans laquelle le délai intégré commence et termine, qui à son tour entraîne un message électronique à envoyer. À partir de là, l'activité AbsoluteDelay s'arrête jusqu'à un <xref:System.DateTime> spécifié (ou 0 seconde si <xref:System.DateTime> est arrivé à expiration), suite à quoi un message électronique est envoyé à l'expiration. Cet exemple montre les deux cas d'utilisation différents de la fonctionnalité <xref:System.Activities.Statements.Delay> intégrée par rapport à l'utilisation d'une activité AbsoluteDelay.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez-vous que SQL Server Express (ou version ultérieure) est installé sur votre ordinateur.  
  
2.  Exécutez setup.cmd (à partir de WF/Basic/Services/AbsoluteDelay/CS) dans une invite de commandes [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] afin de créer la base de données AbsoluteDelaySampleDB, le schéma de persistance et la logique de persistance.  
  
3.  Ouvrez la solution dans [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
4.  Spécifiez la durée de l'activité de report.  
  
5.  Spécifiez l'heure d'expiration dans l'activité AbsoluteDelay.  
  
6.  Mettez à jour les champs SendMailTo, SendMailFrom, SendMailSubject, SendMailBody et SmtpHost dans l'activité SendMail.  
  
    > [!NOTE]
    >  Si vous n'entrez pas d'hôte SMTP valide, l'application lèvera une exception SMTP.  
  
7.  Générez la solution en sélectionnant **générer**, **générer la Solution**.  
  
8.  Exécutez la solution en appuyant sur **F5**.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\AbsoluteDelay`
