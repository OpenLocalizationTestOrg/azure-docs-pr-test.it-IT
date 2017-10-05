---
title: Integrare un servizio cloud di Azure con la rete CDN di Azure | Documentazione Microsoft
description: Informazioni su come distribuire un servizio cloud che fornisce contenuti da un endpoint della rete CDN di Azure integrato
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
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="e2756-103"><a name="intro"></a> Integrare un servizio cloud con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="e2756-104">È possibile integrare un servizio cloud con la rete CDN di Azure, rendendo disponibile qualsiasi contenuto dalla posizione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e2756-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="e2756-105">Questo approccio offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2756-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="e2756-106">Facile distribuzione e aggiornamento di immagini, script e fogli di stile nelle directory del progetto servizio cloud</span><span class="sxs-lookup"><span data-stu-id="e2756-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="e2756-107">Facile aggiornamento dei pacchetti NuGet nel servizio cloud, come le versioni jQuery o Bootstrap</span><span class="sxs-lookup"><span data-stu-id="e2756-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="e2756-108">Gestione dell'applicazione Web e del contenuto gestito dalla rete CDN dalla stessa interfaccia di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2756-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="e2756-109">Flusso di lavoro di distribuzione unificato per l'applicazione Web e il contenuto gestito dalla rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="e2756-110">Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e2756-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e2756-111">What you will learn</span></span>
<span data-ttu-id="e2756-112">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="e2756-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="e2756-113">Integrare un endpoint della rete CDN di Azure con il servizio cloud e rendere disponibile il contenuto statico nella pagine Web dalla rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="e2756-114">Configurare le impostazioni della cache per il contenuto statico nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="e2756-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="e2756-115">Gestire il contenuto dalle azioni del controller tramite la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="e2756-116">Rendere disponibile contenuto in bundle e minimizzato attraverso la rete CDN di Azure, mantenendo comunque l'esperienza di debug degli script in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2756-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="e2756-117">Configurare il fallback di script e file CSS quando la rete CDN di Azure è offline</span><span class="sxs-lookup"><span data-stu-id="e2756-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="e2756-118">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="e2756-118">What you will build</span></span>
<span data-ttu-id="e2756-119">Verrà distribuito un ruolo Web del servizio cloud usando il modello MVC di ASP.NET predefinito, si aggiungerà il codice per gestire il contenuto da una rete CDN di Azure integrata, ad esempio un'immagine, i risultati dell'azione del controller e i file JavaScript e CSS predefiniti, e si scriverà anche il codice per configurare il meccanismo di fallback per i bundle serviti nel caso in cui la rete CDN non sia in linea.</span><span class="sxs-lookup"><span data-stu-id="e2756-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="e2756-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e2756-120">What you will need</span></span>
<span data-ttu-id="e2756-121">Per completare questa esercitazione, è necessario disporre dei prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2756-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="e2756-122">Un [account Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="e2756-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="e2756-123">Visual Studio 2015 con [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="e2756-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="e2756-124">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="e2756-125">È possibile [aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/): si riceveranno dei crediti da usare per provare i servizi di Azure a pagamento e, anche dopo avere esaurito i crediti, è possibile mantenere l'account per usare i servizi di Azure gratuiti, ad esempio Siti Web.</span><span class="sxs-lookup"><span data-stu-id="e2756-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="e2756-126">È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="e2756-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="e2756-127">Distribuire un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="e2756-127">Deploy a cloud service</span></span>
<span data-ttu-id="e2756-128">In questa sezione verrà distribuito il modello di applicazione MVC di ASP.NET predefinito in Visual Studio 2015 a un ruolo Web del servizio cloud, che verrà quindi integrato con un nuovo endpoint CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="e2756-129">Seguire le istruzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2756-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="e2756-130">In Visual Studio 2015 creare un nuovo servizio cloud di Azure dalla barra dei menu **File > Nuovo > Progetto > Cloud > Servizio cloud di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e2756-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="e2756-131">Assegnargli un nome e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2756-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="e2756-132">Selezionare **Ruolo Web ASP.NET** e fare clic sul pulsante **>**.</span><span class="sxs-lookup"><span data-stu-id="e2756-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="e2756-133">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="e2756-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="e2756-134">Selezionare **MVC** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2756-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="e2756-135">Pubblicare ora questo ruolo Web in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="e2756-136">Fare clic con il pulsante destro del mouse sul progetto servizio cloud e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e2756-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="e2756-137">Se non è stata ancora effettuato l’accesso a Microsoft Azure, fare clic su **Aggiungi un account** nell'elenco a discesa e fare clic sulla voce di menu **Aggiungi un account**.</span><span class="sxs-lookup"><span data-stu-id="e2756-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="e2756-138">Nella pagina di accesso eseguire l'accesso con l'account Microsoft usato per attivare l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="e2756-139">Una volta effettuato l'accesso, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e2756-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="e2756-140">Supponendo che non sia stato creato un servizio cloud né un account di archiviazione, Visual Studio aiuterà a crearli entrambi.</span><span class="sxs-lookup"><span data-stu-id="e2756-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="e2756-141">Nella finestra di dialogo **Crea servizio cloud e account di archiviazione** , digitare il nome del servizio desiderato e selezionare l’area desiderata.</span><span class="sxs-lookup"><span data-stu-id="e2756-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="e2756-142">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e2756-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="e2756-143">Nella pagina Impostazioni di pubblicazione, verificare la configurazione e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e2756-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="e2756-144">Il processo di pubblicazione per i servizi cloud richiede tempi elevati.</span><span class="sxs-lookup"><span data-stu-id="e2756-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="e2756-145">L'opzione Abilita Distribuzione Web per tutti i ruoli Web può velocizzare il debug del servizio cloud fornendo aggiornamenti rapidi (ma temporanei) dei ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="e2756-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="e2756-146">Per altre informazioni su questa opzione, vedere [Pubblicazione di un servizio cloud con gli strumenti di Azure](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2756-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="e2756-147">Quando la finestra **Log attività di Microsoft Azure** indica che lo stato di pubblicazione è **Completato**, è possibile creare un endpoint della rete CDN integrato con il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e2756-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="e2756-148">Se, dopo la pubblicazione, il servizio cloud distribuito mostra una schermata di errore, probabilmente è perché il servizio cloud che è stato distribuito usa un [guest del sistema operativo che non include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="e2756-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="e2756-149">È possibile risolvere il problema da [distribuzione .NET 4.5.2 come attività di avvio](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e2756-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="e2756-150">Creare un nuovo profilo di rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-150">Create a new CDN profile</span></span>
<span data-ttu-id="e2756-151">Un profilo di rete CDN è una raccolta di endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="e2756-152">Ogni profilo contiene uno o più endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="e2756-153">Si consiglia di usare più profili per organizzare gli endpoint della rete CDN tramite il dominio internet, l’applicazione web o altri criteri.</span><span class="sxs-lookup"><span data-stu-id="e2756-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="e2756-154">Se si dispone già di un profilo di rete CDN che si desidera usare per questa esercitazione, passare a [Creare un nuovo endpoint della rete CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="e2756-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="e2756-155">Creare un nuovo endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="e2756-156">**Per creare un nuovo endpoint della rete CDN per l'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="e2756-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="e2756-157">Nel [portale di gestione di Azure](https://portal.azure.com)passare al profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="e2756-158">Lo si potrebbe aver bloccato nel dashboard nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e2756-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="e2756-159">Se così non fosse, è possibile trovarlo facendo clic su **Esplora**, quindi su **Profili rete CDN** e facendo clic sul profilo in cui si prevede di aggiungere l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="e2756-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="e2756-160">Viene visualizzato il pannello del profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-160">The CDN profile blade appears.</span></span>
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. <span data-ttu-id="e2756-162">Fare clic sul pulsante **Aggiungi Endpoint** .</span><span class="sxs-lookup"><span data-stu-id="e2756-162">Click the **Add Endpoint** button.</span></span>
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    <span data-ttu-id="e2756-164">Viene visualizzato il pannello **Aggiungi un endpoint** .</span><span class="sxs-lookup"><span data-stu-id="e2756-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. <span data-ttu-id="e2756-166">Immettere un **Nome** per questo endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="e2756-167">Questo nome verrà usato per accedere alle risorse memorizzate nella cache nel dominio `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="e2756-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="e2756-168">Nell'elenco a discesa **Tipo di origine** , selezionare *Servizio cloud*.</span><span class="sxs-lookup"><span data-stu-id="e2756-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="e2756-169">Nell'elenco a discesa **Nome host di origine** , selezionare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e2756-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="e2756-170">Lasciare le impostazioni predefinite per **Percorso dell'origine**, **Intestazione host di origine** e **Protocollo/Porta dell'origine**.</span><span class="sxs-lookup"><span data-stu-id="e2756-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="e2756-171">È necessario specificare almeno un protocollo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="e2756-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="e2756-172">Per creare il nuovo endpoint, fare clic sul pulsante **Aggiungi** .</span><span class="sxs-lookup"><span data-stu-id="e2756-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="e2756-173">Dopo la creazione, l'endpoint sarà visualizzato in un elenco di endpoint per il profilo.</span><span class="sxs-lookup"><span data-stu-id="e2756-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="e2756-174">Nella visualizzazione elenco sono mostrati gli URL da usare per accedere a contenuti memorizzati nella cache, oltre al dominio di origine.</span><span class="sxs-lookup"><span data-stu-id="e2756-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![Endpoint della rete CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="e2756-176">L'endpoint non sarà immediatamente disponibile per l'uso.</span><span class="sxs-lookup"><span data-stu-id="e2756-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="e2756-177">Ci possono volere fino a 90 minuti per far sì che la registrazione si propaghi attraverso la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="e2756-178">È possibile che gli utenti che provano a usare immediatamente il nome di dominio della rete CDN ricevano un errore con codice di stato 404 fino a quando il contenuto non risulterà disponibile tramite la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="e2756-179">Testare l'endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-179">Test the CDN endpoint</span></span>
<span data-ttu-id="e2756-180">Quando lo stato di pubblicazione è **Completato**, aprire una finestra del browser e passare a **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="e2756-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="e2756-181">Nella configurazione illustrata, questo URL è il seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="e2756-182">che corrisponde all'URL di origine seguente all'endpoint della rete CDN:</span><span class="sxs-lookup"><span data-stu-id="e2756-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="e2756-183">Quando si passa a **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, a seconda del browser, verrà richiesto di scaricare o di aprire il file bootstrap.css disponibile nell'app Web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="e2756-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="e2756-184">È possibile accedere in maniera simile a qualsiasi URL pubblicamente accessibile all'indirizzo **http://*&lt;nomeServizio>*.cloudapp.net/**, direttamente dall'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="e2756-185">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2756-185">For example:</span></span>

* <span data-ttu-id="e2756-186">Un file con estensione js dal percorso /Script</span><span class="sxs-lookup"><span data-stu-id="e2756-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="e2756-187">Qualsiasi file di contenuto dal percorso /Content</span><span class="sxs-lookup"><span data-stu-id="e2756-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="e2756-188">Qualsiasi controller/azione</span><span class="sxs-lookup"><span data-stu-id="e2756-188">Any controller/action</span></span>
* <span data-ttu-id="e2756-189">Se la stringa di query viene abilitata sull'endpoint della rete CDN, qualsiasi URL con stringhe di query</span><span class="sxs-lookup"><span data-stu-id="e2756-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="e2756-190">In effetti, con la configurazione precedente, è possibile ospitare l'intero servizio cloud da **http://*&lt;cdnName>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="e2756-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="e2756-191">Se si passa a **http://camservice.azureedge.net/**, si ottiene il risultato dell'azione da Home/Index.</span><span class="sxs-lookup"><span data-stu-id="e2756-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="e2756-192">Ciò non significa, ad ogni modo, che sia sempre una buona idea rendere disponibile un intero servizio cloud attraverso la rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="e2756-193">Una rete CDN con ottimizzazione della distribuzione statica non velocizza necessariamente la distribuzione degli asset dinamici, che non sono progettati per la memorizzazione nella cache o che vengono aggiornati molto spesso, poiché la rete CDN deve eseguire molto spesso il pull di una nuova versione dell'asset dal server di origine.</span><span class="sxs-lookup"><span data-stu-id="e2756-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="e2756-194">Per questo scenario è possibile abilitare l'ottimizzazione [Accelerazione sito dinamico](cdn-dynamic-site-acceleration.md) nell'endpoint di rete CDN che usa diverse tecniche per velocizzare la distribuzione di asset dinamici non memorizzabili nella cache.</span><span class="sxs-lookup"><span data-stu-id="e2756-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="e2756-195">Se è presente un sito con una combinazione di contenuto statico e dinamico, è possibile scegliere di fornire il contenuto statico dalla rete CDN con un tipo di ottimizzazione statica, ad esempio la distribuzione generale sul Web, e di fornire il contenuto dinamico direttamente dal server di origine oppure tramite un endpoint di rete CDN con l'ottimizzazione Accelerazione sito dinamico attivata in base al caso specifico.</span><span class="sxs-lookup"><span data-stu-id="e2756-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="e2756-196">A tale scopo, si è già visto come accedere ai singoli file di contenuto dall'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="e2756-197">Più avanti, in Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure, verrà illustrato come gestire una specifica azione del controller attraverso l'endpoint di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="e2756-198">L'alternativa consiste nel determinare quale contenuto rendere disponibile dalla rete CDN di Azure, valutando caso per caso nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e2756-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="e2756-199">A tale scopo, si è già visto come accedere ai singoli file di contenuto dall'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="e2756-200">Più avanti verrà illustrato come gestire una specifica azione del controller attraverso l'endpoint CDN in [Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure](#controller).</span><span class="sxs-lookup"><span data-stu-id="e2756-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="e2756-201">Configurare le opzioni di memorizzazione nella cache dei file statici nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="e2756-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="e2756-202">Con l'integrazione della rete CDN di Azure nel servizio cloud è possibile specificare in che modo si vuole memorizzare il contenuto statico nella cache dell'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="e2756-203">A tale scopo, aprire il file *Web.config* dal progetto di ruolo Web (ad esempio, WebRole1) e aggiungere un elemento `<staticContent>` a `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="e2756-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="e2756-204">Il linguaggio XML seguente configura la scadenza della cache entro tre giorni.</span><span class="sxs-lookup"><span data-stu-id="e2756-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="e2756-205">A questo punto, tutti i file statici nel servizio cloud osserveranno la stessa regola nella cache della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="e2756-206">Per un controllo più granulare delle impostazioni della cache, aggiungere un file *Web.config* in una cartella e quindi aggiungervi le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="e2756-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="e2756-207">Ad esempio, aggiungere un file *Web.config* alla cartella *\Content* e sostituire il contenuto con il seguente codice XML:</span><span class="sxs-lookup"><span data-stu-id="e2756-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="e2756-208">Queste impostazioni causano la memorizzazione nella cache di tutti i file statici della cartella *\Content* per 15 giorni.</span><span class="sxs-lookup"><span data-stu-id="e2756-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="e2756-209">Per altre informazioni su come configurare l'elemento `<clientCache>`, vedere [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache) (Cache client).</span><span class="sxs-lookup"><span data-stu-id="e2756-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="e2756-210">Nella sezione [Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure](#controller)verrà illustrato anche come configurare le impostazioni della cache per ottenere i risultati dell'azione del controller nella cache della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="e2756-211">Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="e2756-212">Quando si integra un ruolo Web del servizio cloud nella rete CDN di Azure, è relativamente facile gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="e2756-213">Invece di rendere disponibile il servizio cloud direttamente attraverso la rete CDN (come descritto sopra), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra come farlo con un divertente controller MemeGenerator nel video sulla [riduzione della latenza sul Web con la rete CDN di Azure](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN),</span><span class="sxs-lookup"><span data-stu-id="e2756-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="e2756-214">che viene riprodotto semplicemente in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e2756-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="e2756-215">Si supponga di volere generare nel servizio cloud dei meme basati su un'immagine di un giovane Chuck Norris (foto di [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)), come questa:</span><span class="sxs-lookup"><span data-stu-id="e2756-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="e2756-216">Si usa una semplice azione `Index` che consente ai clienti di specificare i superlativi nell'immagine, quindi genera il meme dopo aver pubblicato nell'azione.</span><span class="sxs-lookup"><span data-stu-id="e2756-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="e2756-217">Poiché si tratta di Chuck Norris, ci si aspetta che questa pagina diventi enormemente popolare in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="e2756-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="e2756-218">È un ottimo esempio di come gestire contenuto semi dinamico con la rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="e2756-219">Seguire i passaggi precedenti per configurare questa azione del controller:</span><span class="sxs-lookup"><span data-stu-id="e2756-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="e2756-220">Nella cartella *\Controllers* creare un nuovo file con estensione cs denominato *MemeGeneratorController.cs* e sostituire il contenuto con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="e2756-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="e2756-221">Assicurarsi di sostituire la parte evidenziata con il nome della propria rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve the debug experience
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
2. <span data-ttu-id="e2756-222">Fare clic con il pulsante destro del mouse sull'azione `Index()` predefinita e selezionare **Aggiungi visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="e2756-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="e2756-223">Accettare le impostazioni di seguito e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e2756-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="e2756-224">Aprire il nuovo file *Views\MemeGenerator\Index.cshtml* e sostituire il contenuto con il semplice HTML seguente per inviare i superlativi:</span><span class="sxs-lookup"><span data-stu-id="e2756-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="e2756-225">Pubblicare nuovamente il servizio cloud e passare a **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** nel browser.</span><span class="sxs-lookup"><span data-stu-id="e2756-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="e2756-226">Quando si inviano i valori del modulo a `/MemeGenerator/Index`, il metodo di azione `Index_Post` restituisce un collegamento al metodo di azione `Show` con il rispettivo identificatore di input.</span><span class="sxs-lookup"><span data-stu-id="e2756-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="e2756-227">Facendo clic sul collegamento si raggiunge il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="e2756-228">Se il debugger locale è collegato, si avrà una normale esperienza di debug con un reindirizzamento locale.</span><span class="sxs-lookup"><span data-stu-id="e2756-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="e2756-229">Se viene eseguito nel servizio cloud, si verrà reindirizzati a:</span><span class="sxs-lookup"><span data-stu-id="e2756-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="e2756-230">che corrisponde all'URL di origine seguente in corrispondenza dell'endpoint della rete CDN:</span><span class="sxs-lookup"><span data-stu-id="e2756-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="e2756-231">Sarà quindi possibile usare l'attributo `OutputCacheAttribute` sul metodo `Generate` per specificare come memorizzare nella cache il risultato dell'azione, che verrà rispettato dalla rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="e2756-232">Il codice seguente specifica la scadenza di una cache entro un'ora (3.600 secondi).</span><span class="sxs-lookup"><span data-stu-id="e2756-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="e2756-233">Analogamente, è possibile rendere disponibile il contenuto da qualsiasi azione del controller nel servizio cloud attraverso la rete CDN di Azure, con l'opzione di memorizzazione nella cache desiderata.</span><span class="sxs-lookup"><span data-stu-id="e2756-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="e2756-234">Nella sezione successiva verrà illustrato come gestire gli script e i file CSS in bundle e minimizzati attraverso la rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="e2756-235">Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="e2756-236">Gli script e i fogli di stile CSS cambiano in maniera non frequente e sono i principali candidati per la cache della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="e2756-237">Il modo più semplice per integrare la creazione di bundle e la minimizzazione con la rete CDN di Azure consiste nel rendere disponibile l'intero ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="e2756-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="e2756-238">Tuttavia, poiché potrebbe non essere auspicabile, verrà illustrato come procedere pur mantenendo l'esperienza desiderata dallo sviluppatore per quanto riguarda la creazione di bundle e la minimizzazione ASP.NET, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2756-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="e2756-239">Ottima esperienza della modalità di debug</span><span class="sxs-lookup"><span data-stu-id="e2756-239">Great debug mode experience</span></span>
* <span data-ttu-id="e2756-240">Distribuzione semplificata</span><span class="sxs-lookup"><span data-stu-id="e2756-240">Streamlined deployment</span></span>
* <span data-ttu-id="e2756-241">Aggiornamenti immediati delle versioni di script/css dei client</span><span class="sxs-lookup"><span data-stu-id="e2756-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="e2756-242">Meccanismo di fallback in caso di errore dell'endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="e2756-243">Riduzione delle modifiche del codice</span><span class="sxs-lookup"><span data-stu-id="e2756-243">Minimize code modification</span></span>

<span data-ttu-id="e2756-244">Nel progetto **WebRole1** creato nella sezione dedicata all'[integrazione di un endpoint della rete CDN di Azure con il sito Web di Azure e alla pubblicazione di contenuto statico nelle pagine Web di CDN di Azure](#deploy) aprire *App_Start\BundleConfig.cs* e osservare le chiamate del metodo `bundles.Add()`.</span><span class="sxs-lookup"><span data-stu-id="e2756-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="e2756-245">La prima istruzione `bundles.Add()` aggiunge un'aggregazione di script alla directory virtuale `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="e2756-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="e2756-246">Aprire quindi *Views\Shared\_Layout.cshtml* per verificare come viene eseguito il rendering del bundle di script.</span><span class="sxs-lookup"><span data-stu-id="e2756-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="e2756-247">Dovrebbe essere possibile trovare la riga di codice Razor seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="e2756-248">Quando questo codice Razor viene eseguito nel ruolo Web di Azure, eseguirà il rendering di un tag `<script>` per il bundle di script in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="e2756-249">Tuttavia, quando il codice viene eseguito in Visual Studio digitando `F5`, comporta il rendering individuale di ogni file di script nell'aggregazione (nel caso sopra citato, l'aggregazione contiene un solo file di script):</span><span class="sxs-lookup"><span data-stu-id="e2756-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="e2756-250">Ciò consente di eseguire il debug del codice JavaScript nell'ambiente di sviluppo e allo stesso tempo di ridurre le connessioni client simultanee (creazione di bundle) e migliorare le prestazioni di download dei file (minimizzazione) in produzione.</span><span class="sxs-lookup"><span data-stu-id="e2756-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="e2756-251">È un'ottima funzionalità da mantenere con l'integrazione nella rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="e2756-252">Per di più, dal momento che il bundle di cui è stato eseguito il rendering contiene una stringa di versione generata automaticamente, è opportuno replicare tale funzionalità in modo che ogni volta che si aggiorna la versione di jQuery attraverso NuGet è possibile aggiornarla sul lato client non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="e2756-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="e2756-253">Attenersi alla procedura seguente per integrare la creazione di bundle e la minimizzazione ASP.NET con l'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="e2756-254">Tornando ad *App_Start\BundleConfig.cs*, modificare i metodi `bundles.Add()` in modo da usare un [costruttore di aggregazioni](http://msdn.microsoft.com/library/jj646464.aspx) diverso, che specifichi un indirizzo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="e2756-255">A questo scopo, sostituire la definizione del metodo `RegisterBundles` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="e2756-256">Assicurarsi di sostituire `<yourCDNName>` con il nome della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="e2756-257">In altri termini, si imposta `bundles.UseCdn = true` e si aggiunge un URL della rete CDN definito con precisione a ogni aggregazione.</span><span class="sxs-lookup"><span data-stu-id="e2756-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="e2756-258">Ad esempio, il primo costruttore nel codice:</span><span class="sxs-lookup"><span data-stu-id="e2756-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="e2756-259">è lo stesso di:</span><span class="sxs-lookup"><span data-stu-id="e2756-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="e2756-260">Questo costruttore comunica alle operazioni di creazione di bundle e minimizzazione ASP.NET di eseguire il rendering dei singoli file di script quando ne viene eseguito il debug a livello locale, ma di usare l'indirizzo della rete CDN specificato per accedere allo script in questione.</span><span class="sxs-lookup"><span data-stu-id="e2756-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="e2756-261">Notare tuttavia due importanti caratteristiche di questo URL della rete CDN definito con precisione:</span><span class="sxs-lookup"><span data-stu-id="e2756-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="e2756-262">L'origine per questo URL della rete CDN è `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, che in realtà è la directory virtuale del bundle di script nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e2756-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="e2756-263">Poiché si sta usando un costruttore CDN, il tag dello script CDN per il bundle non contiene più la stringa di versione generata automaticamente nell'URL di cui è stato eseguito il rendering.</span><span class="sxs-lookup"><span data-stu-id="e2756-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="e2756-264">È necessario generare manualmente una stringa di versione univoca ogni volta che il bundle di script viene modificato per forzare un mancato riscontro nella cache nella rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="e2756-265">Allo stesso tempo, questa stringa di versione univoca deve rimanere costante per tutta la durata della distribuzione per aumentare i riscontri nella cache nella rete CDN di Azure dopo aver distribuito il bundle.</span><span class="sxs-lookup"><span data-stu-id="e2756-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="e2756-266">La stringa di query v=<W.X.Y.Z> effettua il pull da *Properties\AssemblyInfo.cs* nel progetto di ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="e2756-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="e2756-267">È possibile prevedere un flusso di lavoro di distribuzione che includa l'incremento della versione di assembly ogni volta che si pubblica su Azure.</span><span class="sxs-lookup"><span data-stu-id="e2756-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="e2756-268">In alternativa, è possibile modificare solo il file *Properties\AssemblyInfo.cs* nel progetto per incrementare automaticamente la stringa di versione ogni volta che si compila, usando il carattere jolly '*'.</span><span class="sxs-lookup"><span data-stu-id="e2756-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="e2756-269">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2756-269">For example:</span></span>
     
        <span data-ttu-id="e2756-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="e2756-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="e2756-271">Qualsiasi altra strategia volta a semplificare la generazione di una stringa univoca per la durata della distribuzione avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e2756-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="e2756-272">Ripubblicare il servizio cloud e accedere alla home page.</span><span class="sxs-lookup"><span data-stu-id="e2756-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="e2756-273">Visualizzare il codice HTML relativo alla pagina.</span><span class="sxs-lookup"><span data-stu-id="e2756-273">View the HTML code for the page.</span></span> <span data-ttu-id="e2756-274">Dovrebbe essere possibile visualizzare l'URL della rete CDN di cui è stato eseguito il rendering, con una stringa di versione univoca ogni volta che si ripubblicano le modifiche al servizio cloud,</span><span class="sxs-lookup"><span data-stu-id="e2756-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="e2756-275">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2756-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="e2756-276">In Visual Studio eseguire il debug del servizio cloud digitando `F5`.</span><span class="sxs-lookup"><span data-stu-id="e2756-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="e2756-277">Visualizzare il codice HTML relativo alla pagina.</span><span class="sxs-lookup"><span data-stu-id="e2756-277">View the HTML code for the page.</span></span> <span data-ttu-id="e2756-278">Sarà ancora possibile visualizzare ciascun file di script di cui sia stato eseguito il rendering, in modo che l'esperienza di debug sia coerente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2756-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="e2756-279">Meccanismo di fallback per gli URL della rete CDN</span><span class="sxs-lookup"><span data-stu-id="e2756-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="e2756-280">Se si verifica un errore nell'endpoint della rete CDN di Azure per un motivo qualsiasi, è consigliabile configurare l'accesso della pagina Web al server Web di origine come opzione di fallback per il caricamento di JavaScript o Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="e2756-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="e2756-281">Un conto è perdere le immagini nel sito a causa della mancata disponibilità della rete CDN, un altro è perdere funzionalità essenziali della pagina fornite dagli script e dai fogli di stile.</span><span class="sxs-lookup"><span data-stu-id="e2756-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="e2756-282">La classe [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) contiene una proprietà denominata [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) che consente di configurare il meccanismo di fallback per l'errore della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="e2756-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="e2756-283">Per usare questa proprietà, seguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2756-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="e2756-284">Nel progetto di ruolo Web, aprire *App_Start\BundleConfig.cs*, a cui è stato aggiunto un URL della rete CDN a ogni [costruttore di bundle](http://msdn.microsoft.com/library/jj646464.aspx) e apportare le modifiche evidenziate di seguito per aggiungere il meccanismo di fallback ai bundle predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e2756-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
   
    <span data-ttu-id="e2756-285">Quando `CdnFallbackExpression` non è Null, lo script viene inserito nel linguaggio HTML per provare se l'aggregazione è stata caricata correttamente. In caso contrario, accedere all'aggregazione direttamente dal server Web dell'origine.</span><span class="sxs-lookup"><span data-stu-id="e2756-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="e2756-286">Questa proprietà deve essere impostata su un'espressione JavaScript che verifichi se il rispettivo bundle CDN è stato caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e2756-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="e2756-287">L'espressione necessaria per testare ogni bundle differisce in base al contenuto.</span><span class="sxs-lookup"><span data-stu-id="e2756-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="e2756-288">Per i bundle predefiniti sopra riportati:</span><span class="sxs-lookup"><span data-stu-id="e2756-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="e2756-289">`window.jquery` viene definito nel file jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="e2756-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="e2756-290">`$.validator` viene definito nel file jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="e2756-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="e2756-291">`window.Modernizr` viene definito nel file modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="e2756-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="e2756-292">`$.fn.modal` viene definito nel file bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="e2756-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="e2756-293">Come è possibile osservare, non è stata impostata la proprietà CdnFallbackExpression per l'aggregazione `~/Cointent/css`,</span><span class="sxs-lookup"><span data-stu-id="e2756-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="e2756-294">perché attualmente esiste un [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) che inserisce un tag `<script>` per il file CSS di fallback invece del tag `<link>` previsto.</span><span class="sxs-lookup"><span data-stu-id="e2756-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="e2756-295">Un'ottima soluzione di [Fallback Style Bundle](https://github.com/EmberConsultingGroup/StyleBundleFallback) è tuttavia offerta da [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="e2756-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="e2756-296">Per usare la soluzione alternativa per CSS, creare un nuovo file .cs nella cartella *App_Start* del progetto di ruolo Web, denominato *StyleBundleExtensions.cs* e sostituirne il contenuto con il [codice di GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="e2756-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="e2756-297">Nel file *App_Start\StyleFundleExtensions.cs*, rinominare lo spazio dei nomi con il nome del proprio ruolo Web (ad esempio **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="e2756-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="e2756-298">Tornare a `App_Start\BundleConfig.cs` e modificare l’ultima istruzione `bundles.Add` con il seguente codice evidenziato:</span><span class="sxs-lookup"><span data-stu-id="e2756-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="e2756-299">Questo nuovo metodo di estensione si basa sulla stessa idea di inserire lo script nel linguaggio HTML per cercare in DOM il nome di classe, il nome di regola e il valore di regola corrispondenti definiti nel bundle CSS, eseguendo il fallback sul server Web in caso non riesca a trovare la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="e2756-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="e2756-300">Pubblicare di nuovo il servizio cloud e accedere alla home page.</span><span class="sxs-lookup"><span data-stu-id="e2756-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="e2756-301">Visualizzare il codice HTML relativo alla pagina.</span><span class="sxs-lookup"><span data-stu-id="e2756-301">View the HTML code for the page.</span></span> <span data-ttu-id="e2756-302">Gli script inseriti dovrebbero essere simili al seguente:</span><span class="sxs-lookup"><span data-stu-id="e2756-302">You should find injected scripts similar to the following:</span></span>    
   
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

    <span data-ttu-id="e2756-303">Si noti che lo script inserito per l'aggregazione CSS contiene ancora residui della proprietà `CdnFallbackExpression` nella riga:</span><span class="sxs-lookup"><span data-stu-id="e2756-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="e2756-304">Poiché però la prima parte dell'espressione || restituirà sempre true (nella riga subito sopra), la funzione document.write() non verrà mai eseguita.</span><span class="sxs-lookup"><span data-stu-id="e2756-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="e2756-305">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="e2756-305">More Information</span></span>
* [<span data-ttu-id="e2756-306">Panoramica della Rete per la distribuzione di contenuti (CDN) di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="e2756-307">Uso della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="e2756-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="e2756-308">Creazione di aggregazioni e minimizzazione ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e2756-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
