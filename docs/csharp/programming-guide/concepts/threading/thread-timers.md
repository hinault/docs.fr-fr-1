---
title: Minuteurs de thread (C#)
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: 52ed71e8-4fd9-43a4-ae40-04cce7cff23f
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9702360408340b28fcdcc8f197467a002f77ee51
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="thread-timers-c"></a>Minuteurs de thread (C#)
La classe <xref:System.Threading.Timer?displayProperty=nameWithType> est utile pour exécuter périodiquement une tâche sur un thread séparé. Par exemple, vous pouvez utiliser un minuteur de thread pour vérifier l’état et l’intégrité d’une base de données ou pour sauvegarder des fichiers essentiels.  
  
## <a name="thread-timer-example"></a>Exemple de minuteur de thread  
 L’exemple suivant démarre une tâche toutes les deux secondes et utilise un indicateur pour lancer la méthode <xref:System.IDisposable.Dispose%2A> qui arrête le minuteur. Cet exemple publie l’état dans la fenêtre de sortie.  
  
```csharp  
private class StateObjClass  
{  
    // Used to hold parameters for calls to TimerTask.  
    public int SomeValue;  
    public System.Threading.Timer TimerReference;  
    public bool TimerCanceled;  
}  
  
public void RunTimer()  
{  
    StateObjClass StateObj = new StateObjClass();  
    StateObj.TimerCanceled = false;  
    StateObj.SomeValue = 1;  
    System.Threading.TimerCallback TimerDelegate =  
        new System.Threading.TimerCallback(TimerTask);  
  
    // Create a timer that calls a procedure every 2 seconds.  
    // Note: There is no Start method; the timer starts running as soon as   
    // the instance is created.  
    System.Threading.Timer TimerItem =  
        new System.Threading.Timer(TimerDelegate, StateObj, 2000, 2000);  
  
    // Save a reference for Dispose.  
    StateObj.TimerReference = TimerItem;    
  
    // Run for ten loops.  
    while (StateObj.SomeValue < 10)   
    {  
        // Wait one second.  
        System.Threading.Thread.Sleep(1000);    
    }  
  
    // Request Dispose of the timer object.  
    StateObj.TimerCanceled = true;    
}  
  
private void TimerTask(object StateObj)  
{  
    StateObjClass State = (StateObjClass)StateObj;  
    // Use the interlocked class to increment the counter variable.  
    System.Threading.Interlocked.Increment(ref State.SomeValue);  
    System.Diagnostics.Debug.WriteLine("Launched new thread  " + DateTime.Now.ToString());  
    if (State.TimerCanceled)      
    // Dispose Requested.  
    {  
        State.TimerReference.Dispose();  
        System.Diagnostics.Debug.WriteLine("Done  " + DateTime.Now.ToString());  
    }  
}  
```  
  
 Les minuteurs de thread sont particulièrement utiles quand l’objet <xref:System.Windows.Forms.Timer?displayProperty=nameWithType> n’est pas disponible, par exemple quand vous développez des applications console.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Threading>  
 [Applications multithread (C#)](../../../../csharp/programming-guide/concepts/threading/multithreaded-applications.md)
