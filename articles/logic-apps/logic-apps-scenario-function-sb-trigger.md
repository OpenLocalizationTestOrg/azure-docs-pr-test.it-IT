---
title: Scenario - Attivare app per la logica con Funzioni di Azure e il bus di servizio di Azure | Documentazione Microsoft
description: Creare una funzione per attivare un'app per la logica usando Funzioni di Azure e il bus di servizio di Azure
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="a6402-103">Scenario: Attivare app per la logica con Funzioni di Azure e il bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="a6402-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="a6402-104">È possibile utilizzare Funzioni di Azure per creare un trigger per un'app per la logica quando è necessario distribuire un listener o un'attività con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="a6402-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="a6402-105">Ad esempio, è possibile creare una funzione che sia in ascolto su una coda e attivi immediatamente un'app per la logica come trigger di push.</span><span class="sxs-lookup"><span data-stu-id="a6402-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="a6402-106">Compilare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="a6402-106">Build the logic app</span></span>
<span data-ttu-id="a6402-107">In questo esempio si ha una funzione in esecuzione per ogni app per la logica da attivare.</span><span class="sxs-lookup"><span data-stu-id="a6402-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="a6402-108">Per prima cosa, creare un'app per la logica con un trigger di richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6402-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="a6402-109">La funzione chiamerà tale endpoint ogniqualvolta venga ricevuto un messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="a6402-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="a6402-110">Creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a6402-110">Create a logic app.</span></span>
2. <span data-ttu-id="a6402-111">Selezionare il trigger **Manual - When an HTTP request is received** (Manuale - Quando si riceve una richiesta HTTP).</span><span class="sxs-lookup"><span data-stu-id="a6402-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="a6402-112">Facoltativamente, è possibile specificare uno schema JSON da utilizzare con il messaggio della coda utilizzando uno strumento come [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="a6402-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="a6402-113">Incollare lo schema nel trigger.</span><span class="sxs-lookup"><span data-stu-id="a6402-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="a6402-114">Grazie agli schemi, la finestra di progettazione potrà riconoscere la forma dei dati e trasferire più facilmente le proprietà nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a6402-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="a6402-115">Aggiungere eventuali ulteriori passaggi che si desidera vengano eseguiti dopo la ricezione di un messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="a6402-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="a6402-116">Ad esempio, inviare un messaggio di posta elettronica tramite Office 365.</span><span class="sxs-lookup"><span data-stu-id="a6402-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="a6402-117">Salvare l'app per la logica per generare l'URL di callback per il trigger di questa app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a6402-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="a6402-118">L'URL è visualizzato nella scheda del trigger.</span><span class="sxs-lookup"><span data-stu-id="a6402-118">The URL appears on the trigger card.</span></span>

![L'URL callback è visualizzato nella scheda del trigger][1]

## <a name="build-the-function"></a><span data-ttu-id="a6402-120">Compilare la funzione</span><span class="sxs-lookup"><span data-stu-id="a6402-120">Build the function</span></span>
<span data-ttu-id="a6402-121">A questo punto è necessario creare una funzione che fungerà da trigger e sarà in ascolto sulla coda.</span><span class="sxs-lookup"><span data-stu-id="a6402-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="a6402-122">Nel [portale di Funzioni di Azure](https://functions.azure.com/signin) selezionare **Nuova funzione** e quindi il modello **ServiceBusQueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="a6402-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portale di Funzioni di Azure][2]
2. <span data-ttu-id="a6402-124">Configurare la connessione alla coda del bus di servizio, che userà il listener `OnMessageReceive()` dell'SDK del bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6402-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="a6402-125">Scrivere una semplice funzione per chiamare l'endpoint dell'app per la logica usando il messaggio nella coda come trigger.</span><span class="sxs-lookup"><span data-stu-id="a6402-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="a6402-126">Quello che segue è l'esempio completo di una funzione.</span><span class="sxs-lookup"><span data-stu-id="a6402-126">Here's a full example of a function.</span></span> <span data-ttu-id="a6402-127">Nell'esempio viene usato il tipo di contenuto di messaggio `application/json`, ma è possibile modificare questo elemento se necessario.</span><span class="sxs-lookup"><span data-stu-id="a6402-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="a6402-128">Per effettuare una prova, aggiungere un messaggio in coda tramite uno strumento quale [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="a6402-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="a6402-129">L'app per la logica verrà attivata subito dopo che la funzione riceverà il messaggio.</span><span class="sxs-lookup"><span data-stu-id="a6402-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
