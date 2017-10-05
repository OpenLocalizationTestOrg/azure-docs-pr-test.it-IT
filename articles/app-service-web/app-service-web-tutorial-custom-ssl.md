---
title: Associare un certificato SSL personalizzato esistente ad app Web di Azure | Microsoft Docs
description: Informazioni su come associare un certificato SSL personalizzato all'app Web, al back-end di un'app per dispositivi mobili o all'app per le API nel Servizio app di Azure.
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="f1922-103">Associare un certificato SSL personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f1922-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="f1922-104">Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="f1922-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f1922-105">Questa esercitazione illustra come associare alle [app Web di Azure](app-service-web-overview.md) un certificato SSL personalizzato acquistato presso un'autorità di certificazione attendibile.</span><span class="sxs-lookup"><span data-stu-id="f1922-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="f1922-106">Al termine, si sarà in grado di accedere all'app Web dall'endpoint HTTPS del dominio DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f1922-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![App Web con certificato SSL personalizzato](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="f1922-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f1922-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1922-109">Aggiornare il piano tariffario dell'app</span><span class="sxs-lookup"><span data-stu-id="f1922-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="f1922-110">Associare il certificato SSL personalizzato al servizio app</span><span class="sxs-lookup"><span data-stu-id="f1922-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="f1922-111">Imporre HTTPS per l'app</span><span class="sxs-lookup"><span data-stu-id="f1922-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="f1922-112">Automatizzare l'associazione dei certificati SSL con gli script</span><span class="sxs-lookup"><span data-stu-id="f1922-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="f1922-113">Se è necessario usare un certificato SSL personalizzato, è possibile ottenerlo direttamente nel portale di Azure e associarlo all'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="f1922-114">Seguire l'[esercitazione sui certificati del Servizio app](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="f1922-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1922-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1922-115">Prerequisites</span></span>

<span data-ttu-id="f1922-116">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="f1922-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="f1922-117">Creare un'app del Servizio app</span><span class="sxs-lookup"><span data-stu-id="f1922-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="f1922-118">Eseguire il mapping di un nome DNS personalizzato all'app Web</span><span class="sxs-lookup"><span data-stu-id="f1922-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="f1922-119">Acquisire un certificato SSL da un'autorità di certificazione attendibile</span><span class="sxs-lookup"><span data-stu-id="f1922-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="f1922-120">Requisiti per il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="f1922-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="f1922-121">Per poter essere usato nel servizio app, il certificato deve soddisfare tutti i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1922-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="f1922-122">Deve essere firmato da un'autorità di certificazione attendibile</span><span class="sxs-lookup"><span data-stu-id="f1922-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="f1922-123">Deve essere esportato come file PFX protetto da password</span><span class="sxs-lookup"><span data-stu-id="f1922-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="f1922-124">Deve contenere una chiave privata costituita da almeno 2048 bit</span><span class="sxs-lookup"><span data-stu-id="f1922-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="f1922-125">Deve contenere tutti i certificati intermedi nella catena di certificati.</span><span class="sxs-lookup"><span data-stu-id="f1922-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="f1922-126">Sebbene non siano descritti in questo articolo, i **certificati di crittografia a curva ellittica (ECC)** possono essere usati con il servizio app.</span><span class="sxs-lookup"><span data-stu-id="f1922-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="f1922-127">Per informazioni sulla procedura per creare i certificati ECC, rivolgersi all'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="f1922-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="f1922-128">Preparare l'app Web</span><span class="sxs-lookup"><span data-stu-id="f1922-128">Prepare your web app</span></span>

<span data-ttu-id="f1922-129">Per associare un certificato SSL personalizzato all'app Web, il [piano di servizio app](https://azure.microsoft.com/pricing/details/app-service/) in uso deve essere di livello **Basic**, **Standard** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="f1922-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="f1922-130">In questo passaggio si verifica che l'app Web sia supportata dal piano tariffario adeguato.</span><span class="sxs-lookup"><span data-stu-id="f1922-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f1922-131">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="f1922-131">Log in to Azure</span></span>

