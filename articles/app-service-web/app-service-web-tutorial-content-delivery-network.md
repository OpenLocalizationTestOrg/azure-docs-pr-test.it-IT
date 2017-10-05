---
title: Aggiungere una rete CDN a un servizio app di Azure | Microsoft Docs
description: Aggiungere una rete per la distribuzione di contenuti (CDN) a un servizio app di Azure per memorizzare nella cache e distribuire i file statici dai server vicini ai clienti in tutto il mondo.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="d9043-103">Aggiungere una rete per la distribuzione di contenuti (CDN) a un servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="d9043-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="d9043-104">La [rete per la distribuzione di contenuti (CDN) di Azure](../cdn/cdn-overview.md) memorizza nella cache il contenuto Web statico in località strategiche per offrire la massima velocità effettiva per la distribuzione del contenuto agli utenti.</span><span class="sxs-lookup"><span data-stu-id="d9043-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="d9043-105">La rete CDN riduce anche il carico del server per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="d9043-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="d9043-106">Questa esercitazione illustra come aggiungere la rete CDN di Azure a un'[app Web nel servizio app di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="d9043-107">Di seguito è riportata la home page del sito HTML statico di esempio che verrà usato:</span><span class="sxs-lookup"><span data-stu-id="d9043-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Home page dell'app di esempio](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="d9043-109">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d9043-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9043-110">Creare un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d9043-111">Aggiornare gli asset memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="d9043-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="d9043-112">Usare stringhe di query per controllare le versioni memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="d9043-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="d9043-113">Usare un dominio personalizzato per l'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9043-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d9043-114">Prerequisites</span></span>

<span data-ttu-id="d9043-115">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d9043-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="d9043-116">Installare Git</span><span class="sxs-lookup"><span data-stu-id="d9043-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="d9043-117">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d9043-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="d9043-118">Creare l'app Web</span><span class="sxs-lookup"><span data-stu-id="d9043-118">Create the web app</span></span>

<span data-ttu-id="d9043-119">Per creare l'app Web che verrà usata, seguire le istruzioni riportate nella [guida introduttiva per siti HTML statici](app-service-web-get-started-html.md) fino al passaggio **Pulire le risorse**.</span><span class="sxs-lookup"><span data-stu-id="d9043-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="d9043-120">Preparare un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="d9043-120">Have a custom domain ready</span></span>

<span data-ttu-id="d9043-121">Per completare il passaggio di questa esercitazione relativo al dominio personalizzato, è necessario essere proprietario di un dominio personalizzato e avere accesso al registro DNS per il provider di dominio, ad esempio GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="d9043-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="d9043-122">Ad esempio, per aggiungere le voci DNS per `contoso.com` e `www.contoso.com`, è necessario avere l’accesso per configurare le impostazioni DNS per il dominio radice `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d9043-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="d9043-123">Se non si ha ancora un nome di dominio, può essere opportuno seguire l'[esercitazione relativa ai domini nel servizio app](custom-dns-web-site-buydomains-web-app.md) per acquistare un dominio usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9043-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="d9043-124">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9043-124">Log in to the Azure portal</span></span>

