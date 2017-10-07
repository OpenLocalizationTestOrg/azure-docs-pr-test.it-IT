---
title: aaaScenario - App per la logica Trigger con le funzioni di Azure e Azure Service Bus | Documenti Microsoft
description: Creare un'app di logica di tootrigger una funzione tramite le funzioni di Azure e Azure Service Bus
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Scenario: Attivare app per la logica con Funzioni di Azure e il bus di servizio di Azure

Quando è necessario toodeploy un listener con esecuzione prolungata o attività, è possibile utilizzare funzioni di Azure toocreate un trigger per un'app di logica. Ad esempio, è possibile creare una funzione che sia in ascolto su una coda e attivi immediatamente un'app per la logica come trigger di push.

## <a name="build-hello-logic-app"></a>Compilare hello logica app
In questo esempio si dispone di una funzione in esecuzione per ogni app per la logica che deve toobe attivato. Per prima cosa, creare un'app per la logica con un trigger di richiesta HTTP. funzione Hello tale endpoint viene chiamato ogni volta che viene ricevuto un messaggio nella coda.  

1. Creare un'app per la logica.
2. Seleziona hello **manuale - quando viene ricevuta una richiesta HTTP** trigger.
   Facoltativamente, è possibile specificare un toouse schema JSON con un messaggio di coda hello utilizzando uno strumento come [jsonschema.net](http://jsonschema.net). Incollare schema hello trigger hello. Gli schemi per comprendere la progettazione hello forma hello delle proprietà di dati e il flusso hello più facilmente tramite flusso di lavoro di hello.
2. Aggiungere eventuali passaggi aggiuntivi che si desidera toooccur dopo aver ricevuto un messaggio nella coda. Ad esempio, inviare un messaggio di posta elettronica tramite Office 365.  
3. Salvare hello logica toogenerate hello callback URL dell'app per app per la logica toothis hello trigger. URL di Hello viene visualizzato nella scheda trigger hello.

![callback Hello URL viene visualizzato nella scheda trigger hello][1]

## <a name="build-hello-function"></a>Compilare la funzione hello
Successivamente, è necessario creare una funzione che funge da trigger hello e in ascolto sulla coda toohello.

1. In hello [portale di Azure funzioni](https://functions.azure.com/signin)selezionare **nuova funzione**, quindi selezionare hello **ServiceBusQueueTrigger - c#** modello.
   
    ![portale di Funzioni di Azure][2]
2. Configurare hello connessione toohello coda di Service Bus, che usa hello Azure Service Bus SDK `OnMessageReceive()` listener.
3. Scrivere un funzione di base toocall hello logica app dell'endpoint (creato in precedenza) utilizzando il messaggio di coda hello come trigger. Quello che segue è l'esempio completo di una funzione. esempio Hello viene utilizzato un `application/json` tipo di contenuto di messaggio, ma è possibile modificare questo tipo in base alle esigenze.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, aggiungere un messaggio nella coda tramite uno strumento quale [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer). Vedere hello logica app attivati immediatamente dopo la funzione hello riceve il messaggio hello.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
