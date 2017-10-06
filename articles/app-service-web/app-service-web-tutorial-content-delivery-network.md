---
title: aaaAdd tooan una rete CDN Azure App Service | Documenti Microsoft
description: Aggiungere un toocache di servizio App di Azure tooan rete CDN (Content Delivery) e recapitare file statici dal server ai clienti tooyour Chiudi tutto il mondo hello.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="eab2e-103">Aggiungere un tooan rete CDN (Content Delivery) servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="eab2e-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="eab2e-104">[Rete di distribuzione Azure contenuti (CDN)](../cdn/cdn-overview.md) memorizza nella cache il contenuto web statico in percorsi strategici tooprovide massima velocità effettiva per il recapito toousers contenuto.</span><span class="sxs-lookup"><span data-stu-id="eab2e-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="eab2e-105">Hello CDN riduce anche il carico del server nell'app web.</span><span class="sxs-lookup"><span data-stu-id="eab2e-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="eab2e-106">Questa esercitazione viene illustrato come tooadd rete CDN di Azure tooa [app web in Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="eab2e-107">Ecco hello home page di hello esempio sito HTML statico che è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="eab2e-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Home page dell'app di esempio](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="eab2e-109">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="eab2e-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eab2e-110">Creare un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="eab2e-111">Aggiornare gli asset memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="eab2e-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="eab2e-112">Versioni di toocontrol memorizzati nella cache delle stringhe di query di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="eab2e-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="eab2e-113">Utilizzare un dominio personalizzato per l'endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eab2e-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eab2e-114">Prerequisites</span></span>

<span data-ttu-id="eab2e-115">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="eab2e-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="eab2e-116">Installare Git</span><span class="sxs-lookup"><span data-stu-id="eab2e-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="eab2e-117">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="eab2e-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="eab2e-118">Creare l'app web hello</span><span class="sxs-lookup"><span data-stu-id="eab2e-118">Create hello web app</span></span>

<span data-ttu-id="eab2e-119">toocreate hello web app che verranno utilizzate, seguire hello [quickstart HTML statico](app-service-web-get-started-html.md) tramite hello **Sfoglia toohello app** passaggio.</span><span class="sxs-lookup"><span data-stu-id="eab2e-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="eab2e-120">Preparare un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="eab2e-120">Have a custom domain ready</span></span>

<span data-ttu-id="eab2e-121">passaggio di dominio personalizzato hello toocomplete di questa esercitazione, è necessario tooown un dominio personalizzato e dispone del Registro di sistema di accesso tooyour DNS per il provider del dominio (ad esempio GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="eab2e-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="eab2e-122">Ad esempio, le voci DNS tooadd per `contoso.com` e `www.contoso.com`, è necessario disporre di impostazioni di accesso tooconfigure hello DNS per hello `contoso.com` dominio radice.</span><span class="sxs-lookup"><span data-stu-id="eab2e-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="eab2e-123">Se si dispone già di un nome di dominio, è consigliabile seguenti hello [esercitazione di dominio di servizio App](custom-dns-web-site-buydomains-web-app.md) toopurchase il dominio utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eab2e-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="eab2e-124">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eab2e-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="eab2e-125">Aprire un browser e passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eab2e-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="eab2e-126">Creare un profilo e un endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="eab2e-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="eab2e-127">Nel riquadro di spostamento sinistro di hello, selezionare **servizi App**e quindi selezionare l'applicazione hello creati in hello [quickstart HTML statico](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Selezionare l'applicazione di servizio App nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="eab2e-129">In hello **servizio App** hello della pagina **impostazioni** selezionare **rete > rete CDN di Azure configurare per l'app**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Selezionare una rete CDN nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="eab2e-131">In hello **rete CDN di Azure** fornire hello **nuovo endpoint** impostazioni come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Creare endpoint e del profilo nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="eab2e-133">Impostazione</span><span class="sxs-lookup"><span data-stu-id="eab2e-133">Setting</span></span> | <span data-ttu-id="eab2e-134">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="eab2e-134">Suggested value</span></span> | <span data-ttu-id="eab2e-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eab2e-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="eab2e-136">**Profilo CDN**</span><span class="sxs-lookup"><span data-stu-id="eab2e-136">**CDN profile**</span></span> | <span data-ttu-id="eab2e-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="eab2e-137">myCDNProfile</span></span> | <span data-ttu-id="eab2e-138">Selezionare **Crea nuovo** toocreate un profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="eab2e-139">Il profilo CDN è una raccolta di endpoint CDN con hello stesso livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="eab2e-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="eab2e-140">**Piano tariffario**</span><span class="sxs-lookup"><span data-stu-id="eab2e-140">**Pricing tier**</span></span> | <span data-ttu-id="eab2e-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="eab2e-141">Standard Akamai</span></span> | <span data-ttu-id="eab2e-142">Hello [tariffario](../cdn/cdn-overview.md#azure-cdn-features) specifica provider hello e le funzionalità disponibili.</span><span class="sxs-lookup"><span data-stu-id="eab2e-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="eab2e-143">In questa esercitazione si userà Akamai standard.</span><span class="sxs-lookup"><span data-stu-id="eab2e-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="eab2e-144">**Nome endpoint rete CDN**</span><span class="sxs-lookup"><span data-stu-id="eab2e-144">**CDN endpoint name**</span></span> | <span data-ttu-id="eab2e-145">Qualsiasi nome che è univoco nel dominio azureedge.net hello</span><span class="sxs-lookup"><span data-stu-id="eab2e-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="eab2e-146">Accedere alle risorse memorizzate nella cache dominio hello  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="eab2e-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="eab2e-147">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-147">Select **Create**.</span></span>

<span data-ttu-id="eab2e-148">Azure Crea profilo hello e endpoint.</span><span class="sxs-lookup"><span data-stu-id="eab2e-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="eab2e-149">viene visualizzata di nuovo endpoint Hello in hello **endpoint** elenco hello stessa pagina, e quando è disponibile lo stato di hello è **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Nuovo endpoint nell'elenco](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="eab2e-151">Hello test endpoint rete CDN</span><span class="sxs-lookup"><span data-stu-id="eab2e-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="eab2e-152">Se è stato selezionato il piano tariffario Verizon, la propagazione dell'endpoint richiede in genere circa 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="eab2e-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="eab2e-153">Per Akamai è sufficiente qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="eab2e-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="eab2e-154">applicazione di esempio Hello ha un `index.html` file e *css*, *img*, e *js* cartelle che contengono altre risorse statici.</span><span class="sxs-lookup"><span data-stu-id="eab2e-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="eab2e-155">percorsi per tutti i file sono contenuto Hello hello stesso all'endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="eab2e-156">Ad esempio, entrambi gli URL seguenti hello accedere hello *bootstrap.css* file hello *css* cartella:</span><span class="sxs-lookup"><span data-stu-id="eab2e-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="eab2e-157">Passare un toohello browser URL seguente:</span><span class="sxs-lookup"><span data-stu-id="eab2e-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Home page dell'app di esempio fornita dalla rete CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="eab2e-159">Vedrai hello stessa pagina è stata eseguita in precedenza in un'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eab2e-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="eab2e-160">Rete CDN di Azure ha recuperato asset dell'app web origine di hello e viene utilizzata dall'endpoint rete CDN hello</span><span class="sxs-lookup"><span data-stu-id="eab2e-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="eab2e-161">tooensure che questa pagina memorizzato nella cache di hello CDN, aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="eab2e-162">Due richieste hello stesso asset sono talvolta necessarie per toocache CDN hello hello contenuto richiesto.</span><span class="sxs-lookup"><span data-stu-id="eab2e-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="eab2e-163">Per altre informazioni sulla creazione dei profili e degli endpoint della rete CDN di Azure, vedere [Introduzione alla rete CDN di Azure](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="eab2e-164">Ripulire hello rete CDN</span><span class="sxs-lookup"><span data-stu-id="eab2e-164">Purge hello CDN</span></span>

<span data-ttu-id="eab2e-165">rete CDN Hello Aggiorna periodicamente le risorse da app web di origine hello in base alla configurazione di hello time-to-live (TTL).</span><span class="sxs-lookup"><span data-stu-id="eab2e-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="eab2e-166">durata TTL predefinita Hello è sette giorni.</span><span class="sxs-lookup"><span data-stu-id="eab2e-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="eab2e-167">In alcuni casi potrebbe essere necessario toorefresh hello CDN prima della scadenza di TTL: hello, ad esempio, quando si distribuisce l'app web toohello contenuto aggiornato.</span><span class="sxs-lookup"><span data-stu-id="eab2e-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="eab2e-168">tootrigger un aggiornamento, è possibile eliminare manualmente le risorse di rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="eab2e-169">In questa sezione dell'esercitazione hello, si distribuisce un'app web toohello di modifica e ripulitura hello CDN tootrigger hello CDN toorefresh la cache.</span><span class="sxs-lookup"><span data-stu-id="eab2e-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="eab2e-170">Distribuire un'app web toohello di modifica</span><span class="sxs-lookup"><span data-stu-id="eab2e-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="eab2e-171">Aprire hello `index.html` file e aggiungere "-V2" intestazione H1 toohello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="eab2e-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="eab2e-172">Eseguire il commit della modifica e distribuirlo toohello web app.</span><span class="sxs-lookup"><span data-stu-id="eab2e-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="eab2e-173">Una volta completata la distribuzione, URL dell'app web toohello Sfoglia e visualizzato hello modificare.</span><span class="sxs-lookup"><span data-stu-id="eab2e-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

!["V2" nel titolo nell'app Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="eab2e-175">URL dell'endpoint rete CDN toohello Sfoglia per hello home page e si non si rilevano hello modificare la versione memorizzata nella cache di hello in hello CDN non è ancora scaduto.</span><span class="sxs-lookup"><span data-stu-id="eab2e-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Titolo nella rete CDN senza "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="eab2e-177">Ripulire hello CDN nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="eab2e-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="eab2e-178">tootrigger hello CDN tooupdate la versione memorizzata nella cache, cancellare hello CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="eab2e-179">Spostamento a sinistra del portale hello, selezionare **gruppi di risorse**, quindi selezionare gruppo di risorse hello creato per l'app web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="eab2e-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Selezionare il gruppo di risorse](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="eab2e-181">Nell'elenco di hello delle risorse, selezionare l'endpoint CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-181">In hello list of resources, select your CDN endpoint.</span></span>

![Selezionare l'endpoint](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="eab2e-183">Nella parte superiore di hello di hello **Endpoint** pagina, fare clic su **ripulire**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Selezionare Ripulisci](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="eab2e-185">Immettere i percorsi del contenuto hello desiderato toopurge.</span><span class="sxs-lookup"><span data-stu-id="eab2e-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="eab2e-186">È possibile passare un toopurge percorso completo del file, un singolo file o un toopurge segmento di percorso e aggiorna tutto il contenuto in una cartella.</span><span class="sxs-lookup"><span data-stu-id="eab2e-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="eab2e-187">Poiché hai cambiato `index.html`, assicurarsi che sia uno dei percorsi di hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="eab2e-188">Nella parte inferiore di hello della pagina hello, selezionare **ripulire**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-188">At hello bottom of hello page, select **Purge**.</span></span>

![Pagina Ripulisci](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="eab2e-190">Verificare che hello che viene aggiornata della rete CDN</span><span class="sxs-lookup"><span data-stu-id="eab2e-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="eab2e-191">Attendere che la richiesta di eliminazione hello ha completato l'elaborazione, in genere un paio di minuti.</span><span class="sxs-lookup"><span data-stu-id="eab2e-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="eab2e-192">toosee hello lo stato corrente, icona campana hello selezionare nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Notifica di ripulitura](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="eab2e-194">Individuare l'URL dell'endpoint rete CDN toohello per `index.html`, ed è ora possibile visualizzare hello V2 che è stato aggiunto toohello titolo hello home page.</span><span class="sxs-lookup"><span data-stu-id="eab2e-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="eab2e-195">Ciò indica che è stata aggiornata per cache di hello rete CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" nel titolo nella rete CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="eab2e-197">Per altre informazioni, vedere [Ripulire un endpoint della rete CDN di Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="eab2e-198">Utilizzare il contenuto di tooversion stringhe di query</span><span class="sxs-lookup"><span data-stu-id="eab2e-198">Use query strings tooversion content</span></span>

<span data-ttu-id="eab2e-199">Hello rete CDN di Azure offre hello le opzioni di memorizzazione nella cache comportamento seguenti:</span><span class="sxs-lookup"><span data-stu-id="eab2e-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="eab2e-200">Ignora stringhe di query</span><span class="sxs-lookup"><span data-stu-id="eab2e-200">Ignore query strings</span></span>
* <span data-ttu-id="eab2e-201">Disabilita la memorizzazione nella cache per le stringhe di query</span><span class="sxs-lookup"><span data-stu-id="eab2e-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="eab2e-202">Memorizza nella cache tutti gli URL univoci</span><span class="sxs-lookup"><span data-stu-id="eab2e-202">Cache every unique URL</span></span> 

<span data-ttu-id="eab2e-203">Hello innanzitutto di questi è l'impostazione predefinita di hello, che non esiste un'unica versione memorizzata nella cache di un cespite indipendentemente dalla stringa di query hello hello URL.</span><span class="sxs-lookup"><span data-stu-id="eab2e-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="eab2e-204">In questa sezione dell'esercitazione hello è modificare hello la memorizzazione nella cache comportamento toocache tutti gli URL univoci.</span><span class="sxs-lookup"><span data-stu-id="eab2e-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="eab2e-205">Modificare il comportamento della cache di hello</span><span class="sxs-lookup"><span data-stu-id="eab2e-205">Change hello cache behavior</span></span>

<span data-ttu-id="eab2e-206">Nel portale di Azure hello **Endpoint rete CDN** selezionare **Cache**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="eab2e-207">Selezionare **memorizzare nella Cache tutti gli URL univoci** da hello **stringa di Query, il comportamento di memorizzazione nella cache** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="eab2e-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="eab2e-208">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-208">Select **Save**.</span></span>

![Selezionare il comportamento di memorizzazione nella cache della stringa di query](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="eab2e-210">Verificare che gli URL univoci vengano memorizzati nella cache separatamente</span><span class="sxs-lookup"><span data-stu-id="eab2e-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="eab2e-211">In un browser, passare l'endpoint rete CDN hello toohello home page, ma includono una stringa di query:</span><span class="sxs-lookup"><span data-stu-id="eab2e-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="eab2e-212">rete CDN Hello restituisce hello web app contenuto corrente, ovvero "2" nell'intestazione di hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="eab2e-213">tooensure che questa pagina memorizzato nella cache di hello CDN, aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="eab2e-214">Aprire `index.html` e modificare anche "V2" "V3" e distribuire hello modifica.</span><span class="sxs-lookup"><span data-stu-id="eab2e-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="eab2e-215">In un browser, passare l'URL dell'endpoint rete CDN toohello con una nuova stringa di query, ad esempio `q=2`.</span><span class="sxs-lookup"><span data-stu-id="eab2e-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="eab2e-216">rete CDN Hello Ottiene hello corrente `index.html` file e visualizza "V3".</span><span class="sxs-lookup"><span data-stu-id="eab2e-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="eab2e-217">Ma se si passa l'endpoint rete CDN toohello con hello `q=1` stringa di query viene visualizzato "V2".</span><span class="sxs-lookup"><span data-stu-id="eab2e-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" nel titolo nella rete CDN, con stringa di query 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" nel titolo nella rete CDN, con stringa di query 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="eab2e-220">Questo output mostra che ogni stringa di query viene trattata in modo diverso:</span><span class="sxs-lookup"><span data-stu-id="eab2e-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="eab2e-221">Poiché q=1 è stata usata in precedenza, vengono restituiti i contenuti memorizzati nella cache (V2).</span><span class="sxs-lookup"><span data-stu-id="eab2e-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="eab2e-222">q = 2 è una novità, in modo più recente contenuto dell'app web hello viene recuperati e restituito (V3).</span><span class="sxs-lookup"><span data-stu-id="eab2e-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="eab2e-223">Per altre informazioni, vedere [Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="eab2e-224">Eseguire il mapping di un endpoint rete CDN tooa di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="eab2e-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="eab2e-225">Viene eseguito il mapping del tooyour dominio personalizzato CDN Endpoint tramite la creazione di un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="eab2e-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="eab2e-226">Un record CNAME è una funzionalità DNS che esegue il mapping di un dominio di destinazione tooa di dominio di origine.</span><span class="sxs-lookup"><span data-stu-id="eab2e-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="eab2e-227">Ad esempio, è possibile mappare `cdn.contoso.com` o `static.contoso.com` troppo`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="eab2e-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="eab2e-228">Se non si dispone di un dominio personalizzato, prendere in considerazione seguenti hello [esercitazione di dominio di servizio App](custom-dns-web-site-buydomains-web-app.md) toopurchase il dominio utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eab2e-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="eab2e-229">Trovare hello hostname toouse con hello CNAME</span><span class="sxs-lookup"><span data-stu-id="eab2e-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="eab2e-230">Nel portale di Azure hello **Endpoint** assicurarsi **Panoramica** è selezionata in hello sinistro spostamento e quindi seleziona hello **+ dominio personalizzato** pulsante nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Selezionare l'aggiunta di un dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="eab2e-232">In hello **aggiungere un dominio personalizzato** visualizzata hello toouse nome host di endpoint per la creazione di un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="eab2e-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="eab2e-233">nome host Hello è derivato dall'URL dell'endpoint rete CDN:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Pagina per l'aggiunta di un dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="eab2e-235">Configurare hello CNAME con il registrar</span><span class="sxs-lookup"><span data-stu-id="eab2e-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="eab2e-236">Sito web del registrar di dominio tooyour passare e individuare la sezione hello per la creazione di record DNS.</span><span class="sxs-lookup"><span data-stu-id="eab2e-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="eab2e-237">Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="eab2e-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="eab2e-238">Trovare la sezione hello per la gestione dei record CNAME.</span><span class="sxs-lookup"><span data-stu-id="eab2e-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="eab2e-239">È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello CNAME, Alias o diversi sottodomini.</span><span class="sxs-lookup"><span data-stu-id="eab2e-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="eab2e-240">Creare un record CNAME che esegue il mapping del sottodominio scelto (ad esempio, **statico** o **cdn**) toohello **nome host dell'Endpoint** illustrato in precedenza nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="eab2e-241">Immettere dominio personalizzato hello in Azure</span><span class="sxs-lookup"><span data-stu-id="eab2e-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="eab2e-242">Restituire toohello **aggiungere un dominio personalizzato** pagina e immettere il dominio personalizzato, inclusi il sottodominio hello, nella finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="eab2e-243">Ad esempio, immettere `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="eab2e-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="eab2e-244">Azure verifica l'esistenza di record CNAME hello hello nome di dominio immesso.</span><span class="sxs-lookup"><span data-stu-id="eab2e-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="eab2e-245">Se hello CNAME è corretto, viene convalidato il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="eab2e-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="eab2e-246">Per i server di tooname toopropagate record CNAME hello in hello Internet può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="eab2e-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="eab2e-247">Se il dominio non viene convalidato immediatamente, attendere qualche minuto e riprovare.</span><span class="sxs-lookup"><span data-stu-id="eab2e-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="eab2e-248">Dominio personalizzato hello di test</span><span class="sxs-lookup"><span data-stu-id="eab2e-248">Test hello custom domain</span></span>

<span data-ttu-id="eab2e-249">In un browser, passare toohello `index.html` file utilizzando il dominio personalizzato (ad esempio, `cdn.contoso.com/index.html`) tooverify hello risultato del metodo hello stesso come quando si passa direttamente troppo`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="eab2e-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Home page dell'app di esempio con URL del dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="eab2e-251">Per ulteriori informazioni, vedere [dominio di rete CDN di Azure mappa tooa contenuto personalizzato](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="eab2e-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="eab2e-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eab2e-252">Next steps</span></span>

<span data-ttu-id="eab2e-253">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="eab2e-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eab2e-254">Creare un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="eab2e-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="eab2e-255">Aggiornare gli asset memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="eab2e-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="eab2e-256">Versioni di toocontrol memorizzati nella cache delle stringhe di query di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="eab2e-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="eab2e-257">Utilizzare un dominio personalizzato per l'endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="eab2e-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="eab2e-258">Informazioni su come le prestazioni della rete CDN toooptimize hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="eab2e-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eab2e-259">Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="eab2e-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="eab2e-260">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="eab2e-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