<span data-ttu-id="d9043-125">Aprire un browser e passare al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9043-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="d9043-126">Creare un profilo e un endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d9043-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="d9043-127">Nel riquadro di spostamento a sinistra selezionare **Servizi app** e quindi l'app creata nella [guida introduttiva per siti HTML statici](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Selezionare Servizi app nel portale](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="d9043-129">Nella sezione **Impostazioni** della pagina **Servizio app** selezionare **Rete > Configurare la rete CDN di Azure per l'app**.</span><span class="sxs-lookup"><span data-stu-id="d9043-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Selezionare la rete CDN nel portale](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="d9043-131">Nella pagina **Rete per la distribuzione di contenuti di Azure** specificare le impostazioni in **Nuovo endpoint** come indicato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="d9043-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Creare un profilo e un endpoint nel portale](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="d9043-133">Impostazione</span><span class="sxs-lookup"><span data-stu-id="d9043-133">Setting</span></span> | <span data-ttu-id="d9043-134">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="d9043-134">Suggested value</span></span> | <span data-ttu-id="d9043-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d9043-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="d9043-136">**Profilo CDN**</span><span class="sxs-lookup"><span data-stu-id="d9043-136">**CDN profile**</span></span> | <span data-ttu-id="d9043-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="d9043-137">myCDNProfile</span></span> | <span data-ttu-id="d9043-138">Selezionare **Crea nuovo** per creare un profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="d9043-139">Un profilo di rete CDN è una raccolta di endpoint della rete CDN con lo stesso piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="d9043-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="d9043-140">**Piano tariffario**</span><span class="sxs-lookup"><span data-stu-id="d9043-140">**Pricing tier**</span></span> | <span data-ttu-id="d9043-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="d9043-141">Standard Akamai</span></span> | <span data-ttu-id="d9043-142">Il [piano tariffario](../cdn/cdn-overview.md#azure-cdn-features) specifica il provider e le funzionalità disponibili.</span><span class="sxs-lookup"><span data-stu-id="d9043-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="d9043-143">In questa esercitazione si userà Akamai standard.</span><span class="sxs-lookup"><span data-stu-id="d9043-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="d9043-144">**Nome endpoint rete CDN**</span><span class="sxs-lookup"><span data-stu-id="d9043-144">**CDN endpoint name**</span></span> | <span data-ttu-id="d9043-145">Qualsiasi nome univoco nel dominio azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d9043-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="d9043-146">Si accede alle risorse memorizzate nella cache nel dominio *\<nomeendpoint>.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="d9043-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="d9043-147">Selezionare **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9043-147">Select **Create**.</span></span>

<span data-ttu-id="d9043-148">Azure crea il profilo e l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9043-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="d9043-149">Il nuovo endpoint verrà visualizzato nell'elenco **Endpoint** nella stessa pagina e al termine del relativo provisioning lo stato sarà **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="d9043-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Nuovo endpoint nell'elenco](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="d9043-151">Testare l'endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d9043-151">Test the CDN endpoint</span></span>

<span data-ttu-id="d9043-152">Se è stato selezionato il piano tariffario Verizon, la propagazione dell'endpoint richiede in genere circa 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="d9043-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="d9043-153">Per Akamai è sufficiente qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="d9043-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="d9043-154">L'app di esempio include un file `index.html` e le cartelle *css*, *img* e *js* che contengono altri asset statici.</span><span class="sxs-lookup"><span data-stu-id="d9043-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="d9043-155">I percorsi del contenuto per tutti questi file sono gli stessi nell'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="d9043-156">Entrambi gli URL seguenti, ad esempio, accedono al file *bootstrap.css* nella cartella *css*:</span><span class="sxs-lookup"><span data-stu-id="d9043-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="d9043-157">Usare un browser per passare all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="d9043-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Home page dell'app di esempio fornita dalla rete CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="d9043-159">Viene visualizzata la stessa pagina eseguita in precedenza in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9043-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="d9043-160">La rete CDN di Azure ha recuperato gli asset dell'app Web di origine e li specifica dal proprio endpoint</span><span class="sxs-lookup"><span data-stu-id="d9043-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="d9043-161">Per assicurarsi che questa pagina sia memorizzata nella cache nella rete CDN, aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="d9043-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="d9043-162">Affinché la rete CDN memorizzi nella cache il contenuto richiesto sono talvolta necessarie due richieste dello stesso asset.</span><span class="sxs-lookup"><span data-stu-id="d9043-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="d9043-163">Per altre informazioni sulla creazione dei profili e degli endpoint della rete CDN di Azure, vedere [Introduzione alla rete CDN di Azure](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="d9043-164">Ripulire la rete CDN</span><span class="sxs-lookup"><span data-stu-id="d9043-164">Purge the CDN</span></span>

<span data-ttu-id="d9043-165">La rete CDN aggiorna periodicamente le proprie risorse dall'app Web di origine in base alla configurazione della durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="d9043-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="d9043-166">La durata predefinita è di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="d9043-166">The default TTL is seven days.</span></span>

<span data-ttu-id="d9043-167">Potrebbe essere talvolta necessario aggiornare la rete CDN prima della scadenza del valore TTL, ad esempio quando si distribuisce contenuto aggiornato nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="d9043-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="d9043-168">Per attivare un aggiornamento, è possibile ripulire manualmente le risorse della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="d9043-169">In questa sezione dell'esercitazione si distribuirà una modifica nell'app Web e si ripulirà la rete CDN per attivare l'aggiornamento della cache.</span><span class="sxs-lookup"><span data-stu-id="d9043-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="d9043-170">Distribuire una modifica nell'app Web</span><span class="sxs-lookup"><span data-stu-id="d9043-170">Deploy a change to the web app</span></span>

<span data-ttu-id="d9043-171">Aprire il file `index.html` e aggiungere "- V2" all'intestazione H1 come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d9043-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="d9043-172">Eseguire il commit della modifica e distribuirla nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="d9043-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="d9043-173">Al termine della distribuzione, passando all'URL dell'app Web verrà visualizzata la modifica.</span><span class="sxs-lookup"><span data-stu-id="d9043-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

!["V2" nel titolo nell'app Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="d9043-175">Passando all'URL dell'endpoint della rete CDN per la home page, la modifica non verrà visualizzata perché la versione memorizzata nella cache nella rete CDN non è ancora scaduta.</span><span class="sxs-lookup"><span data-stu-id="d9043-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Titolo nella rete CDN senza "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="d9043-177">Ripulire la rete CDN nel portale</span><span class="sxs-lookup"><span data-stu-id="d9043-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="d9043-178">Per attivare l'aggiornamento della versione memorizzata nella cache nella rete CDN, ripulire la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="d9043-179">Nel riquadro di spostamento a sinistra nel portale selezionare **Gruppi di risorse** e quindi il gruppo di risorse creato per l'app Web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="d9043-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Selezionare il gruppo di risorse](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="d9043-181">Nell'elenco delle risorse selezionare l'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-181">In the list of resources, select your CDN endpoint.</span></span>

![Selezionare l'endpoint](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="d9043-183">Nella parte superiore della pagina **Endpoint** fare clic su **Ripulisci**.</span><span class="sxs-lookup"><span data-stu-id="d9043-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Selezionare Ripulisci](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="d9043-185">Immettere i percorsi del contenuto che si vuole ripulire.</span><span class="sxs-lookup"><span data-stu-id="d9043-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="d9043-186">È possibile passare un percorso file completo per ripulire un singolo file oppure un segmento di percorso per ripulire e aggiornare tutto il contenuto in una cartella.</span><span class="sxs-lookup"><span data-stu-id="d9043-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="d9043-187">Dato che è stato modificato `index.html`, verificare che sia incluso in tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="d9043-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="d9043-188">Nella parte inferiore della pagina selezionare **Ripulisci**.</span><span class="sxs-lookup"><span data-stu-id="d9043-188">At the bottom of the page, select **Purge**.</span></span>

![Pagina Ripulisci](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="d9043-190">Verificare che la rete CDN sia aggiornata</span><span class="sxs-lookup"><span data-stu-id="d9043-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="d9043-191">Attendere il completamento dell'elaborazione della richiesta di ripulitura, che in genere richiede qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="d9043-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="d9043-192">Per visualizzare lo stato corrente, selezionare l'icona a forma di campana nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="d9043-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Notifica di ripulitura](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="d9043-194">Passando all'URL dell'endpoint della rete CDN per `index.html`, "V2" risulterà ora aggiunto al titolo nella home page.</span><span class="sxs-lookup"><span data-stu-id="d9043-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="d9043-195">Ciò dimostra che la cache della rete CDN è stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="d9043-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" nel titolo nella rete CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="d9043-197">Per altre informazioni, vedere [Ripulire un endpoint della rete CDN di Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="d9043-198">Usare le stringhe di query per il controllo delle versioni del contenuto</span><span class="sxs-lookup"><span data-stu-id="d9043-198">Use query strings to version content</span></span>

<span data-ttu-id="d9043-199">Per il comportamento di memorizzazione nella cache, la rete CDN di Azure offre le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9043-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="d9043-200">Ignora stringhe di query</span><span class="sxs-lookup"><span data-stu-id="d9043-200">Ignore query strings</span></span>
* <span data-ttu-id="d9043-201">Disabilita la memorizzazione nella cache per le stringhe di query</span><span class="sxs-lookup"><span data-stu-id="d9043-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="d9043-202">Memorizza nella cache tutti gli URL univoci</span><span class="sxs-lookup"><span data-stu-id="d9043-202">Cache every unique URL</span></span> 

<span data-ttu-id="d9043-203">La prima è l'opzione predefinita, ovvero esiste una sola versione di un asset memorizzata nella cache indipendentemente dalla stringa di query nell'URL.</span><span class="sxs-lookup"><span data-stu-id="d9043-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="d9043-204">In questa sezione dell'esercitazione si modificherà il comportamento per memorizzare nella cache tutti gli URL univoci.</span><span class="sxs-lookup"><span data-stu-id="d9043-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="d9043-205">Modificare il comportamento della cache</span><span class="sxs-lookup"><span data-stu-id="d9043-205">Change the cache behavior</span></span>

<span data-ttu-id="d9043-206">Nella pagina **Endpoint rete CDN** del portale di Azure selezionare **Cache**.</span><span class="sxs-lookup"><span data-stu-id="d9043-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="d9043-207">Selezionare **Memorizza nella cache tutti gli URL univoci** nell'elenco a discesa **Comportamento di memorizzazione nella cache della stringa di query**.</span><span class="sxs-lookup"><span data-stu-id="d9043-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="d9043-208">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d9043-208">Select **Save**.</span></span>

![Selezionare il comportamento di memorizzazione nella cache della stringa di query](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="d9043-210">Verificare che gli URL univoci vengano memorizzati nella cache separatamente</span><span class="sxs-lookup"><span data-stu-id="d9043-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="d9043-211">In un browser passare alla home page nell'endpoint della rete CDN includendo però una stringa di query:</span><span class="sxs-lookup"><span data-stu-id="d9043-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="d9043-212">La rete CDN restituirà il contenuto corrente dell'app Web, che include "V2" nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="d9043-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="d9043-213">Per assicurarsi che questa pagina sia memorizzata nella cache nella rete CDN, aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="d9043-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="d9043-214">Aprire `index.html`, modificare "V2" in "V3" e distribuire la modifica.</span><span class="sxs-lookup"><span data-stu-id="d9043-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="d9043-215">In un browser passare all'URL dell'endpoint della rete CDN con una nuova stringa di query come `q=2`.</span><span class="sxs-lookup"><span data-stu-id="d9043-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="d9043-216">La rete CDN recupera il file `index.html` corrente e visualizza "V3".</span><span class="sxs-lookup"><span data-stu-id="d9043-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="d9043-217">Se invece si passa all'endpoint della rete CDN con la stringa di query `q=1`, viene visualizzato "V2".</span><span class="sxs-lookup"><span data-stu-id="d9043-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" nel titolo nella rete CDN, con stringa di query 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" nel titolo nella rete CDN, con stringa di query 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="d9043-220">Questo output mostra che ogni stringa di query viene trattata in modo diverso:</span><span class="sxs-lookup"><span data-stu-id="d9043-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="d9043-221">Poiché q=1 è stata usata in precedenza, vengono restituiti i contenuti memorizzati nella cache (V2).</span><span class="sxs-lookup"><span data-stu-id="d9043-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="d9043-222">Poiché q=2 non è mai stata usata, vengono recuperati e restituiti i contenuti dell'app Web più recenti (V3).</span><span class="sxs-lookup"><span data-stu-id="d9043-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="d9043-223">Per altre informazioni, vedere [Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="d9043-224">Eseguire il mapping di un dominio personalizzato a un endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d9043-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="d9043-225">Per eseguire il mapping del dominio personalizzato all'endpoint della rete CDN si creerà un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="d9043-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="d9043-226">Un record CNAME è una funzionalità DNS tramite cui viene eseguito il mapping di un dominio di origine a uno di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d9043-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="d9043-227">Ad esempio, si potrebbe eseguire il mapping di `cdn.contoso.com` o `static.contoso.com` a `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="d9043-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="d9043-228">Se non si ha un dominio personalizzato, può essere opportuno seguire l'[esercitazione relativa ai domini nel servizio app](custom-dns-web-site-buydomains-web-app.md) per acquistare un dominio usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9043-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="d9043-229">Trovare il nome host da usare con il record CNAME</span><span class="sxs-lookup"><span data-stu-id="d9043-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="d9043-230">Nella pagina **Endpoint** del portale di Azure verificare che nel riquadro di spostamento a sinistra sia selezionata l'opzione **Panoramica** e quindi selezionare il pulsante **+ Dominio personalizzato** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="d9043-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Selezionare l'aggiunta di un dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="d9043-232">Nella pagina **Aggiungi dominio personalizzato** verrà visualizzato il nome host dell'endpoint da usare per la creazione di un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="d9043-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="d9043-233">Il nome host è derivato dall'URL dell'endpoint della rete CDN: **&lt;NomeEndpoint>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="d9043-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Pagina per l'aggiunta di un dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="d9043-235">Configurare il record CNAME con il registrar</span><span class="sxs-lookup"><span data-stu-id="d9043-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="d9043-236">Passare al sito Web del registrar e individuare la sezione per la creazione di record DNS.</span><span class="sxs-lookup"><span data-stu-id="d9043-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="d9043-237">Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="d9043-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="d9043-238">Individuare la sezione per la gestione dei record CNAME.</span><span class="sxs-lookup"><span data-stu-id="d9043-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="d9043-239">Potrebbe essere necessario passare a una pagina di impostazioni avanzate e cercare le parole CNAME, Alias o Subdomains.</span><span class="sxs-lookup"><span data-stu-id="d9043-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="d9043-240">Creare un record CNAME per il mapping del sottodominio scelto (ad esempio, **static** o **cdn**) al **nome host dell'endpoint** visualizzato in precedenza nel portale.</span><span class="sxs-lookup"><span data-stu-id="d9043-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="d9043-241">Immettere il dominio personalizzato in Azure</span><span class="sxs-lookup"><span data-stu-id="d9043-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="d9043-242">Tornare alla pagina **Aggiungi dominio personalizzato** e immettere il dominio personalizzato, includendo il sottodominio, nella finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d9043-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="d9043-243">Ad esempio, immettere `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d9043-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="d9043-244">Azure verifica l'esistenza del record CNAME per il nome di dominio immesso.</span><span class="sxs-lookup"><span data-stu-id="d9043-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="d9043-245">Se il record CNAME è corretto, il dominio personalizzato viene convalidato.</span><span class="sxs-lookup"><span data-stu-id="d9043-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="d9043-246">La propagazione del record CNAME nei server dei nomi in Internet può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="d9043-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="d9043-247">Se il dominio non viene convalidato immediatamente, attendere qualche minuto e riprovare.</span><span class="sxs-lookup"><span data-stu-id="d9043-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="d9043-248">Testare il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="d9043-248">Test the custom domain</span></span>

<span data-ttu-id="d9043-249">In un browser passare al file `index.html` usando il dominio personalizzato (ad esempio, `cdn.contoso.com/index.html`) per verificare che il risultato sia lo stesso ottenuto andando direttamente a `<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="d9043-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Home page dell'app di esempio con URL del dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="d9043-251">Per altre informazioni, vedere [Eseguire il mapping del contenuto della rete CDN di Azure a un dominio personalizzato](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d9043-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d9043-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9043-252">Next steps</span></span>

<span data-ttu-id="d9043-253">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d9043-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9043-254">Creare un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d9043-255">Aggiornare gli asset memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="d9043-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="d9043-256">Usare stringhe di query per controllare le versioni memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="d9043-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="d9043-257">Usare un dominio personalizzato per l'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d9043-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="d9043-258">Per informazioni su come ottimizzare la rete CDN, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9043-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9043-259">Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d9043-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9043-260">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d9043-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
