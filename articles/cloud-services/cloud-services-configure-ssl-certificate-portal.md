---
title: aaaConfigure SSL per un servizio cloud | Documenti Microsoft
description: Informazioni su come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione. Questi esempi utilizzano hello portale di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="569ab-104">Configurazione di SSL per un'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="569ab-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="569ab-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="569ab-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="569ab-106">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="569ab-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="569ab-107">La crittografia Secure Socket Layer (SSL) è il metodo di hello più comunemente usato per proteggere i dati inviati attraverso hello internet.</span><span class="sxs-lookup"><span data-stu-id="569ab-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="569ab-108">Questa attività viene illustrato come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="569ab-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="569ab-109">procedure di Hello in questa attività si applicano i servizi di Cloud tooAzure; per i servizi di App, vedere [questo](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="569ab-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="569ab-110">In questa attività viene usata una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="569ab-110">This task uses a production deployment.</span></span> <span data-ttu-id="569ab-111">Alla fine di hello di questo argomento vengono fornite informazioni sull'utilizzo di una distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="569ab-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="569ab-112">Leggere [questo articolo](cloud-services-how-to-create-deploy-portal.md) se non è stato ancora creato un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="569ab-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="569ab-113">Passaggio 1: Ottenere un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="569ab-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="569ab-114">tooconfigure SSL per un'applicazione, è innanzitutto necessario tooget un certificato SSL firmato da un'autorità di certificazione, una terza parte attendibile che rilascia certificati a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="569ab-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="569ab-115">Se non hai già uno, è necessario tooobtain da una società che vende i certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="569ab-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="569ab-116">certificato Hello deve soddisfare i seguenti requisiti per i certificati SSL in Azure hello:</span><span class="sxs-lookup"><span data-stu-id="569ab-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="569ab-117">certificato di Hello deve contenere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="569ab-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="569ab-118">Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).</span><span class="sxs-lookup"><span data-stu-id="569ab-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="569ab-119">Hello nome soggetto del certificato deve corrispondere il servizio cloud hello di hello dominio utilizzato tooaccess.</span><span class="sxs-lookup"><span data-stu-id="569ab-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="569ab-120">È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per il dominio cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="569ab-121">È necessario acquisire un toouse nome di dominio personalizzato durante l'accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="569ab-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="569ab-122">Quando si richiede un certificato da un'autorità di certificazione, nome del soggetto del certificato hello deve corrispondere tooaccess nome di dominio personalizzato hello l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="569ab-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="569ab-123">Se ad esempio il nome di dominio personalizzato è **contoso.com**, il certificato da richiedere alla CA è ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="569ab-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="569ab-124">certificato di Hello deve utilizzare almeno la crittografia a 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="569ab-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="569ab-125">Per eseguire delle prove, è possibile [creare](cloud-services-certs-create.md) e usare un certificato auto firmato.</span><span class="sxs-lookup"><span data-stu-id="569ab-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="569ab-126">Un certificato autofirmato non viene autenticato tramite un'autorità di certificazione e utilizza dominio cloudapp.net hello come URL del sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="569ab-127">Ad esempio, hello attività seguente utilizza un certificato autofirmato in cui hello è il nome comune (CN) utilizzato nel certificato hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="569ab-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="569ab-128">Successivamente, è necessario includere informazioni sul certificato hello nella definizione del servizio e i file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="569ab-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="569ab-129"><a name="modify"></a></span><span class="sxs-lookup"><span data-stu-id="569ab-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="569ab-130">Passaggio 2: Modificare il file di definizione e configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="569ab-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="569ab-131">L'applicazione deve essere certificato hello toouse configurata e deve essere aggiunto un endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="569ab-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="569ab-132">Di conseguenza, hello definizione del servizio e i file di configurazione del servizio necessario toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="569ab-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="569ab-133">Nell'ambiente di sviluppo, aprire il file di definizione del servizio (CSDEF) hello, aggiungere un **certificati** sezione all'interno di hello **WebRole** sezione e includono le seguenti informazioni hello il certificato (e i certificati intermedi):</span><span class="sxs-lookup"><span data-stu-id="569ab-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="569ab-134">Hello **certificati** sezione definisce il nome di hello di questo certificato, il percorso e nome hello dell'archivio di hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="569ab-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="569ab-135">Autorizzazioni (`permisionLevel` attributi) possa essere tooone set di hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="569ab-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="569ab-136">Valore di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="569ab-136">Permission Value</span></span> | <span data-ttu-id="569ab-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="569ab-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="569ab-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="569ab-138">limitedOrElevated</span></span> |<span data-ttu-id="569ab-139">**(Impostazione predefinita)**  Tutti i processi del ruolo possono accedere la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="569ab-140">elevated</span><span class="sxs-lookup"><span data-stu-id="569ab-140">elevated</span></span> |<span data-ttu-id="569ab-141">Solo i processi con privilegi elevati possono accedere la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="569ab-142">Nel file di definizione del servizio, aggiungere un **InputEndpoint** elemento all'interno di hello **endpoint** sezione tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="569ab-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="569ab-143">Nel file di definizione del servizio, aggiungere un **associazione** elemento all'interno di hello **siti** sezione.</span><span class="sxs-lookup"><span data-stu-id="569ab-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="569ab-144">Questo elemento viene aggiunto un toomap associazione HTTPS del sito tooyour endpoint:</span><span class="sxs-lookup"><span data-stu-id="569ab-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="569ab-145">Una volta completati tutti i file di definizione del servizio hello le modifiche necessarie toohello; Tuttavia, è necessario le informazioni sul certificato per il file di configurazione servizio hello tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="569ab-146">Nel file di configurazione del servizio (CSCFG), ServiceConfiguration.Cloud.cscfg, aggiungere in **Certificates** un valore corrispondente al proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="569ab-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="569ab-147">Hello nell'esempio di codice seguente vengono fornite informazioni dettagliate di hello **certificati** sezione, tranne il valore di identificazione personale hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="569ab-148">(In questo esempio Usa **sha1** per l'algoritmo di identificazione digitale hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="569ab-149">Specifica valore appropriato di hello per l'algoritmo di identificazione personale del certificato).</span><span class="sxs-lookup"><span data-stu-id="569ab-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="569ab-150">Ora che sono stati aggiornati hello servizio definizione e il servizio file di configurazione, la distribuzione per il caricamento tooAzure del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="569ab-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="569ab-151">Se si usa **cspack**, non usare il flag **/generateConfigurationFile**, poiché questo sovrascriverebbe le informazioni del certificato appena inserite.</span><span class="sxs-lookup"><span data-stu-id="569ab-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="569ab-152">Passaggio 3: Caricare un certificato</span><span class="sxs-lookup"><span data-stu-id="569ab-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="569ab-153">Connettersi toohello portale di Azure e...</span><span class="sxs-lookup"><span data-stu-id="569ab-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="569ab-154">In hello **tutte le risorse** sezione di hello portale, selezionare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="569ab-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="569ab-156">Fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="569ab-156">Click **Certificates**.</span></span>

    ![Fare clic sull'icona di certificati hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="569ab-158">Fare clic su **caricare** nella parte superiore di hello dell'area di certificati hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Fare clic sulla voce di menu caricamento hello](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="569ab-160">Fornire hello **File**, **Password**, quindi fare clic su **caricare** nella parte inferiore di hello dell'area di immissione dati hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="569ab-161">Passaggio 4: Connettere l'istanza del ruolo toohello tramite HTTPS</span><span class="sxs-lookup"><span data-stu-id="569ab-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="569ab-162">Ora che la distribuzione sia in esecuzione in Azure, è possibile connettersi tooit tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="569ab-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="569ab-163">Fare clic su hello **URL del sito** tooopen browser web hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Fare clic su hello URL del sito](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="569ab-165">Nel web browser, modificare hello collegamento toouse **https** anziché **http**e quindi visitare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="569ab-166">Se si utilizza un certificato autofirmato, quando si passa l'endpoint HTTPS tooan associato hello autofirmato che venga visualizzato un errore di certificato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="569ab-167">L'utilizzo di un certificato firmato da un'autorità di certificazione attendibile Elimina questo problema. in hello frattempo, è possibile ignorare errore hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="569ab-168">(Un'altra opzione è l'archivio certificati Autorità di certificati attendibili dell'utente di tooadd hello certificato autofirmato toohello).</span><span class="sxs-lookup"><span data-stu-id="569ab-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Anteprima del sito](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="569ab-170">Se si desidera toouse SSL per una distribuzione di gestione temporanea invece di una distribuzione di produzione, è prima necessario toodetermine hello URL utilizzato per la distribuzione di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="569ab-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="569ab-171">Una volta distribuito il servizio cloud, hello URL toohello ambiente di gestione temporanea è determinato dal hello **ID distribuzione** GUID nel formato seguente:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="569ab-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="569ab-172">Creare un certificato con hello comune (CN) uguale toohello basato su GUID URL nome (ad esempio, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="569ab-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="569ab-173">Utilizzare hello tooadd portale hello certificato tooyour di gestione temporanea del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="569ab-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="569ab-174">Aggiungere quindi hello informazioni tooyour estensione CSCFG e CSDEF file di certificato, ricreare il pacchetto dell'applicazione e aggiornare il pacchetto di distribuzione di gestione temporanea toouse hello nuovo.</span><span class="sxs-lookup"><span data-stu-id="569ab-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="569ab-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="569ab-175">Next steps</span></span>
* <span data-ttu-id="569ab-176">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="569ab-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="569ab-177">Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="569ab-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="569ab-178">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="569ab-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="569ab-179">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="569ab-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
