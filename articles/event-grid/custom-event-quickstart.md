---
title: Eventi personalizzati per la griglia di eventi di Azure | Microsoft Docs
description: Usare la griglia di eventi di Azure per pubblicare un argomento e sottoscrivere l'evento.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="aabf9-103">Creare e instradare eventi personalizzati con la griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="aabf9-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="aabf9-104">La griglia di eventi di Azure è un servizio di gestione degli eventi per il cloud.</span><span class="sxs-lookup"><span data-stu-id="aabf9-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="aabf9-105">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure per creare un argomento personalizzato, sottoscrivere l'argomento e attivare l'evento per visualizzare il risultato.</span><span class="sxs-lookup"><span data-stu-id="aabf9-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="aabf9-106">In genere, si inviano eventi a un endpoint che risponde all'evento, ad esempio un webhook o una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="aabf9-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="aabf9-107">Per maggiore semplicità, tuttavia, in questo articolo gli eventi vengono inviati a un URL che si limita a raccoglie i messaggi.</span><span class="sxs-lookup"><span data-stu-id="aabf9-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="aabf9-108">L'URL viene creato con [RequestBin](https://requestb.in/), uno strumento open source di terze parti.</span><span class="sxs-lookup"><span data-stu-id="aabf9-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="aabf9-109">**RequestBin** è uno strumento open source non destinato all'utilizzo a velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="aabf9-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="aabf9-110">L'uso dello strumento in questo esempio è esclusivamente dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="aabf9-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="aabf9-111">Se si esegue il push di più di un evento alla volta, è possibile che non vengano visualizzati tutti gli eventi nello strumento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="aabf9-112">Al termine, i dati dell'evento vengono inviati a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="aabf9-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Dati dell'evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aabf9-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo articolo è necessario eseguire la versione più recente dell'interfaccia della riga di comando di Azure (2.0.14 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="aabf9-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="aabf9-115">Per trovare la versione, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="aabf9-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="aabf9-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aabf9-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="aabf9-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="aabf9-117">Create a resource group</span></span>

<span data-ttu-id="aabf9-118">Gli argomenti della griglia di eventi sono risorse di Azure e devono essere inseriti in un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="aabf9-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="aabf9-119">Un gruppo di risorse è una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="aabf9-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="aabf9-120">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="aabf9-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="aabf9-121">L'esempio seguente crea un gruppo di risorse denominato *gridResourceGroup* nella località *westus2*.</span><span class="sxs-lookup"><span data-stu-id="aabf9-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="aabf9-122">Creare un argomento personalizzato</span><span class="sxs-lookup"><span data-stu-id="aabf9-122">Create a custom topic</span></span>

<span data-ttu-id="aabf9-123">Un argomento fornisce un endpoint definito dall'utente in cui vengono pubblicati gli eventi.</span><span class="sxs-lookup"><span data-stu-id="aabf9-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="aabf9-124">L'esempio seguente crea l'argomento nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aabf9-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="aabf9-125">Sostituire `<topic_name>` con un nome univoco per l'argomento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="aabf9-126">Il nome dell'argomento deve essere univoco perché è rappresentato da una voce DNS.</span><span class="sxs-lookup"><span data-stu-id="aabf9-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="aabf9-127">Per la versione di anteprima, la griglia di eventi supporta le località **westus2** e **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="aabf9-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="aabf9-128">Creare un endpoint del messaggio</span><span class="sxs-lookup"><span data-stu-id="aabf9-128">Create a message endpoint</span></span>

