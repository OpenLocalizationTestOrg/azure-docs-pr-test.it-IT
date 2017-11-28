---
title: aaaBind SSL personalizzato esistente certificato App Web tooAzure | Documenti Microsoft
description: Informazioni tootoobind un'applicazione web di tooyour di certificati SSL personalizzati, back-end dell'app mobile o app per le API in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="09dd4-103">Associare un esistente personalizzato SSL certificato tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="09dd4-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="09dd4-104">Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="09dd4-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="09dd4-105">Questa esercitazione viene illustrato come toobind un SSL personalizzato certificato che si è acquistato da un'autorità di certificazione troppo[App Web di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09dd4-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="09dd4-106">Al termine, sarà in grado di tooaccess app web in endpoint HTTPS hello del dominio DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="09dd4-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![App Web con certificato SSL personalizzato](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="09dd4-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="09dd4-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09dd4-109">Aggiornare il piano tariffario dell'app</span><span class="sxs-lookup"><span data-stu-id="09dd4-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="09dd4-110">Associare il tooApp di certificato SSL del servizio personalizzato</span><span class="sxs-lookup"><span data-stu-id="09dd4-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="09dd4-111">Imporre HTTPS per l'app</span><span class="sxs-lookup"><span data-stu-id="09dd4-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="09dd4-112">Automatizzare l'associazione dei certificati SSL con gli script</span><span class="sxs-lookup"><span data-stu-id="09dd4-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="09dd4-113">Se è necessario un certificato SSL personalizzato tooget, è possibile ottenere uno nel portale di Azure hello direttamente e associarlo tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="09dd4-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="09dd4-114">Seguire hello [esercitazione i certificati di servizio App](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="09dd4-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09dd4-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="09dd4-115">Prerequisites</span></span>

<span data-ttu-id="09dd4-116">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="09dd4-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="09dd4-117">Creare un'app del Servizio app</span><span class="sxs-lookup"><span data-stu-id="09dd4-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="09dd4-118">Eseguire il mapping di un'app web tooyour di nome DNS personalizzata</span><span class="sxs-lookup"><span data-stu-id="09dd4-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="09dd4-119">Acquisire un certificato SSL da un'autorità di certificazione attendibile</span><span class="sxs-lookup"><span data-stu-id="09dd4-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="09dd4-120">Requisiti per il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="09dd4-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="09dd4-121">toouse un certificato nel servizio App, il certificato di hello deve soddisfare hello tutti i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="09dd4-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="09dd4-122">Deve essere firmato da un'autorità di certificazione attendibile</span><span class="sxs-lookup"><span data-stu-id="09dd4-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="09dd4-123">Deve essere esportato come file PFX protetto da password</span><span class="sxs-lookup"><span data-stu-id="09dd4-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="09dd4-124">Deve contenere una chiave privata costituita da almeno 2048 bit</span><span class="sxs-lookup"><span data-stu-id="09dd4-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="09dd4-125">Contiene tutti i certificati intermedi nella catena di certificati hello</span><span class="sxs-lookup"><span data-stu-id="09dd4-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="09dd4-126">Sebbene non siano descritti in questo articolo, i **certificati di crittografia a curva ellittica (ECC)** possono essere usati con il servizio app.</span><span class="sxs-lookup"><span data-stu-id="09dd4-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="09dd4-127">Funziona con un'autorità di certificazione in certificati ECC toocreate passaggi esatti di hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="09dd4-128">Preparare l'app Web</span><span class="sxs-lookup"><span data-stu-id="09dd4-128">Prepare your web app</span></span>

<span data-ttu-id="09dd4-129">toobind un SSL personalizzato certificato tooyour app web, il [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere in hello **base**, **Standard**, o **Premium** livello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="09dd4-130">In questo passaggio assicurarsi che l'app web è in hello supportata piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="09dd4-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="09dd4-131">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="09dd4-131">Log in tooAzure</span></span>

<span data-ttu-id="09dd4-132">Aprire hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09dd4-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="09dd4-133">Passare tooyour web app</span><span class="sxs-lookup"><span data-stu-id="09dd4-133">Navigate tooyour web app</span></span>

<span data-ttu-id="09dd4-134">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Selezionare l'app Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="09dd4-136">Atterraggio nella pagina di gestione di hello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="09dd4-137">Controllo hello piano tariffario</span><span class="sxs-lookup"><span data-stu-id="09dd4-137">Check hello pricing tier</span></span>

<span data-ttu-id="09dd4-138">Nella finestra di navigazione a sinistra di hello della pagina web app, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="09dd4-140">Controllare toomake assicurarsi che l'app web non hello **libero** o **Shared** livello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="09dd4-141">Il livello corrente dell'app Web è evidenziato da una casella blu scuro.</span><span class="sxs-lookup"><span data-stu-id="09dd4-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="09dd4-143">SSL personalizzato non è supportato in hello **libero** o **Shared** livello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="09dd4-144">Se è necessario tooscale backup, seguire i passaggi di hello nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="09dd4-145">In alternativa, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[caricare e associare il certificato SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="09dd4-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="09dd4-146">Passare a un piano di servizio app superiore</span><span class="sxs-lookup"><span data-stu-id="09dd4-146">Scale up your App Service plan</span></span>

<span data-ttu-id="09dd4-147">Selezionare una delle hello **base**, **Standard**, o **Premium** livelli.</span><span class="sxs-lookup"><span data-stu-id="09dd4-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="09dd4-148">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-148">Click **Select**.</span></span>

![Scegliere un piano tariffario](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="09dd4-150">Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="09dd4-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Notifica di passaggio al livello superiore](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="09dd4-152">Associare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="09dd4-152">Bind your SSL certificate</span></span>

<span data-ttu-id="09dd4-153">Si sono pronti tooupload app web tooyour certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="09dd4-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="09dd4-154">Unire i certificati intermedi</span><span class="sxs-lookup"><span data-stu-id="09dd4-154">Merge intermediate certificates</span></span>

<span data-ttu-id="09dd4-155">Se un'autorità di certificazione consente più certificati nella catena di certificati hello, sono necessari i certificati di hello toomerge in ordine.</span><span class="sxs-lookup"><span data-stu-id="09dd4-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="09dd4-156">toodo questa operazione, aprire ogni certificato ricevuto in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="09dd4-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="09dd4-157">Creare un file di certificato unite hello, denominato _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="09dd4-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="09dd4-158">In un editor di testo, copiare il contenuto di hello di ogni certificato in questo file.</span><span class="sxs-lookup"><span data-stu-id="09dd4-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="09dd4-159">ordine di Hello certificati dovrebbe essere simile hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="09dd4-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="09dd4-160">Esporta certificato tooPFX</span><span class="sxs-lookup"><span data-stu-id="09dd4-160">Export certificate tooPFX</span></span>

<span data-ttu-id="09dd4-161">Esportare il certificato SSL unito con la chiave privata hello generata con la richiesta di certificato.</span><span class="sxs-lookup"><span data-stu-id="09dd4-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="09dd4-162">Se è stato usato OpenSSL per generare la richiesta del certificato, è stato creato un file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="09dd4-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="09dd4-163">tooexport tooPFX il certificato, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="09dd4-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="09dd4-164">Sostituire i segnaposto hello  _&lt;file di chiave privata >_ e  _&lt;file di certificato unito >_.</span><span class="sxs-lookup"><span data-stu-id="09dd4-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="09dd4-165">Quando richiesto, definire una password di esportazione.</span><span class="sxs-lookup"><span data-stu-id="09dd4-165">When prompted, define an export password.</span></span> <span data-ttu-id="09dd4-166">Utilizzare questa password quando si carica il SSL certificato tooApp servizio in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="09dd4-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="09dd4-167">Se si utilizza IIS o _Certreq.exe_ toogenerate la richiesta di certificato, installa hello certificato tooyour computer locale, quindi [esportare hello certificato tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="09dd4-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="09dd4-168">Caricare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="09dd4-168">Upload your SSL certificate</span></span>

<span data-ttu-id="09dd4-169">tooupload il certificato SSL, fare clic su **i certificati SSL** nel riquadro di spostamento dell'app web sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="09dd4-170">Fare clic su **Carica certificato**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="09dd4-171">In **File del certificato PFX** selezionare il file PFX.</span><span class="sxs-lookup"><span data-stu-id="09dd4-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="09dd4-172">In **password certificato**, digitare la password hello creato durante l'esportazione dei file PFX hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="09dd4-173">Fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-173">Click **Upload**.</span></span>

![Caricamento del certificato](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="09dd4-175">Quando l'App completato il caricamento del certificato, viene visualizzata in hello **i certificati SSL** pagina.</span><span class="sxs-lookup"><span data-stu-id="09dd4-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificato caricato](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="09dd4-177">Associare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="09dd4-177">Bind your SSL certificate</span></span>

<span data-ttu-id="09dd4-178">In hello **associazioni SSL** fare clic su **aggiungere un'associazione**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="09dd4-179">In hello **aggiungere un Binding SSL** pagina, usare hello elenchi a discesa tooselect hello dominio nome toosecure e toouse certificato hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="09dd4-180">Se è stato caricato il certificato ma non i nomi di dominio hello in hello **Hostname** elenco a discesa, provare ad aggiornare la pagina di browser hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="09dd4-181">In **SSL tipo**, selezionare se toouse  **[indicazione nome Server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o basata su IP SSL.</span><span class="sxs-lookup"><span data-stu-id="09dd4-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="09dd4-182">**SSL basato su SNI**: è possibile aggiungere più associazioni SSL basate su SNI.</span><span class="sxs-lookup"><span data-stu-id="09dd4-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="09dd4-183">Questa opzione consente a più toosecure di certificati SSL più domini in hello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="09dd4-184">La maggior parte dei browser moderni (tra cui Internet Explorer, Chrome, Firefox e Opera) supporta SNI. Per altre informazioni sul supporto dei browser, vedere [Indicazione nome server](http://wikipedia.org/wiki/Server_Name_Indication).</span><span class="sxs-lookup"><span data-stu-id="09dd4-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="09dd4-185">**SSL basato su IP**: è possibile aggiungere una sola associazione SSL basata su IP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="09dd4-186">Questa opzione consente un solo toosecure di certificato SSL di un indirizzo IP pubblico dedicato.</span><span class="sxs-lookup"><span data-stu-id="09dd4-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="09dd4-187">toosecure più domini, è necessario proteggere tali tutti con hello stesso certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="09dd4-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="09dd4-188">Si tratta hello opzione tradizionale per l'associazione SSL.</span><span class="sxs-lookup"><span data-stu-id="09dd4-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="09dd4-189">Fare clic su **Aggiungi l'associazione**.</span><span class="sxs-lookup"><span data-stu-id="09dd4-189">Click **Add Binding**.</span></span>

![Associare un certificato SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="09dd4-191">Quando l'App completato il caricamento del certificato, viene visualizzata in hello **associazioni SSL** sezioni.</span><span class="sxs-lookup"><span data-stu-id="09dd4-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certificato associato tooweb app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="09dd4-193">Eseguire nuovamente il mapping di un record A per IP SSL</span><span class="sxs-lookup"><span data-stu-id="09dd4-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="09dd4-194">Se non si utilizza SSL basato su IP nell'app web, ignorare troppo[Test HTTPS per il dominio personalizzato](#test).</span><span class="sxs-lookup"><span data-stu-id="09dd4-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="09dd4-195">Per impostazione predefinita, l'app Web usa un indirizzo IP pubblico condiviso.</span><span class="sxs-lookup"><span data-stu-id="09dd4-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="09dd4-196">Quando si associa un certificato con SSL basato su IP, il servizio app crea un nuovo indirizzo IP dedicato per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="09dd4-197">Se è stato eseguito il mapping di un'app web di un record tooyour, aggiornare il Registro di sistema di dominio con questo indirizzo IP dedicato, nuovo.</span><span class="sxs-lookup"><span data-stu-id="09dd4-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="09dd4-198">App web **dominio personalizzato** pagina viene aggiornata con l'indirizzo IP dedicato, nuova di hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="09dd4-199">[Copiare questo indirizzo IP](app-service-web-tutorial-custom-domain.md#info), quindi [rimappatura hello un record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="09dd4-200">Testare HTTPS</span><span class="sxs-lookup"><span data-stu-id="09dd4-200">Test HTTPS</span></span>

<span data-ttu-id="09dd4-201">Tutto ciò che ha lasciato toodo ora è toomake assicurarsi che HTTPS funzioni per il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="09dd4-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="09dd4-202">In diversi browser, passare troppo`https://<your.custom.domain>` toosee che fornisca l'app web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="09dd4-204">Se l'app Web visualizza errori di convalida del certificato, è probabile che si stia usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="09dd4-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="09dd4-205">Se non è questo caso di hello, potrebbe trovarsi i certificati intermedi quando si esporta il file PFX del certificato toohello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="09dd4-206">Applicare HTTPS</span><span class="sxs-lookup"><span data-stu-id="09dd4-206">Enforce HTTPS</span></span>

<span data-ttu-id="09dd4-207">Il Servizio app *non* impone l'uso del protocollo HTTPS, pertanto gli utenti possono continuare ad accedere all'app Web usando il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="09dd4-208">tooenforce HTTPS per l'app web, definire una regola di riscrittura in hello _Web. config_ file per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="09dd4-209">Servizio App utilizza questo file, indipendentemente dal framework del linguaggio hello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="09dd4-210">Il reindirizzamento delle richieste è specifico per ogni linguaggio.</span><span class="sxs-lookup"><span data-stu-id="09dd4-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="09dd4-211">ASP.NET MVC è possibile utilizzare hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro anziché una regola di riscrittura hello in _Web. config_.</span><span class="sxs-lookup"><span data-stu-id="09dd4-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="09dd4-212">Gli sviluppatori .NET dovrebbero avere familiarità con questo file.</span><span class="sxs-lookup"><span data-stu-id="09dd4-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="09dd4-213">È in una directory radice della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="09dd4-214">Se invece si sviluppa con PHP, Node.js, Python o Java, è possibile che questo file sia già stato generato da Microsoft nel Servizio app.</span><span class="sxs-lookup"><span data-stu-id="09dd4-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="09dd4-215">Connettere l'endpoint FTP dell'app web tooyour seguendo le istruzioni di hello in [distribuire il servizio App utilizzando FTP/S di tooAzure app](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="09dd4-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="09dd4-216">Questo file sarà disponibile in _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="09dd4-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="09dd4-217">In caso contrario, creare un _Web. config_ file in questa cartella con hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="09dd4-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="09dd4-218">Per un oggetto esistente _Web. config_ file, copiare l'intero hello `<rule>` elemento nel _Web. config_del `configuration/system.webServer/rewrite/rules` elemento.</span><span class="sxs-lookup"><span data-stu-id="09dd4-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="09dd4-219">Se sono presenti altri `<rule>` gli elementi del _Web. config_, sul posto hello copiato `<rule>` elemento prima hello altri `<rule>` elementi.</span><span class="sxs-lookup"><span data-stu-id="09dd4-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="09dd4-220">Questa regola restituisce il protocollo HTTPS toohello un HTTP 301 (reindirizzamento permanente) ogni volta che l'utente hello rende un'app di web tooyour richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="09dd4-221">Ad esempio, viene reindirizzato dal `http://contoso.com` troppo`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="09dd4-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="09dd4-222">Per ulteriori informazioni sul modulo IIS URL Rewrite hello, vedere hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentazione.</span><span class="sxs-lookup"><span data-stu-id="09dd4-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="09dd4-223">Imporre l'uso di HTTPS per le app Web in Linux</span><span class="sxs-lookup"><span data-stu-id="09dd4-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="09dd4-224">Poiché il servizio app in Linux *non* impone l'uso di HTTPS, gli utenti possono continuare ad accedere all'app Web usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="09dd4-225">tooenforce HTTPS per l'app web, definire una regola di riscrittura in hello _. htaccess_ file per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="09dd4-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="09dd4-226">Connettere l'endpoint FTP dell'app web tooyour seguendo le istruzioni di hello in [distribuire il servizio App utilizzando FTP/S di tooAzure app](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="09dd4-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="09dd4-227">In _/home/site/wwwroot_, creare un _. htaccess_ file con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="09dd4-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="09dd4-228">Questa regola restituisce il protocollo HTTPS toohello un HTTP 301 (reindirizzamento permanente) ogni volta che l'utente hello rende un'app di web tooyour richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="09dd4-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="09dd4-229">Ad esempio, viene reindirizzato dal `http://contoso.com` troppo`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="09dd4-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="09dd4-230">Automatizzazione con gli script</span><span class="sxs-lookup"><span data-stu-id="09dd4-230">Automate with scripts</span></span>

<span data-ttu-id="09dd4-231">È possibile automatizzare le associazioni SSL per l'app web con gli script, utilizzando hello [CLI di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09dd4-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="09dd4-232">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="09dd4-232">Azure CLI</span></span>

<span data-ttu-id="09dd4-233">Hello comando seguente carica un file PFX esportato e ottiene l'identificazione personale hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="09dd4-234">Hello seguente comando aggiunge un'associazione SSL basata su SNI, con identificazione personale hello dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="09dd4-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="09dd4-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09dd4-235">Azure PowerShell</span></span>

<span data-ttu-id="09dd4-236">Hello comando seguente carica un file PFX esportato e aggiunge un'associazione basata su SNI SSL.</span><span class="sxs-lookup"><span data-stu-id="09dd4-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="09dd4-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09dd4-237">Next steps</span></span>

<span data-ttu-id="09dd4-238">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="09dd4-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09dd4-239">Aggiornare il piano tariffario dell'app</span><span class="sxs-lookup"><span data-stu-id="09dd4-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="09dd4-240">Associare il tooApp di certificato SSL del servizio personalizzato</span><span class="sxs-lookup"><span data-stu-id="09dd4-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="09dd4-241">Imporre HTTPS per l'app</span><span class="sxs-lookup"><span data-stu-id="09dd4-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="09dd4-242">Automatizzare l'associazione dei certificati SSL con gli script</span><span class="sxs-lookup"><span data-stu-id="09dd4-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="09dd4-243">Spostare toolearn esercitazione successiva toohello come toouse rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="09dd4-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09dd4-244">Aggiungere un tooan rete CDN (Content Delivery) servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="09dd4-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
