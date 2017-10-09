---
title: aaaConfigure SSL per un servizio cloud (classico) | Documenti Microsoft
description: Informazioni su come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="80aa1-103">Configurazione di SSL per un'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="80aa1-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80aa1-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="80aa1-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="80aa1-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="80aa1-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="80aa1-106">La crittografia Secure Socket Layer (SSL) è il metodo di hello più comunemente usato per proteggere i dati inviati attraverso hello internet.</span><span class="sxs-lookup"><span data-stu-id="80aa1-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="80aa1-107">Questa attività viene illustrato come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80aa1-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="80aa1-108">procedure di Hello in questa attività si applicano i servizi di Cloud tooAzure; per i servizi di App, vedere [questo](../app-service-web/web-sites-configure-ssl-certificate.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="80aa1-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="80aa1-109">In questa attività viene usata una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="80aa1-109">This task uses a production deployment.</span></span> <span data-ttu-id="80aa1-110">Alla fine di hello di questo argomento vengono fornite informazioni sull'utilizzo di una distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="80aa1-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="80aa1-111">Leggere prima [questo articolo](cloud-services-how-to-create-deploy.md) se non è stato ancora creato un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="80aa1-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="80aa1-112">Passaggio 1: Ottenere un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="80aa1-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="80aa1-113">tooconfigure SSL per un'applicazione, è innanzitutto necessario tooget un certificato SSL firmato da un'autorità di certificazione, una terza parte attendibile che rilascia certificati a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="80aa1-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="80aa1-114">Se non hai già uno, è necessario tooobtain da una società che vende i certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="80aa1-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="80aa1-115">certificato Hello deve soddisfare i seguenti requisiti per i certificati SSL in Azure hello:</span><span class="sxs-lookup"><span data-stu-id="80aa1-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="80aa1-116">certificato di Hello deve contenere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="80aa1-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="80aa1-117">Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).</span><span class="sxs-lookup"><span data-stu-id="80aa1-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="80aa1-118">Hello nome soggetto del certificato deve corrispondere il servizio cloud hello di hello dominio utilizzato tooaccess.</span><span class="sxs-lookup"><span data-stu-id="80aa1-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="80aa1-119">È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per il dominio cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="80aa1-120">È necessario acquisire un toouse nome di dominio personalizzato durante l'accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="80aa1-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="80aa1-121">Quando si richiede un certificato da un'autorità di certificazione, nome del soggetto del certificato hello deve corrispondere tooaccess nome di dominio personalizzato hello l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80aa1-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="80aa1-122">Se ad esempio il nome di dominio personalizzato è **contoso.com**, il certificato da richiedere alla CA è ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="80aa1-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="80aa1-123">certificato di Hello deve utilizzare almeno la crittografia a 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="80aa1-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="80aa1-124">Per eseguire delle prove, è possibile [creare](cloud-services-certs-create.md) e usare un certificato auto firmato.</span><span class="sxs-lookup"><span data-stu-id="80aa1-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="80aa1-125">Un certificato autofirmato non viene autenticato tramite un'autorità di certificazione e utilizza dominio cloudapp.net hello come URL del sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="80aa1-126">Ad esempio, hello attività seguente utilizza un certificato autofirmato in cui hello è il nome comune (CN) utilizzato nel certificato hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="80aa1-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="80aa1-127">Successivamente, è necessario includere informazioni sul certificato hello nella definizione del servizio e i file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="80aa1-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="80aa1-128">Passaggio 2: Modificare il file di definizione e configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="80aa1-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="80aa1-129">L'applicazione deve essere certificato hello toouse configurata e deve essere aggiunto un endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80aa1-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="80aa1-130">Di conseguenza, hello definizione del servizio e i file di configurazione del servizio necessario toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="80aa1-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="80aa1-131">Nell'ambiente di sviluppo, aprire il file di definizione del servizio (CSDEF) hello, aggiungere un **certificati** sezione all'interno di hello **WebRole** sezione e includono le seguenti informazioni hello il certificato (e i certificati intermedi):</span><span class="sxs-lookup"><span data-stu-id="80aa1-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="80aa1-132">Hello **certificati** sezione definisce il nome di hello di questo certificato, il percorso e nome hello dell'archivio di hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="80aa1-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="80aa1-133">Autorizzazioni (`permisionLevel` attributi) possa essere tooone set di hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="80aa1-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="80aa1-134">Valore di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="80aa1-134">Permission Value</span></span> | <span data-ttu-id="80aa1-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="80aa1-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="80aa1-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="80aa1-136">limitedOrElevated</span></span> |<span data-ttu-id="80aa1-137">**(Impostazione predefinita)**  Tutti i processi del ruolo possono accedere la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="80aa1-138">elevated</span><span class="sxs-lookup"><span data-stu-id="80aa1-138">elevated</span></span> |<span data-ttu-id="80aa1-139">Solo i processi con privilegi elevati possono accedere la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="80aa1-140">Nel file di definizione del servizio, aggiungere un **InputEndpoint** elemento all'interno di hello **endpoint** sezione tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="80aa1-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="80aa1-141">Nel file di definizione del servizio, aggiungere un **associazione** elemento all'interno di hello **siti** sezione.</span><span class="sxs-lookup"><span data-stu-id="80aa1-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="80aa1-142">In questa sezione consente di aggiungere un toomap associazione HTTPS del sito tooyour endpoint:</span><span class="sxs-lookup"><span data-stu-id="80aa1-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="80aa1-143">Una volta completati tutti i file di definizione del servizio hello le modifiche necessarie toohello, ma è comunque necessario le informazioni sul certificato per il file di configurazione servizio hello tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="80aa1-144">Nel file di configurazione di servizio (CSCFG), ServiceConfiguration, aggiungere un **certificati** sezione all'interno di hello **ruolo** sezione, sostituendo hello valore di identificazione personale di esempio illustrato di seguito con che del certificato:</span><span class="sxs-lookup"><span data-stu-id="80aa1-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="80aa1-145">(hello precedente viene illustrato come utilizzare **sha1** per l'algoritmo di identificazione digitale hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="80aa1-146">Specifica valore appropriato di hello per l'algoritmo di identificazione personale del certificato).</span><span class="sxs-lookup"><span data-stu-id="80aa1-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="80aa1-147">Ora che sono stati aggiornati hello servizio definizione e il servizio file di configurazione, la distribuzione per il caricamento tooAzure del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="80aa1-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="80aa1-148">Se si usa **cspack**, non usare il flag **/generateConfigurationFile**, poiché questo sovrascrive le informazioni del certificato inserite.</span><span class="sxs-lookup"><span data-stu-id="80aa1-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="80aa1-149">Passaggio 3: Caricare un certificato</span><span class="sxs-lookup"><span data-stu-id="80aa1-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="80aa1-150">Il pacchetto di distribuzione è stato aggiornato toouse certificato di hello ed è stato aggiunto un endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80aa1-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="80aa1-151">È ora possibile caricare tooAzure hello di pacchetto e dei certificati con hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="80aa1-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="80aa1-152">Accedi toohello [portale di Azure classico][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="80aa1-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="80aa1-153">Fare clic su **servizi Cloud** nel riquadro di spostamento a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="80aa1-154">Fare clic su servizio cloud hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="80aa1-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="80aa1-155">Fare clic su hello **certificati** scheda.</span><span class="sxs-lookup"><span data-stu-id="80aa1-155">Click hello **Certificates** tab.</span></span>
   
    ![Fare clic sulla scheda certificati hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="80aa1-157">Fare clic su hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="80aa1-157">Click hello **Upload** button.</span></span>
   
    ![Carica](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="80aa1-159">Fornire hello **File**, **Password**, quindi fare clic su **completa** (hello segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="80aa1-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="80aa1-160">Passaggio 4: Connettere l'istanza del ruolo toohello tramite HTTPS</span><span class="sxs-lookup"><span data-stu-id="80aa1-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="80aa1-161">Ora che la distribuzione sia in esecuzione in Azure, è possibile connettersi tooit tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80aa1-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="80aa1-162">In hello portale di Azure classico, selezionare la distribuzione, quindi fare clic sul collegamento hello in **URL del sito**.</span><span class="sxs-lookup"><span data-stu-id="80aa1-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Determinare l'URL del sito][2]
2. <span data-ttu-id="80aa1-164">Nel web browser, modificare hello collegamento toouse **https** anziché **http**e quindi visitare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80aa1-165">Se si utilizza un certificato autofirmato, quando si passa l'endpoint HTTPS tooan associato hello autofirmato che venga visualizzato un errore di certificato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="80aa1-166">L'utilizzo di un certificato firmato da un'autorità di certificazione attendibile Elimina questo problema. in hello frattempo, è possibile ignorare errore hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="80aa1-167">(Un'altra opzione è l'archivio certificati Autorità di certificati attendibili dell'utente di tooadd hello certificato autofirmato toohello).</span><span class="sxs-lookup"><span data-stu-id="80aa1-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Sito Web SSL di esempio][3]

<span data-ttu-id="80aa1-169">Se si desidera toouse SSL per una distribuzione di gestione temporanea invece di una distribuzione di produzione, è necessario innanzitutto toodetermine hello URL utilizzato per la distribuzione di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="80aa1-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="80aa1-170">Distribuire l'ambiente di gestione temporanea toohello di servizio cloud senza includere un certificato o eventuali informazioni del certificato.</span><span class="sxs-lookup"><span data-stu-id="80aa1-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="80aa1-171">Una volta distribuito, è possibile determinare l'URL basato su GUID hello, che è elencato nel portale di Azure classico hello **URL del sito** campo.</span><span class="sxs-lookup"><span data-stu-id="80aa1-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="80aa1-172">Creare un certificato con hello comune (CN) uguale toohello basato su GUID URL nome (ad esempio, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="80aa1-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="80aa1-173">Utilizzare hello Azure tooadd portale classico hello certificato tooyour di gestione temporanea del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="80aa1-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="80aa1-174">Aggiungere quindi hello informazioni tooyour estensione CSCFG e CSDEF file di certificato, ricreare il pacchetto dell'applicazione e aggiornare il pacchetto di distribuzione di gestione temporanea toouse hello nuovo.</span><span class="sxs-lookup"><span data-stu-id="80aa1-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80aa1-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80aa1-175">Next steps</span></span>
* <span data-ttu-id="80aa1-176">[Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="80aa1-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="80aa1-177">Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="80aa1-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="80aa1-178">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="80aa1-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="80aa1-179">[Gestire il servizio cloud](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="80aa1-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