<span data-ttu-id="f1922-132">Aprire il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1922-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="f1922-133">Accedere all'app Web</span><span class="sxs-lookup"><span data-stu-id="f1922-133">Navigate to your web app</span></span>

<span data-ttu-id="f1922-134">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Selezionare l'app Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="f1922-136">Viene visualizzata la pagina di gestione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="f1922-137">Scegliere il piano tariffario</span><span class="sxs-lookup"><span data-stu-id="f1922-137">Check the pricing tier</span></span>

<span data-ttu-id="f1922-138">Nel riquadro di spostamento a sinistra della pagina dell'app Web scorrere fino alla sezione **Impostazioni** e selezionare **Scala verticalmente (piano di servizio app)**.</span><span class="sxs-lookup"><span data-stu-id="f1922-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="f1922-140">Verificare che l'app Web non sia inclusa nel livello **Gratuito** o **Condiviso**.</span><span class="sxs-lookup"><span data-stu-id="f1922-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="f1922-141">Il livello corrente dell'app Web è evidenziato da una casella blu scuro.</span><span class="sxs-lookup"><span data-stu-id="f1922-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="f1922-143">Il certificato SSL personalizzato non è supportato nel livello **Gratuito** o **Condiviso**.</span><span class="sxs-lookup"><span data-stu-id="f1922-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="f1922-144">Se è necessario passare a un livello superiore, seguire la procedura della sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="f1922-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="f1922-145">In caso contrario, chiudere la pagina **Scegliere il livello di prezzo** e passare a [Caricare il certificato SSL e Associare il certificato SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="f1922-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="f1922-146">Passare a un piano di servizio app superiore</span><span class="sxs-lookup"><span data-stu-id="f1922-146">Scale up your App Service plan</span></span>

<span data-ttu-id="f1922-147">Selezionare uno tra i livelli **Basic**, **Standard** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="f1922-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="f1922-148">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="f1922-148">Click **Select**.</span></span>

![Scegliere un piano tariffario](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="f1922-150">La visualizzazione della notifica seguente indica che l'operazione di passaggio al livello superiore è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f1922-150">When you see the following notification, the scale operation is complete.</span></span>

![Notifica di passaggio al livello superiore](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="f1922-152">Associare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="f1922-152">Bind your SSL certificate</span></span>

<span data-ttu-id="f1922-153">Si è ora pronti a caricare il certificato SSL nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="f1922-154">Unire i certificati intermedi</span><span class="sxs-lookup"><span data-stu-id="f1922-154">Merge intermediate certificates</span></span>

<span data-ttu-id="f1922-155">Se l'autorità di certificazione offre più certificati nella catena di certificati, è necessario unire i certificati nell'ordine.</span><span class="sxs-lookup"><span data-stu-id="f1922-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="f1922-156">A tale scopo, aprire ogni certificato ricevuto in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="f1922-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="f1922-157">Creare un file per il certificato unito denominato _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="f1922-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="f1922-158">In un editor di testo copiare il contenuto di ogni certificato nel file.</span><span class="sxs-lookup"><span data-stu-id="f1922-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="f1922-159">L'ordine dei certificati dovrebbe essere simile al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="f1922-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="f1922-160">Esportare il certificato in un file PFX</span><span class="sxs-lookup"><span data-stu-id="f1922-160">Export certificate to PFX</span></span>

<span data-ttu-id="f1922-161">Esportare il certificato SSL unito con la chiave privata con cui è stata generata la richiesta del certificato.</span><span class="sxs-lookup"><span data-stu-id="f1922-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="f1922-162">Se è stato usato OpenSSL per generare la richiesta del certificato, è stato creato un file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="f1922-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="f1922-163">Per esportare il certificato in un file PFX, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f1922-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="f1922-164">Sostituire i segnaposto _&lt;private-key-file>_ e _&lt;merged-certificate-file>_.</span><span class="sxs-lookup"><span data-stu-id="f1922-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="f1922-165">Quando richiesto, definire una password di esportazione.</span><span class="sxs-lookup"><span data-stu-id="f1922-165">When prompted, define an export password.</span></span> <span data-ttu-id="f1922-166">La password verrà usata in seguito durante il caricamento del certificato SSL nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="f1922-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="f1922-167">se è stato usato IIS o _Certreq.exe_ per generare la richiesta di certificato, installare il certificato nel computer locale e quindi [esportarlo in un file PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="f1922-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="f1922-168">Caricare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="f1922-168">Upload your SSL certificate</span></span>

<span data-ttu-id="f1922-169">Per caricare il certificato SSL, fare clic su **Certificati SSL** nel riquadro di spostamento sinistro dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="f1922-170">Fare clic su **Carica certificato**.</span><span class="sxs-lookup"><span data-stu-id="f1922-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="f1922-171">In **File del certificato PFX** selezionare il file PFX.</span><span class="sxs-lookup"><span data-stu-id="f1922-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="f1922-172">In **Password certificato** digitare la password creata durante l'esportazione del file PFX.</span><span class="sxs-lookup"><span data-stu-id="f1922-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="f1922-173">Fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="f1922-173">Click **Upload**.</span></span>

![Caricamento del certificato](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="f1922-175">Dopo che il Servizio app ha terminato il caricamento del certificato, viene visualizzata la pagina **Certificati SSL**.</span><span class="sxs-lookup"><span data-stu-id="f1922-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificato caricato](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="f1922-177">Associare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="f1922-177">Bind your SSL certificate</span></span>

<span data-ttu-id="f1922-178">Nella sezione **Associazioni SSL** fare clic su **Aggiungi l'associazione**.</span><span class="sxs-lookup"><span data-stu-id="f1922-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="f1922-179">Nel pannello **Aggiungi associazione SSL** usare gli elenchi a discesa per selezionare il nome di dominio da proteggere e il certificato da usare.</span><span class="sxs-lookup"><span data-stu-id="f1922-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="f1922-180">Se il certificato è stato caricato ma i nomi di dominio non appaiono nell'elenco a discesa **Nome host**, provare ad aggiornare la pagina del browser.</span><span class="sxs-lookup"><span data-stu-id="f1922-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="f1922-181">In **Tipo SSL** selezionare se usare l'SSL basato su **[indicazione nome server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** o basato su IP.</span><span class="sxs-lookup"><span data-stu-id="f1922-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="f1922-182">**SSL basato su SNI**: è possibile aggiungere più associazioni SSL basate su SNI.</span><span class="sxs-lookup"><span data-stu-id="f1922-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="f1922-183">Questa opzione consente di usare più certificati SSL per proteggere più domini nello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="f1922-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="f1922-184">La maggior parte dei browser moderni (tra cui Internet Explorer, Chrome, Firefox e Opera) supporta SNI. Per altre informazioni sul supporto dei browser, vedere [Indicazione nome server](http://wikipedia.org/wiki/Server_Name_Indication).</span><span class="sxs-lookup"><span data-stu-id="f1922-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="f1922-185">**SSL basato su IP**: è possibile aggiungere una sola associazione SSL basata su IP.</span><span class="sxs-lookup"><span data-stu-id="f1922-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="f1922-186">Questa opzione consente di usare solo un certificato SSL per proteggere un indirizzo IP pubblico dedicato.</span><span class="sxs-lookup"><span data-stu-id="f1922-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="f1922-187">Per proteggere più domini, è necessario proteggerli tutti usando lo stesso certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="f1922-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="f1922-188">Questa è l'opzione tradizionale per l'associazione SSL.</span><span class="sxs-lookup"><span data-stu-id="f1922-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="f1922-189">Fare clic su **Aggiungi l'associazione**.</span><span class="sxs-lookup"><span data-stu-id="f1922-189">Click **Add Binding**.</span></span>

![Associare un certificato SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="f1922-191">Al termine del caricamento da parte del Servizio app, il certificato viene visualizzato nella sezione **Certificati SSL**.</span><span class="sxs-lookup"><span data-stu-id="f1922-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificato associato all'app Web](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="f1922-193">Eseguire nuovamente il mapping di un record A per IP SSL</span><span class="sxs-lookup"><span data-stu-id="f1922-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="f1922-194">Se non si usa l'SSL basato su IP nell'app Web, passare direttamente alla sezione [Testare HTTPS per il dominio personalizzato](#test).</span><span class="sxs-lookup"><span data-stu-id="f1922-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="f1922-195">Per impostazione predefinita, l'app Web usa un indirizzo IP pubblico condiviso.</span><span class="sxs-lookup"><span data-stu-id="f1922-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="f1922-196">Quando si associa un certificato con SSL basato su IP, il servizio app crea un nuovo indirizzo IP dedicato per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="f1922-197">Se è stato eseguito il mapping di un record A all'app Web, aggiornare il Registro di sistema del dominio con questo nuovo indirizzo IP dedicato.</span><span class="sxs-lookup"><span data-stu-id="f1922-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="f1922-198">La pagina **Dominio personalizzato** dell'app Web viene aggiornata con il nuovo indirizzo IP dedicato.</span><span class="sxs-lookup"><span data-stu-id="f1922-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="f1922-199">[Copiare questo indirizzo IP](app-service-web-tutorial-custom-domain.md#info), quindi [eseguire nuovamente il mapping del record A](app-service-web-tutorial-custom-domain.md#map-an-a-record) a questo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="f1922-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="f1922-200">Testare HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1922-200">Test HTTPS</span></span>

<span data-ttu-id="f1922-201">A questo punto, non resta che assicurarsi che HTTPS funzioni correttamente per il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f1922-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="f1922-202">In diversi browser passare a `https://<your.custom.domain>` per verificare che l'app Web sia gestita.</span><span class="sxs-lookup"><span data-stu-id="f1922-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="f1922-204">Se l'app Web visualizza errori di convalida del certificato, è probabile che si stia usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="f1922-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="f1922-205">Se non è questo il motivo, è possibile che siano stati esclusi i certificati intermedi durante l'esportazione del certificato nel file PFX.</span><span class="sxs-lookup"><span data-stu-id="f1922-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="f1922-206">Applicare HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1922-206">Enforce HTTPS</span></span>

<span data-ttu-id="f1922-207">Il Servizio app *non* impone l'uso del protocollo HTTPS, pertanto gli utenti possono continuare ad accedere all'app Web usando il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1922-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="f1922-208">Per imporre l'uso di HTTPS per l'app Web, definire una regola di riscrittura nel file _web.config_ dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="f1922-209">Il Servizio app usa questo file indipendentemente dal framework del linguaggio dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="f1922-210">Il reindirizzamento delle richieste è specifico per ogni linguaggio.</span><span class="sxs-lookup"><span data-stu-id="f1922-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="f1922-211">ASP.NET MVC può usare il filtro [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) anziché la regola di riscrittura in _web.config_.</span><span class="sxs-lookup"><span data-stu-id="f1922-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="f1922-212">Gli sviluppatori .NET dovrebbero avere familiarità con questo file.</span><span class="sxs-lookup"><span data-stu-id="f1922-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="f1922-213">Il file è disponibile nella radice della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f1922-213">It is in the root of your solution.</span></span>

<span data-ttu-id="f1922-214">Se invece si sviluppa con PHP, Node.js, Python o Java, è possibile che questo file sia già stato generato da Microsoft nel Servizio app.</span><span class="sxs-lookup"><span data-stu-id="f1922-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="f1922-215">Connettersi all'endpoint FTP dell'app Web seguendo le istruzioni fornite in [Distribuire l'app nel Servizio app di Azure usando FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="f1922-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="f1922-216">Questo file sarà disponibile in _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="f1922-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="f1922-217">Se non è disponibile, creare un file _web.config_ in questa cartella usando il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="f1922-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="f1922-218">Per un file _web.config_ esistente, copiare l'intero elemento `<rule>` nell'elemento `configuration/system.webServer/rewrite/rules` del file _web.config_.</span><span class="sxs-lookup"><span data-stu-id="f1922-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="f1922-219">Se sono presenti altri elementi `<rule>` nel file _web.config_, inserire l'elemento `<rule>` copiato prima degli altri elementi `<rule>`.</span><span class="sxs-lookup"><span data-stu-id="f1922-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="f1922-220">Questa regola restituisce un errore HTTP 301 (reindirizzamento permanente) al protocollo HTTPS ogni volta che l'utente effettua una richiesta HTTP all'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="f1922-221">Reindirizza ad esempio da `http://contoso.com` a `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="f1922-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="f1922-222">Per altre informazioni sul modulo IIS Riscrittura URL, vedere la documentazione [Riscrittura URL](http://www.iis.net/downloads/microsoft/url-rewrite) .</span><span class="sxs-lookup"><span data-stu-id="f1922-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="f1922-223">Imporre l'uso di HTTPS per le app Web in Linux</span><span class="sxs-lookup"><span data-stu-id="f1922-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="f1922-224">Poiché il servizio app in Linux *non* impone l'uso di HTTPS, gli utenti possono continuare ad accedere all'app Web usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1922-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="f1922-225">Per imporre l'uso di HTTPS per l'app Web, definire una regola di riscrittura nel file _.htaccess_ dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="f1922-226">Connettersi all'endpoint FTP dell'app Web seguendo le istruzioni fornite in [Distribuire l'app nel Servizio app di Azure usando FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="f1922-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="f1922-227">In _/home/site/wwwroot_ creare un file _.htaccess_ con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f1922-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="f1922-228">Questa regola restituisce un errore HTTP 301 (reindirizzamento permanente) al protocollo HTTPS ogni volta che l'utente effettua una richiesta HTTP all'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1922-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="f1922-229">Reindirizza ad esempio da `http://contoso.com` a `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="f1922-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="f1922-230">Automatizzare con gli script</span><span class="sxs-lookup"><span data-stu-id="f1922-230">Automate with scripts</span></span>

<span data-ttu-id="f1922-231">È possibile automatizzare le associazioni SSL per l'app Web con gli script usando l'[interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1922-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="f1922-232">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f1922-232">Azure CLI</span></span>

<span data-ttu-id="f1922-233">Il comando seguente carica un file PFX esportato e ottiene l'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="f1922-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="f1922-234">Il comando seguente aggiunge un'associazione SSL basata su SNI, usando l'identificazione personale ottenuta con il comando precedente.</span><span class="sxs-lookup"><span data-stu-id="f1922-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="f1922-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1922-235">Azure PowerShell</span></span>

<span data-ttu-id="f1922-236">Il comando seguente carica un file PFX esportato e aggiunge un'associazione SSL basata su SNI.</span><span class="sxs-lookup"><span data-stu-id="f1922-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="f1922-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1922-237">Next steps</span></span>

<span data-ttu-id="f1922-238">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="f1922-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1922-239">Aggiornare il piano tariffario dell'app</span><span class="sxs-lookup"><span data-stu-id="f1922-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="f1922-240">Associare il certificato SSL personalizzato al servizio app</span><span class="sxs-lookup"><span data-stu-id="f1922-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="f1922-241">Imporre HTTPS per l'app</span><span class="sxs-lookup"><span data-stu-id="f1922-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="f1922-242">Automatizzare l'associazione dei certificati SSL con gli script</span><span class="sxs-lookup"><span data-stu-id="f1922-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="f1922-243">Passare all'esercitazione successiva per imparare a usare la rete di distribuzione dei contenuti di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1922-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1922-244">Aggiungere una rete per la distribuzione di contenuti (CDN) a un servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="f1922-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
