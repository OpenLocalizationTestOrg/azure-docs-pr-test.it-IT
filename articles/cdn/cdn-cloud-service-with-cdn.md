---
title: un servizio cloud di Azure con la rete CDN Azure aaaIntegrate | Documenti Microsoft
description: Informazioni su come toodeploy un servizio cloud che fornisce contenuto da un endpoint rete CDN di Azure integrato
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="a8a85-103"><a name="intro"></a> Integrare un servizio cloud con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="a8a85-104">Un servizio cloud può essere integrato con una rete CDN di Azure, del contenuto dal percorso del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="a8a85-105">In questo modo di approccio hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a8a85-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="a8a85-106">Facile distribuzione e aggiornamento di immagini, script e fogli di stile nelle directory del progetto servizio cloud</span><span class="sxs-lookup"><span data-stu-id="a8a85-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="a8a85-107">Aggiornare facilmente i pacchetti di NuGet hello nel servizio cloud, ad esempio jQuery o le versioni di Bootstrap</span><span class="sxs-lookup"><span data-stu-id="a8a85-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="a8a85-108">Gestire l'applicazione Web e la rete CDN-serviti contenuti tutte da hello stessa interfaccia di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8a85-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="a8a85-109">Flusso di lavoro di distribuzione unificato per l'applicazione Web e il contenuto gestito dalla rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="a8a85-110">Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a8a85-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a8a85-111">What you will learn</span></span>
<span data-ttu-id="a8a85-112">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="a8a85-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="a8a85-113">Integrare un endpoint della rete CDN di Azure con il servizio cloud e rendere disponibile il contenuto statico nella pagine Web dalla rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="a8a85-114">Configurare le impostazioni della cache per il contenuto statico nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="a8a85-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="a8a85-115">Gestire il contenuto dalle azioni del controller tramite la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="a8a85-116">Serve in bundle e minimizzare contenuto tramite rete CDN di Azure mantenendo script hello debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8a85-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="a8a85-117">Configurare il fallback di script e file CSS quando la rete CDN di Azure è offline</span><span class="sxs-lookup"><span data-stu-id="a8a85-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="a8a85-118">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="a8a85-118">What you will build</span></span>
<span data-ttu-id="a8a85-119">Verrà distribuito un ruolo Web del servizio cloud utilizzando il modello di MVC ASP.NET predefinito di hello, aggiungere il contenuto di tooserve codice di una rete CDN Azure integrata, ad esempio un'immagine, i risultati dell'azione controller e i file di JavaScript e CSS di predefinito hello e anche scrivere hello tooconfigure codice meccanismo di fallback per bundle servita nell'evento hello che hello CDN è offline.</span><span class="sxs-lookup"><span data-stu-id="a8a85-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="a8a85-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8a85-120">What you will need</span></span>
<span data-ttu-id="a8a85-121">Per questa esercitazione sono hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="a8a85-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="a8a85-122">Un [account Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="a8a85-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="a8a85-123">Visual Studio 2015 con [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="a8a85-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="a8a85-124">È necessario un account di Azure di toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="a8a85-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="a8a85-125">È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che vengono utilizzati fino è possibile tenere conto di hello e liberare di utilizzare servizi di Azure, ad esempio siti Web.</span><span class="sxs-lookup"><span data-stu-id="a8a85-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="a8a85-126">È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="a8a85-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="a8a85-127">Distribuire un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="a8a85-127">Deploy a cloud service</span></span>
<span data-ttu-id="a8a85-128">In questa sezione, si verrà distribuito predefinito hello modello di applicazione MVC ASP.NET nel ruolo Web del servizio cloud tooa Visual Studio 2015 e quindi integrarlo con un nuovo endpoint CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="a8a85-129">Seguire le istruzioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8a85-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="a8a85-130">In Visual Studio 2015, creare un nuovo servizio cloud Azure dalla barra dei menu hello passando troppo**File > Nuovo > progetto > Cloud > servizio Cloud di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="a8a85-131">Assegnargli un nome e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="a8a85-132">Selezionare **ruolo Web ASP.NET** e fare clic su hello  **>**  pulsante.</span><span class="sxs-lookup"><span data-stu-id="a8a85-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="a8a85-133">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="a8a85-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="a8a85-134">Selezionare **MVC** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="a8a85-135">A questo punto, pubblicare questo tooan ruolo Web servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="a8a85-136">Fare clic sul progetto servizio cloud hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="a8a85-137">Se non hanno ancora effettuato l'accesso a Microsoft Azure, fare clic su hello **aggiungere un account...**  hello elenco a discesa e fare clic su **aggiungere un account** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="a8a85-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="a8a85-138">In hello-pagina di accesso, accedere con hello account Microsoft usato tooactivate l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="a8a85-139">Una volta effettuato l'accesso, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="a8a85-140">Supponendo che non sia stato creato un servizio cloud né un account di archiviazione, Visual Studio aiuterà a crearli entrambi.</span><span class="sxs-lookup"><span data-stu-id="a8a85-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="a8a85-141">In hello **Crea servizio Cloud e Account** finestra di dialogo, nome del tipo hello servizio desiderato e la regione desiderata hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="a8a85-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="a8a85-142">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="a8a85-143">In hello della pagina di impostazioni di pubblicazione, verificare la configurazione di hello e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="a8a85-144">processo di pubblicazione per i servizi cloud Hello richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="a8a85-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="a8a85-145">Hello Abilita distribuzione Web per l'opzione di tutti i ruoli consentono di debug del servizio cloud molto più rapidamente, fornendo tooyour aggiornamenti veloce, ma temporanei, i ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="a8a85-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="a8a85-146">Per ulteriori informazioni su questa opzione, vedere [pubblicazione di un servizio Cloud utilizzando strumenti di Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8a85-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="a8a85-147">Quando hello **Log attività di Microsoft Azure** indica che lo stato di pubblicazione è **completato**, si creerà un endpoint rete CDN è integrato con questo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a8a85-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="a8a85-148">Se, dopo la pubblicazione, servizio cloud distribuito hello Visualizza una schermata di errore, è probabile perché è utilizzato da servizio cloud hello è stato distribuito un [guest del sistema operativo che non include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="a8a85-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="a8a85-149">È possibile risolvere il problema da [distribuzione .NET 4.5.2 come attività di avvio](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a8a85-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="a8a85-150">Creare un nuovo profilo di rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-150">Create a new CDN profile</span></span>
<span data-ttu-id="a8a85-151">Un profilo di rete CDN è una raccolta di endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="a8a85-152">Ogni profilo contiene uno o più endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="a8a85-153">È preferibile toouse più profili tooorganize gli endpoint CDN dal dominio internet, l'applicazione web o ad altri criteri.</span><span class="sxs-lookup"><span data-stu-id="a8a85-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="a8a85-154">Se si dispone già di un profilo di rete CDN che si desidera toouse per questa esercitazione, andare troppo[creare un nuovo endpoint CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="a8a85-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="a8a85-155">Creare un nuovo endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="a8a85-156">**toocreate un nuovo endpoint rete CDN per l'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="a8a85-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="a8a85-157">In hello [il portale di gestione di Azure](https://portal.azure.com), passare il profilo CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="a8a85-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="a8a85-158">Si potrebbe avere aggiunto toohello dashboard nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="a8a85-159">Se è, non sarà possibile trovarlo facendo **Sfoglia**, quindi **i profili di rete CDN**, e fare clic sul profilo hello prevede tooadd l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="a8a85-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="a8a85-160">verrà visualizzata la finestra di blade profilo rete CDN di Hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-160">hello CDN profile blade appears.</span></span>
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. <span data-ttu-id="a8a85-162">Fare clic su hello **Aggiungi Endpoint** pulsante.</span><span class="sxs-lookup"><span data-stu-id="a8a85-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    <span data-ttu-id="a8a85-164">Hello **aggiungere un endpoint** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="a8a85-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. <span data-ttu-id="a8a85-166">Immettere un **Nome** per questo endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="a8a85-167">Questo nome verrà usato tooaccess le risorse memorizzate nella cache nel dominio hello `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="a8a85-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="a8a85-168">In hello **tipo di origine** elenco a discesa Seleziona *servizio Cloud*.</span><span class="sxs-lookup"><span data-stu-id="a8a85-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="a8a85-169">In hello **nome host dell'origine** elenco a discesa selezionare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a8a85-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="a8a85-170">Lasciare i valori predefiniti di hello per **il percorso di origine**, **intestazione host di origine**, e **porta protocollo/origine**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="a8a85-171">È necessario specificare almeno un protocollo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="a8a85-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="a8a85-172">Fare clic su hello **Aggiungi** toocreate pulsante hello nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="a8a85-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="a8a85-173">Dopo aver creato endpoint hello, viene visualizzato in un elenco di endpoint per il profilo hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="a8a85-174">visualizzazione elenco Hello Mostra hello URL toouse tooaccess memorizzati nella cache il contenuto, nonché il dominio di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Endpoint della rete CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="a8a85-176">endpoint di Hello non immediatamente sarà disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="a8a85-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="a8a85-177">Operazione può richiedere minuti too90 hello registrazione toopropagate tramite rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="a8a85-178">Gli utenti che tentano di nome di dominio della rete CDN hello toouse immediatamente potrebbero ricevere il codice di stato 404 fino a quando non è disponibile tramite hello CDN contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="a8a85-179">Hello test endpoint rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="a8a85-180">Quando lo stato di pubblicazione hello è **completato**, aprire una finestra del browser e passare troppo**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="a8a85-181">Nella configurazione illustrata, questo URL è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a8a85-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="a8a85-182">Che corrisponde a toohello URL di origine all'endpoint rete CDN hello seguente:</span><span class="sxs-lookup"><span data-stu-id="a8a85-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="a8a85-183">Quando ci si sposta troppo**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, a seconda del browser, sarà richiesta toodownload o bootstrap.css hello aperto che proviene da un'applicazione Web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="a8a85-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="a8a85-184">È possibile accedere in maniera simile a qualsiasi URL pubblicamente accessibile all'indirizzo **http://*&lt;nomeServizio>*.cloudapp.net/**, direttamente dall'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="a8a85-185">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a85-185">For example:</span></span>

* <span data-ttu-id="a8a85-186">Un file. js dal percorso /Script hello</span><span class="sxs-lookup"><span data-stu-id="a8a85-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="a8a85-187">Qualsiasi file di contenuto da hello /Content percorso</span><span class="sxs-lookup"><span data-stu-id="a8a85-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="a8a85-188">Qualsiasi controller/azione</span><span class="sxs-lookup"><span data-stu-id="a8a85-188">Any controller/action</span></span>
* <span data-ttu-id="a8a85-189">Se la stringa di query hello è abilitata a endpoint della rete CDN, qualsiasi URL con stringhe di query</span><span class="sxs-lookup"><span data-stu-id="a8a85-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="a8a85-190">Infatti, con hello di sopra di configurazione, è possibile ospitare hello intero servizio cloud da  **http://*&lt;cdnName >*.azureedge.net/**. Se passa troppo**http://camservice.azureedge.net/ * *, ottenere il risultato di azione hello da Home/Index.</span><span class="sxs-lookup"><span data-stu-id="a8a85-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="a8a85-191">Ciò significa, tuttavia, che è sempre tooserve una buona idea un intero servizio cloud tramite rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="a8a85-192">Una rete CDN con l'ottimizzazione di recapito statico non necessariamente velocizzare il recapito di asset dinamico che non sono memorizzati nella cache toobe o vengono aggiornati con una frequenza elevata, poiché hello CDN è necessario inserire una nuova versione di asset hello dal server di origine hello molto spesso.</span><span class="sxs-lookup"><span data-stu-id="a8a85-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="a8a85-193">Per questo scenario, è possibile abilitare [accelerazione di sito dinamico](cdn-dynamic-site-acceleration.md) ottimizzazione (DSA) per l'endpoint rete CDN che usa diverse tecniche toospeed le opzioni di distribuzione di asset dinamico non memorizzabile nella cache.</span><span class="sxs-lookup"><span data-stu-id="a8a85-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="a8a85-194">Se si dispone di un sito con una combinazione di contenuto statico e dinamico, è possibile scegliere tooserve contenuto statico dalla rete CDN con un tipo di ottimizzazione statiche (ad esempio recapito web generali) il contenuto dinamico tooserve direttamente dal server di origine hello o tramite una rete CDN endpoint con l'ottimizzazione DSA attivata caso per caso.</span><span class="sxs-lookup"><span data-stu-id="a8a85-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="a8a85-195">toothat fine, è già stato illustrato come i file di contenuto di singoli tooaccess dall'endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="a8a85-196">Illustra come tooserve un'azione del controller specifico tramite un endpoint rete CDN specifico in servire contenuto da azioni del controller tramite la rete CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="a8a85-197">In alternativa Hello è toodetermine quale contenuto tooserve dalla rete CDN di Azure nel caso per caso nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a8a85-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="a8a85-198">toothat fine, è già stato illustrato come i file di contenuto di singoli tooaccess dall'endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="a8a85-199">Si vedrà come tooserve un'azione del controller specifico tramite hello endpoint rete CDN in [Distribuisci il contenuto da azioni del controller tramite la rete CDN Azure](#controller).</span><span class="sxs-lookup"><span data-stu-id="a8a85-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="a8a85-200">Configurare le opzioni di memorizzazione nella cache dei file statici nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="a8a85-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="a8a85-201">Con l'integrazione della rete CDN di Azure nel servizio cloud, è possibile specificare come si desidera statico toobe contenuto memorizzato nella cache in endpoint rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="a8a85-202">toodo, aprire *Web. config* dal ruolo Web del progetto (ad esempio WebRole1) e aggiungere un `<staticContent>` elemento troppo`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="a8a85-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="a8a85-203">Hello XML riportato di seguito consente di configurare tooexpire cache di hello dopo 3 giorni.</span><span class="sxs-lookup"><span data-stu-id="a8a85-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="a8a85-204">Una volta fatto questo, tutti i file statici nel servizio cloud verranno considerato hello stessa regola presenti nella cache della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="a8a85-205">Per un controllo più granulare delle impostazioni della cache, aggiungere un file *Web.config* in una cartella e quindi aggiungervi le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a8a85-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="a8a85-206">Ad esempio, aggiungere un *Web. config* file toohello *\Content* cartella e sostituire hello contenuto con hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="a8a85-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="a8a85-207">Questa impostazione, tutti i file statici dal hello *\Content* toobe cartella memorizzata nella cache per 15 giorni.</span><span class="sxs-lookup"><span data-stu-id="a8a85-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="a8a85-208">Per ulteriori informazioni su come hello tooconfigure `<clientCache>` elemento, vedere [nella Cache del Client &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="a8a85-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="a8a85-209">In [Distribuisci il contenuto da azioni del controller tramite la rete CDN Azure](#controller), apprenderà inoltre come è possibile configurare le impostazioni della cache per i risultati dell'azione controller in hello cache della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="a8a85-210">Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="a8a85-211">Quando si integra un ruolo Web del servizio cloud con rete CDN di Azure, è contenuto tooserve relativamente facile da azioni del controller tramite hello rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="a8a85-212">Individuare il cloud service direttamente tramite rete CDN di Azure (illustrato in precedenza), [Maarten Balliauw](https://twitter.com/maartenballiauw) illustra come toodo con una divertente controller MemeGenerator [riducendo la latenza del sito Web hello con hello rete CDN di Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="a8a85-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="a8a85-213">che viene riprodotto semplicemente in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a8a85-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="a8a85-214">Si supponga che nel servizio cloud desiderato memes toogenerate basata su un'immagine di Chuck Norris giovane (foto da [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) come segue:</span><span class="sxs-lookup"><span data-stu-id="a8a85-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="a8a85-215">Si dispone di una semplice `Index` azione che consente ai clienti di hello superlatives hello toospecify nell'immagine di hello, quindi genera l'errore hello meme dopo INVIO toohello azione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="a8a85-216">Poiché si tratta di Chuck Norris, che ci si aspetta toobecome questa pagina notevolmente più diffusi a livello globale.</span><span class="sxs-lookup"><span data-stu-id="a8a85-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="a8a85-217">È un ottimo esempio di come gestire contenuto semi dinamico con la rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="a8a85-218">Seguire i passaggi di hello sopra toosetup questa azione del controller:</span><span class="sxs-lookup"><span data-stu-id="a8a85-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="a8a85-219">In hello *\Controllers* cartella, creare un nuovo file con estensione cs denominato *MemeGeneratorController.cs* e hello sostituire il contenuto con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="a8a85-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="a8a85-220">Impossibile verificare tooreplace hello nella parte evidenziata con il nome della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="a8a85-221">Fare doppio clic nella predefinito hello `Index()` azione e selezionare **Aggiungi visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="a8a85-222">Accettare le impostazioni di hello riportate di seguito e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8a85-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="a8a85-223">Aprire hello nuovo *Views\MemeGenerator\Index.cshtml* e sostituire il contenuto di hello con hello seguente HTML semplice per l'invio di superlatives hello:</span><span class="sxs-lookup"><span data-stu-id="a8a85-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="a8a85-224">Pubblicare di nuovo servizio cloud hello e passare troppo**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** nel browser.</span><span class="sxs-lookup"><span data-stu-id="a8a85-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="a8a85-225">Quando si inviano i valori del form hello troppo`/MemeGenerator/Index`, hello `Index_Post` metodo di azione restituisce un collegamento di toohello `Show` metodo di azione con l'identificatore dell'input rispettivi hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="a8a85-226">Quando si fa clic sul collegamento hello, raggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a8a85-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="a8a85-227">Se è collegato il debugger locale, si otterrà esperienza di debug regolare hello con un reindirizzamento locale.</span><span class="sxs-lookup"><span data-stu-id="a8a85-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="a8a85-228">Se è in esecuzione nel servizio cloud hello, verrà reindirizzare a:</span><span class="sxs-lookup"><span data-stu-id="a8a85-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="a8a85-229">Che corrisponde a toohello seguente URL di origine all'endpoint della rete CDN:</span><span class="sxs-lookup"><span data-stu-id="a8a85-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="a8a85-230">È quindi possibile utilizzare hello `OutputCacheAttribute` attributo hello `Generate` toospecify metodo come risultato dell'azione hello deve essere memorizzato nella cache, che rispetta rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="a8a85-231">codice Hello seguente specificare una scadenza della cache di 1 ora (3.600 secondi).</span><span class="sxs-lookup"><span data-stu-id="a8a85-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="a8a85-232">Analogamente, può essere utilizzato il contenuto da qualsiasi azione del controller nel servizio cloud tramite la rete CDN di Azure, con l'opzione di memorizzazione nella cache di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="a8a85-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="a8a85-233">Nella sezione successiva hello, vi mostrerò come tooserve hello in bundle e minimizzare gli script e CSS tramite rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="a8a85-234">Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="a8a85-235">Fogli di stile CSS e gli script non vengono modificati spesso e sono candidati ideali per hello cache rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="a8a85-236">Servono hello intero ruolo Web tramite la rete CDN di Azure è toointegrate modo più semplice hello minimizzazione con rete CDN di Azure e aggregazione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="a8a85-237">Tuttavia, come si può non desidera toodo, vi mostrerò come toodo, mantenendo hello desiderato esperienza per sviluppatori di aggregazione di ASP.NET e di riduzione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a85-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="a8a85-238">Ottima esperienza della modalità di debug</span><span class="sxs-lookup"><span data-stu-id="a8a85-238">Great debug mode experience</span></span>
* <span data-ttu-id="a8a85-239">Distribuzione semplificata</span><span class="sxs-lookup"><span data-stu-id="a8a85-239">Streamlined deployment</span></span>
* <span data-ttu-id="a8a85-240">Tooclients immediata di aggiornamenti per gli aggiornamenti di versione script/CSS</span><span class="sxs-lookup"><span data-stu-id="a8a85-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="a8a85-241">Meccanismo di fallback in caso di errore dell'endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="a8a85-242">Riduzione delle modifiche del codice</span><span class="sxs-lookup"><span data-stu-id="a8a85-242">Minimize code modification</span></span>

<span data-ttu-id="a8a85-243">In hello **WebRole1** progetto creato in [integrare un endpoint rete CDN di Azure con il sito Web di Azure e fornire contenuto statico delle pagine Web dalla rete CDN di Azure](#deploy)aprire *App_Start\ BundleConfig.cs* e dare un'occhiata hello `bundles.Add()` chiamate al metodo.</span><span class="sxs-lookup"><span data-stu-id="a8a85-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="a8a85-244">prima di Hello `bundles.Add()` istruzione consente di aggiungere un bundle di script alla directory virtuale hello `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="a8a85-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="a8a85-245">Aprire quindi *Views\Shared\_cshtml* toosee la modalità con cui viene eseguito il rendering di tag di hello script bundle.</span><span class="sxs-lookup"><span data-stu-id="a8a85-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="a8a85-246">Dovrebbe essere in grado di toofind hello successiva riga di codice Razor:</span><span class="sxs-lookup"><span data-stu-id="a8a85-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="a8a85-247">Quando questo codice Razor viene eseguito nel ruolo Web Azure hello, esegue il rendering di un `<script>` tag per hello seguente toohello simile bundle di script:</span><span class="sxs-lookup"><span data-stu-id="a8a85-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="a8a85-248">Tuttavia, quando viene eseguito in Visual Studio digitando `F5`, esegue il rendering di ogni file di script nel bundle hello singolarmente (in caso di hello precedente, solo un file script è in bundle hello):</span><span class="sxs-lookup"><span data-stu-id="a8a85-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="a8a85-249">In questo modo il codice JavaScript hello toodebug nell'ambiente di sviluppo mentre riducendo le connessioni client simultanee (aggregazione) e file di miglioramento delle prestazioni di scaricamento (minimizzazione) nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="a8a85-250">È un toopreserve grande funzionalità con l'integrazione della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="a8a85-251">Inoltre, poiché bundle hello sottoposto a rendering contiene già una stringa di versione generato automaticamente, si desidera tooreplicate che funzionalità hello pertanto quando si aggiorna la versione di jQuery tramite NuGet, possono essere aggiornato sul lato client hello appena possibili.</span><span class="sxs-lookup"><span data-stu-id="a8a85-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="a8a85-252">Eseguire operazioni di hello seguenti toointegration ASP.NET aggregazione e minimizzazione con l'endpoint CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="a8a85-253">In *App_Start\BundleConfig.cs*, modificare hello `bundles.Add()` toouse metodi un altro [costruttore Bundle](http://msdn.microsoft.com/library/jj646464.aspx), uno che specifica un indirizzo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="a8a85-254">toodo hello, sostituire `RegisterBundles` definizione di metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a8a85-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="a8a85-255">Tooreplace assicurarsi di essere `<yourCDNName>` con nome hello della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="a8a85-256">In parole semplici, si imposta `bundles.UseCdn = true` e aggiunta di un bundle di tooeach appositamente URL della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="a8a85-257">Ad esempio, hello primo costruttore nel codice hello:</span><span class="sxs-lookup"><span data-stu-id="a8a85-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="a8a85-258">è hello uguale a:</span><span class="sxs-lookup"><span data-stu-id="a8a85-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="a8a85-259">Questo costruttore indica aggregazione ASP.NET e minimizzazione toorender singoli file di script durante il debug in locale, ma utilizzare hello specificato in questione script hello tooaccess indirizzi della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="a8a85-260">Notare tuttavia due importanti caratteristiche di questo URL della rete CDN definito con precisione:</span><span class="sxs-lookup"><span data-stu-id="a8a85-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="a8a85-261">l'origine per l'URL della rete CDN Hello è `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, che è effettivamente hello directory virtuale del bundle di script hello nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a8a85-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="a8a85-262">Poiché si utilizza il costruttore della rete CDN, hello tag di script della rete CDN per il bundle di hello non contiene la stringa di versione hello generato automaticamente in hello rendering URL.</span><span class="sxs-lookup"><span data-stu-id="a8a85-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="a8a85-263">È necessario generare una stringa di versione univoci manualmente ogni volta che l'aggregazione di script hello tooforce modificato non è disponibile una cache all'interno della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="a8a85-264">AT hello stesso tempo, la stringa di versione univoci deve rimanere costante tramite vita hello di riscontri nella cache di hello distribuzione toomaximize all'interno della rete CDN di Azure dopo aver distribuito il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="a8a85-265">stringa di query v Hello = < w.x.y. z > esegue il pull da *Properties \ AssemblyInfo.cs* nel progetto di ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="a8a85-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="a8a85-266">È possibile disporre di un flusso di lavoro di distribuzione che include l'incremento di versione dell'assembly hello ogni volta che si pubblica tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a8a85-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="a8a85-267">In alternativa, è possibile solo modificare *Properties \ AssemblyInfo.cs* nella stringa di versione del progetto tooautomatically incremento hello ogni volta che si compila, con carattere jolly hello ' *'.</span><span class="sxs-lookup"><span data-stu-id="a8a85-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="a8a85-268">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a85-268">For example:</span></span>
     
        <span data-ttu-id="a8a85-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="a8a85-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="a8a85-270">Altri toostreamline strategia generando una stringa univoca per la durata hello di una distribuzione funzionerà qui.</span><span class="sxs-lookup"><span data-stu-id="a8a85-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="a8a85-271">Ripubblicare hello cloud service e accesso hello la home page.</span><span class="sxs-lookup"><span data-stu-id="a8a85-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="a8a85-272">Il codice HTML per la pagina hello hello di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="a8a85-273">È necessario essere in grado di toosee hello URL CDN sottoposto a rendering, con una stringa di versione univoca ogni volta che si ripubblica servizio cloud tooyour di modifiche.</span><span class="sxs-lookup"><span data-stu-id="a8a85-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="a8a85-274">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a85-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="a8a85-275">In Visual Studio, eseguire il debug del servizio cloud hello in Visual Studio digitando `F5`.,</span><span class="sxs-lookup"><span data-stu-id="a8a85-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="a8a85-276">Il codice HTML per la pagina hello hello di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="a8a85-277">Sarà ancora possibile visualizzare ciascun file di script di cui sia stato eseguito il rendering, in modo che l'esperienza di debug sia coerente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8a85-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="a8a85-278">Meccanismo di fallback per gli URL della rete CDN</span><span class="sxs-lookup"><span data-stu-id="a8a85-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="a8a85-279">Quando l'endpoint rete CDN di Azure non riesce per qualsiasi motivo, è opportuno toobe la pagina Web smart sufficiente tooaccess al server Web di origine come opzione di fallback per il caricamento di JavaScript o Bootstrap hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="a8a85-280">È abbastanza grave toolose immagini nel sito Web a causa di mancata disponibilità tooCDN ma molto più gravi funzionalità della pagina fondamentale toolose fornito da script e fogli di stile.</span><span class="sxs-lookup"><span data-stu-id="a8a85-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="a8a85-281">Hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contiene una proprietà denominata [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) che consente di meccanismo di fallback hello tooconfigure di errore della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a8a85-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="a8a85-282">toouse questa proprietà, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8a85-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="a8a85-283">Nel progetto di ruolo Web, aprire *App_Start\BundleConfig.cs*, cui è stato aggiunto un URL della rete CDN in ogni [costruttore Bundle](http://msdn.microsoft.com/library/jj646464.aspx)e seguenti hello evidenziato cambia tooadd meccanismo di fallback toohello bundle predefinita:</span><span class="sxs-lookup"><span data-stu-id="a8a85-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="a8a85-284">Quando `CdnFallbackExpression` è non null, script, viene inserito nelle tootest hello HTML se è stata caricata bundle hello e, in caso contrario, hello bundle di accedere direttamente dal server Web di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a8a85-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="a8a85-285">Questa proprietà deve toobe set tooa JavaScript espressione che controlla se bundle CDN rispettivi hello è caricata correttamente.</span><span class="sxs-lookup"><span data-stu-id="a8a85-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="a8a85-286">espressione Hello necessari tootest ogni bundle è diverso in base toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="a8a85-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="a8a85-287">Per i pacchetti predefiniti hello precedente:</span><span class="sxs-lookup"><span data-stu-id="a8a85-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="a8a85-288">`window.jquery` viene definito nel file jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="a8a85-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="a8a85-289">`$.validator` viene definito nel file jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="a8a85-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="a8a85-290">`window.Modernizr` viene definito nel file modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="a8a85-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="a8a85-291">`$.fn.modal` viene definito nel file bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="a8a85-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="a8a85-292">È possibile notare che non è stata impostata CdnFallbackExpression per hello `~/Cointent/css` bundle.</span><span class="sxs-lookup"><span data-stu-id="a8a85-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="a8a85-293">In questo modo è attualmente presente una [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) che inserisce un `<script>` tag per hello fallback CSS anziché hello previsto `<link>` tag.</span><span class="sxs-lookup"><span data-stu-id="a8a85-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="a8a85-294">Un'ottima soluzione di [Fallback Style Bundle](https://github.com/EmberConsultingGroup/StyleBundleFallback) è tuttavia offerta da [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="a8a85-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="a8a85-295">soluzione alternativa hello toouse per CSS, creare un nuovo file con estensione cs del progetto di ruolo Web *App_Start* cartella denominata *StyleBundleExtensions.cs*e sostituirne il contenuto con hello [il codice da GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="a8a85-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="a8a85-296">In *App_Start\StyleFundleExtensions.cs*, rinominare il nome del ruolo di hello dello spazio dei nomi tooyour Web (ad esempio **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="a8a85-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="a8a85-297">Tornare indietro troppo`App_Start\BundleConfig.cs` e modificare hello ultima `bundles.Add` istruzione con hello codice evidenziato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8a85-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="a8a85-298">Questo nuovo metodo di estensione Usa hello stesso concetto tooinject script in hello HTML toocheck hello DOM per hello un nome di classe corrispondente, il nome della regola e il valore di regola definita in bundle CSS hello e cade toohello indietro server Web di origine in caso di corrispondenza hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a8a85-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="a8a85-299">Pubblicare nuovamente i servizi cloud di hello e accesso hello home page.</span><span class="sxs-lookup"><span data-stu-id="a8a85-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="a8a85-300">Il codice HTML per la pagina hello hello di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8a85-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="a8a85-301">È necessario trovare script inserito simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8a85-301">You should find injected scripts similar toohello following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="a8a85-302">Si noti che uno script per il bundle CSS hello contiene ancora rimanente e volontariamente hello da hello `CdnFallbackExpression` proprietà nella riga hello:</span><span class="sxs-lookup"><span data-stu-id="a8a85-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="a8a85-303">Ma, poiché hello prima parte hello | | espressione restituirà sempre true (nella riga hello direttamente sopra), la funzione Document hello non verrà mai eseguito.</span><span class="sxs-lookup"><span data-stu-id="a8a85-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="a8a85-304">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a8a85-304">More Information</span></span>
* [<span data-ttu-id="a8a85-305">Panoramica di hello Azure rete CDN (Content Delivery)</span><span class="sxs-lookup"><span data-stu-id="a8a85-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="a8a85-306">Uso della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="a8a85-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="a8a85-307">Creazione di aggregazioni e minimizzazione ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8a85-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