<span data-ttu-id="aabf9-129">Prima di sottoscrivere l'argomento, creare l'endpoint per il messaggio dell'evento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="aabf9-130">Anziché scrivere codice per rispondere all'evento, creare un endpoint che raccoglie i messaggi per poterli visualizzare.</span><span class="sxs-lookup"><span data-stu-id="aabf9-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="aabf9-131">RequestBin è uno strumento open source di terze parti che consente di creare un endpoint e visualizza le richieste che gli vengono inviate.</span><span class="sxs-lookup"><span data-stu-id="aabf9-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="aabf9-132">Passare a [RequestBin](https://requestb.in/) e fare clic su **Create a RequestBin** (Crea un RequestBin).</span><span class="sxs-lookup"><span data-stu-id="aabf9-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="aabf9-133">Copiare l'URL del contenitore, necessario per sottoscrivere l'argomento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="aabf9-134">Sottoscrivere un argomento</span><span class="sxs-lookup"><span data-stu-id="aabf9-134">Subscribe to a topic</span></span>

<span data-ttu-id="aabf9-135">Si sottoscrive un argomento per indicare alla griglia di eventi gli eventi di cui si vuole tenere traccia. L'esempio seguente sottoscrive l'argomento creato e passa l'URL da RequestBin come endpoint per la notifica dell'evento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="aabf9-136">Sostituire `<event_subscription_name>` con un nome univoco per la sottoscrizione e `<URL_from_RequestBin>` con il valore preso dalla sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="aabf9-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="aabf9-137">Se durante la sottoscrizione si specifica un endpoint, la griglia di eventi gestisce il routing degli eventi verso tale endpoint.</span><span class="sxs-lookup"><span data-stu-id="aabf9-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="aabf9-138">Per `<topic_name>`, usare il valore creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="aabf9-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="aabf9-139">Inviare un evento all'argomento</span><span class="sxs-lookup"><span data-stu-id="aabf9-139">Send an event to your topic</span></span>

<span data-ttu-id="aabf9-140">A questo punto, attivare un evento per vedere come la griglia di eventi distribuisce il messaggio nell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="aabf9-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="aabf9-141">Ottenere prima di tutto l'URL e la chiave per l'argomento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="aabf9-142">Usare ancora una volta il nome dell'argomento per `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="aabf9-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="aabf9-143">Per semplificare questo articolo, sono stati configurati dati di esempio dell'evento da inviare all'argomento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="aabf9-144">In genere, i dati dell'evento vengono inviati da un'applicazione o un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="aabf9-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="aabf9-145">L'esempio seguente ottiene i dati dell'evento:</span><span class="sxs-lookup"><span data-stu-id="aabf9-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="aabf9-146">Eseguendo `echo "$body"` è possibile visualizzare l'evento completo.</span><span class="sxs-lookup"><span data-stu-id="aabf9-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="aabf9-147">L'elemento `data` del JSON è il payload dell'evento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="aabf9-148">Questo campo accetta qualsiasi JSON ben formato.</span><span class="sxs-lookup"><span data-stu-id="aabf9-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="aabf9-149">È anche possibile usare il campo oggetto per il filtro e il routing avanzato.</span><span class="sxs-lookup"><span data-stu-id="aabf9-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="aabf9-150">CURL è una utilità che esegue richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="aabf9-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="aabf9-151">In questo articolo CURL viene usato per inviare l'evento all'argomento.</span><span class="sxs-lookup"><span data-stu-id="aabf9-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="aabf9-152">È stato attivato l'evento e la griglia di eventi ha inviato il messaggio all'endpoint configurato al momento della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="aabf9-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="aabf9-153">Passare all'URL di RequestBin creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="aabf9-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="aabf9-154">In alternativa, fare clic su Aggiorna nel browser di RequestBin aperto.</span><span class="sxs-lookup"><span data-stu-id="aabf9-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="aabf9-155">Verrà visualizzato l'evento appena inviato.</span><span class="sxs-lookup"><span data-stu-id="aabf9-155">You see the event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="aabf9-156">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="aabf9-156">Clean up resources</span></span>
<span data-ttu-id="aabf9-157">Se si intende continuare a usare questo evento, non è necessario pulire le risorse create con questo articolo.</span><span class="sxs-lookup"><span data-stu-id="aabf9-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="aabf9-158">Se non si intende continuare, usare il comando seguente per eliminare le risorse create con questo articolo.</span><span class="sxs-lookup"><span data-stu-id="aabf9-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="aabf9-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aabf9-159">Next steps</span></span>

<span data-ttu-id="aabf9-160">Ora che si è appreso come creare argomenti e sottoscrizioni di eventi, è possibile approfondire le operazioni possibili con la griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="aabf9-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="aabf9-161">Informazioni sulla griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="aabf9-161">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="aabf9-162">Monitorare le modifiche alla macchina virtuale con la griglia di eventi di Azure e le app per la logica</span><span class="sxs-lookup"><span data-stu-id="aabf9-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
