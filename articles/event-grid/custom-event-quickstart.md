---
title: gli eventi aaaCustom per griglia di eventi di Azure | Documenti Microsoft
description: Utilizzare toopublish griglia di eventi di Azure un argomento e sottoscrizione evento toothat.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="657c4-103">Creare e instradare eventi personalizzati con la griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="657c4-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="657c4-104">Azure griglia di eventi è un servizio di gestione degli eventi per il cloud hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="657c4-105">In questo articolo, utilizzare hello Azure CLI toocreate un argomento personalizzato, sottoscrizione toohello argomento e attivare i risultati di hello evento tooview hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="657c4-106">In genere, si inviano endpoint tooan gli eventi che risponde a eventi toohello, ad esempio, un webhook o una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="657c4-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="657c4-107">Tuttavia, toosimplify in questo articolo, si invia hello eventi tooa URL che raccoglie solo i messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="657c4-108">L'URL viene creato con [RequestBin](https://requestb.in/), uno strumento open source di terze parti.</span><span class="sxs-lookup"><span data-stu-id="657c4-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="657c4-109">**RequestBin** è uno strumento open source non destinato all'utilizzo a velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="657c4-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="657c4-110">uso di Hello dello strumento di hello qui è puramente dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="657c4-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="657c4-111">Se si esegue il push più di un evento alla volta, potrebbe non visualizza tutti gli eventi dello strumento hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="657c4-112">Al termine, vedrai che i dati dell'evento hello sono stati inviati tooan endpoint.</span><span class="sxs-lookup"><span data-stu-id="657c4-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Dati dell'evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="657c4-114">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo articolo richiede che si eseguono più recente di Azure CLI hello (2.0.14 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="657c4-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="657c4-115">versione di hello toofind, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="657c4-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="657c4-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="657c4-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="657c4-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="657c4-117">Create a resource group</span></span>

<span data-ttu-id="657c4-118">Gli argomenti della griglia di eventi sono risorse di Azure e devono essere inseriti in un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="657c4-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="657c4-119">gruppo di risorse Hello è una raccolta logica in cui Azure le risorse vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="657c4-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="657c4-120">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="657c4-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="657c4-121">esempio Hello crea un gruppo di risorse denominato *gridResourceGroup* in hello *westus2* percorso.</span><span class="sxs-lookup"><span data-stu-id="657c4-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="657c4-122">Creare un argomento personalizzato</span><span class="sxs-lookup"><span data-stu-id="657c4-122">Create a custom topic</span></span>

<span data-ttu-id="657c4-123">Un argomento fornisce un endpoint definito dall'utente in cui vengono pubblicati gli eventi.</span><span class="sxs-lookup"><span data-stu-id="657c4-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="657c4-124">Hello esempio seguente crea argomento hello nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="657c4-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="657c4-125">Sostituire `<topic_name>` con un nome univoco per l'argomento.</span><span class="sxs-lookup"><span data-stu-id="657c4-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="657c4-126">nome dell'argomento Hello deve essere univoco perché viene rappresentata da una voce DNS.</span><span class="sxs-lookup"><span data-stu-id="657c4-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="657c4-127">Per la versione di anteprima hello griglia eventi supporta **westus2** e **westcentralus** percorsi.</span><span class="sxs-lookup"><span data-stu-id="657c4-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="657c4-128">Creare un endpoint del messaggio</span><span class="sxs-lookup"><span data-stu-id="657c4-128">Create a message endpoint</span></span>

<span data-ttu-id="657c4-129">Prima di sottoscrizione toohello argomento, creare endpoint hello per il messaggio di evento hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="657c4-130">Anziché scrivere eventi toohello toorespond di codice, creare un endpoint che raccoglie i messaggi hello, pertanto è possibile visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="657c4-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="657c4-131">RequestBin è un'open source, strumento di terze parti che consente di toocreate un endpoint e visualizza le richieste inviate tooit.</span><span class="sxs-lookup"><span data-stu-id="657c4-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="657c4-132">Andare troppo[RequestBin](https://requestb.in/), fare clic su **creare un RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="657c4-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="657c4-133">Copiare l'URL bin hello, perché necessaria per la sottoscrizione toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="657c4-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="657c4-134">La sottoscrizione di argomento tooa</span><span class="sxs-lookup"><span data-stu-id="657c4-134">Subscribe tooa topic</span></span>

<span data-ttu-id="657c4-135">L'iscrizione tooa argomento tootell griglia eventi gli eventi che si desidera tootrack.</span><span class="sxs-lookup"><span data-stu-id="657c4-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="657c4-136">Hello esempio sottoscrive toohello argomento è stato creato e passa l'URL di hello da RequestBin come endpoint hello la notifica dell'evento.</span><span class="sxs-lookup"><span data-stu-id="657c4-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="657c4-137">Sostituire `<event_subscription_name>` con un nome univoco per la sottoscrizione, e `<URL_from_RequestBin>` con valore hello hello precedente sezione.</span><span class="sxs-lookup"><span data-stu-id="657c4-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="657c4-138">Se si specifica un endpoint per la sottoscrizione, griglia eventi gestisce hello routing dell'endpoint toothat eventi.</span><span class="sxs-lookup"><span data-stu-id="657c4-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="657c4-139">Per `<topic_name>`, utilizzare il valore di hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="657c4-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="657c4-140">Inviare un argomento dell'evento tooyour</span><span class="sxs-lookup"><span data-stu-id="657c4-140">Send an event tooyour topic</span></span>

<span data-ttu-id="657c4-141">A questo punto, si attivano toosee un evento come evento griglia distribuisce endpoint tooyour di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="657c4-142">In primo luogo, è ora possibile ottenere l'URL di hello e la chiave per l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="657c4-143">Usare ancora una volta il nome dell'argomento per `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="657c4-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="657c4-144">toosimplify questo articolo è stata configurata toosend toohello argomento dell'esempio evento dati.</span><span class="sxs-lookup"><span data-stu-id="657c4-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="657c4-145">In genere, un'applicazione o servizio di Azure invierebbe dati dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="657c4-146">Hello di esempio seguente ottiene i dati dell'evento hello:</span><span class="sxs-lookup"><span data-stu-id="657c4-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="657c4-147">Se si `echo "$body"` è possibile visualizzare eventi completo hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="657c4-148">Hello `data` elemento di hello JSON è payload hello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="657c4-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="657c4-149">Questo campo accetta qualsiasi JSON ben formato.</span><span class="sxs-lookup"><span data-stu-id="657c4-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="657c4-150">È inoltre possibile utilizzare il campo di soggetto hello per il routing e il filtro avanzato.</span><span class="sxs-lookup"><span data-stu-id="657c4-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="657c4-151">CURL è una utilità che esegue richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="657c4-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="657c4-152">In questo articolo, utilizziamo argomento tooour dell'evento CURL toosend hello.</span><span class="sxs-lookup"><span data-stu-id="657c4-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="657c4-153">Si have attivato l'evento hello e griglia di eventi inviati endpoint di toohello messaggio hello che è configurato per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="657c4-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="657c4-154">Sfoglia toohello RequestBin URL creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="657c4-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="657c4-155">In alternativa, fare clic su Aggiorna nel browser di RequestBin aperto.</span><span class="sxs-lookup"><span data-stu-id="657c4-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="657c4-156">Viene visualizzato l'evento di hello che appena stata inviata.</span><span class="sxs-lookup"><span data-stu-id="657c4-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="657c4-157">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="657c4-157">Clean up resources</span></span>
<span data-ttu-id="657c4-158">Se si prevede di utilizzo di questo evento toocontinue, non eseguire la pulizia delle risorse di hello create in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="657c4-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="657c4-159">Se non si prevede toocontinue, utilizzare hello seguendo le risorse di hello toodelete comando che è stato creato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="657c4-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="657c4-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="657c4-160">Next steps</span></span>

<span data-ttu-id="657c4-161">Ora che è stato appreso come toocreate argomenti e sottoscrizioni di eventi, ulteriori informazioni su quali griglia di eventi consente di eseguire:</span><span class="sxs-lookup"><span data-stu-id="657c4-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="657c4-162">Informazioni sulla griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="657c4-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="657c4-163">Monitorare le modifiche alla macchina virtuale con la griglia di eventi di Azure e le app per la logica</span><span class="sxs-lookup"><span data-stu-id="657c4-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
