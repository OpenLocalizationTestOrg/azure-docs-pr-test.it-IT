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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="f1916-103">Scenario: Attivare app per la logica con Funzioni di Azure e il bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="f1916-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="f1916-104">Quando è necessario toodeploy un listener con esecuzione prolungata o attività, è possibile utilizzare funzioni di Azure toocreate un trigger per un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="f1916-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="f1916-105">Ad esempio, è possibile creare una funzione che sia in ascolto su una coda e attivi immediatamente un'app per la logica come trigger di push.</span><span class="sxs-lookup"><span data-stu-id="f1916-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="f1916-106">Compilare hello logica app</span><span class="sxs-lookup"><span data-stu-id="f1916-106">Build hello logic app</span></span>
<span data-ttu-id="f1916-107">In questo esempio si dispone di una funzione in esecuzione per ogni app per la logica che deve toobe attivato.</span><span class="sxs-lookup"><span data-stu-id="f1916-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="f1916-108">Per prima cosa, creare un'app per la logica con un trigger di richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1916-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="f1916-109">funzione Hello tale endpoint viene chiamato ogni volta che viene ricevuto un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f1916-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="f1916-110">Creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f1916-110">Create a logic app.</span></span>
2. <span data-ttu-id="f1916-111">Seleziona hello **manuale - quando viene ricevuta una richiesta HTTP** trigger.</span><span class="sxs-lookup"><span data-stu-id="f1916-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="f1916-112">Facoltativamente, è possibile specificare un toouse schema JSON con un messaggio di coda hello utilizzando uno strumento come [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="f1916-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="f1916-113">Incollare schema hello trigger hello.</span><span class="sxs-lookup"><span data-stu-id="f1916-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="f1916-114">Gli schemi per comprendere la progettazione hello forma hello delle proprietà di dati e il flusso hello più facilmente tramite flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="f1916-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="f1916-115">Aggiungere eventuali passaggi aggiuntivi che si desidera toooccur dopo aver ricevuto un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f1916-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="f1916-116">Ad esempio, inviare un messaggio di posta elettronica tramite Office 365.</span><span class="sxs-lookup"><span data-stu-id="f1916-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="f1916-117">Salvare hello logica toogenerate hello callback URL dell'app per app per la logica toothis hello trigger.</span><span class="sxs-lookup"><span data-stu-id="f1916-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="f1916-118">URL di Hello viene visualizzato nella scheda trigger hello.</span><span class="sxs-lookup"><span data-stu-id="f1916-118">hello URL appears on hello trigger card.</span></span>

![callback Hello URL viene visualizzato nella scheda trigger hello][1]

## <a name="build-hello-function"></a><span data-ttu-id="f1916-120">Compilare la funzione hello</span><span class="sxs-lookup"><span data-stu-id="f1916-120">Build hello function</span></span>
<span data-ttu-id="f1916-121">Successivamente, è necessario creare una funzione che funge da trigger hello e in ascolto sulla coda toohello.</span><span class="sxs-lookup"><span data-stu-id="f1916-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="f1916-122">In hello [portale di Azure funzioni](https://functions.azure.com/signin)selezionare **nuova funzione**, quindi selezionare hello **ServiceBusQueueTrigger - c#** modello.</span><span class="sxs-lookup"><span data-stu-id="f1916-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portale di Funzioni di Azure][2]
2. <span data-ttu-id="f1916-124">Configurare hello connessione toohello coda di Service Bus, che usa hello Azure Service Bus SDK `OnMessageReceive()` listener.</span><span class="sxs-lookup"><span data-stu-id="f1916-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="f1916-125">Scrivere un funzione di base toocall hello logica app dell'endpoint (creato in precedenza) utilizzando il messaggio di coda hello come trigger.</span><span class="sxs-lookup"><span data-stu-id="f1916-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="f1916-126">Quello che segue è l'esempio completo di una funzione.</span><span class="sxs-lookup"><span data-stu-id="f1916-126">Here's a full example of a function.</span></span> <span data-ttu-id="f1916-127">esempio Hello viene utilizzato un `application/json` tipo di contenuto di messaggio, ma è possibile modificare questo tipo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f1916-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="f1916-128">tootest, aggiungere un messaggio nella coda tramite uno strumento quale [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="f1916-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="f1916-129">Vedere hello logica app attivati immediatamente dopo la funzione hello riceve il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="f1916-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
