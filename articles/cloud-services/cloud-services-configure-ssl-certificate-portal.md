---
title: Configurare SSL per un servizio cloud | Documentazione Microsoft
description: Informazioni su come specificare un endpoint HTTPS per un ruolo Web e come caricare un certificato SSL al fine di proteggere l'applicazione. Questi esempi utilizzano il portale di Azure.
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="b2f3d-104">Configurazione di SSL per un'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="b2f3d-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2f3d-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b2f3d-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="b2f3d-106">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="b2f3d-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="b2f3d-107">La crittografia SSL (Secure Socket Layer) è il metodo più diffuso per proteggere i dati inviati tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="b2f3d-108">In questa attività comune viene illustrato come specificare un endpoint HTTPS per un ruolo Web e come caricare un certificato SSL al fine di proteggere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="b2f3d-109">Le procedure in questa attività si applicano a Servizi cloud di Azure. Per Servizi app, vedere [questo articolo](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="b2f3d-110">In questa attività viene usata una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-110">This task uses a production deployment.</span></span> <span data-ttu-id="b2f3d-111">Alla fine di questo argomento vengono fornite informazioni sull'uso di una distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="b2f3d-112">Leggere [questo articolo](cloud-services-how-to-create-deploy-portal.md) se non è stato ancora creato un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="b2f3d-113">Passaggio 1: Ottenere un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="b2f3d-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="b2f3d-114">Per configurare SSL per un'applicazione, è necessario prima ottenere un certificato SSL che sia stato firmato da un'Autorità di certificazione (CA), ovvero un ente di terze parti attendibile che rilascia certificati per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="b2f3d-115">Se non se ne dispone già, è necessario ottenerne uno da un rivenditore di certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="b2f3d-116">Il certificato deve soddisfare i requisiti seguenti per i certificati SSL in Azure:</span><span class="sxs-lookup"><span data-stu-id="b2f3d-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="b2f3d-117">Il certificato deve includere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="b2f3d-118">Il certificato deve essere stato creato per lo scambio di chiave, esportabile in un file con estensione pfx (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="b2f3d-119">Il nome del soggetto del certificato deve corrispondere al dominio usato per accedere al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="b2f3d-120">Non è possibile ottenere un certificato SSL da un'Autorità di certificazione (CA) per il dominio cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="b2f3d-121">È necessario acquistare un nome di dominio personalizzato da utilizzare per accedere al servizio.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="b2f3d-122">Quando si richiede un certificato da una CA, il nome del soggetto del certificato deve corrispondere al nome di dominio personalizzato utilizzato per accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="b2f3d-123">Se ad esempio il nome di dominio personalizzato è **contoso.com**, il certificato da richiedere alla CA è ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="b2f3d-124">Per il certificato deve essere usata una crittografia di almeno 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="b2f3d-125">Per eseguire delle prove, è possibile [creare](cloud-services-certs-create.md) e usare un certificato auto firmato.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="b2f3d-126">Un certificato autofirmato non è autenticato tramite una CA e può usare il dominio cloudapp.net come URL del sito Web.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="b2f3d-127">Nell'attività seguente, ad esempio, viene usato un certificato autofirmato in cui il nome comune è **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="b2f3d-128">A questo punto, è necessario includere le informazioni sul certificato nei file di definizione e configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="b2f3d-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="b2f3d-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="b2f3d-130">Passaggio 2: Modificare i file di definizione e configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="b2f3d-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="b2f3d-131">L'applicazione deve essere configurata per utilizzare il certificato ed è necessario aggiungere un endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="b2f3d-132">Di conseguenza, è necessario aggiornare i file di definizione e configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="b2f3d-133">Nell'ambiente di sviluppo aprire il file di definizione del servizio (CSDEF), aggiungere una sezione **Certificates** all'interno della sezione **WebRole** e includere le informazioni seguenti relative al certificato (e ai certificati intermedi):</span><span class="sxs-lookup"><span data-stu-id="b2f3d-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="b2f3d-134">Nella sezione **Certificates** è definito il nome del certificato, il relativo percorso e il nome dell'archivio in cui è situato.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="b2f3d-135">Le autorizzazioni (attributo`permisionLevel`) possono essere impostate su uno dei seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="b2f3d-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="b2f3d-136">Valore di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b2f3d-136">Permission Value</span></span> | <span data-ttu-id="b2f3d-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b2f3d-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b2f3d-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="b2f3d-138">limitedOrElevated</span></span> |<span data-ttu-id="b2f3d-139">**(Predefinito)** Tutti i processi di ruolo possono accedere alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="b2f3d-140">elevated</span><span class="sxs-lookup"><span data-stu-id="b2f3d-140">elevated</span></span> |<span data-ttu-id="b2f3d-141">Solo i processi con autorizzazioni elevate possono accedere alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="b2f3d-142">Nel file csdef aggiungere un elemento **InputEndpoint** all'interno della sezione **Endpoints** per abilitare HTTPS:</span><span class="sxs-lookup"><span data-stu-id="b2f3d-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="b2f3d-143">Nel file di definizione del servizio aggiungere un elemento **Binding** all'interno della sezione **Sites**.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="b2f3d-144">Questo elemento aggiunge un'associazione HTTPS per il mapping dell'endpoint al sito:</span><span class="sxs-lookup"><span data-stu-id="b2f3d-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="b2f3d-145">Tutte le modifiche necessarie al file di definizione del servizio sono state completate, ma è ora necessario aggiungere le informazioni del certificato al file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="b2f3d-146">Nel file di configurazione del servizio (CSCFG), ServiceConfiguration.Cloud.cscfg, aggiungere in **Certificates** un valore corrispondente al proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="b2f3d-147">L'esempio di codice seguente contiene i dettagli della sezione **Certificates**, fatta eccezione per il valore dell'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="b2f3d-148">Questo esempio usa **sha1** come algoritmo di identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="b2f3d-149">Specificare il valore appropriato per l'algoritmo di identificazione personale del certificato in uso.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="b2f3d-150">Ora che i file di definizione e configurazione del servizio sono stati aggiornati, creare il pacchetto della distribuzione per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="b2f3d-151">Se si usa **cspack**, non usare il flag **/generateConfigurationFile**, poiché questo sovrascriverebbe le informazioni del certificato appena inserite.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="b2f3d-152">Passaggio 3: Caricare un certificato</span><span class="sxs-lookup"><span data-stu-id="b2f3d-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="b2f3d-153">Connettersi al portale di Azure e...</span><span class="sxs-lookup"><span data-stu-id="b2f3d-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="b2f3d-154">Nella sezione **Tutte le risorse** del portale selezionare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="b2f3d-156">Fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-156">Click **Certificates**.</span></span>

    ![Fare clic sull'icona dei certificati](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="b2f3d-158">Fare clic su **Carica** nella parte superiore dell'area dei certificati.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Scegliere la voce di menu Carica](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="b2f3d-160">Specificare il **file** e la **password**, quindi fare clic su **Carica** nella parte inferiore dell'area di immissione di dati.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="b2f3d-161">Passaggio 4: Connettersi all'istanza del ruolo usando HTTPS</span><span class="sxs-lookup"><span data-stu-id="b2f3d-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="b2f3d-162">Ora che la distribuzione è in esecuzione in Azure, è possibile connettersi a questa usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="b2f3d-163">Fare clic sull'**URL del sito** per aprire il Web browser.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Fare clic sull'URL del sito](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="b2f3d-165">Nel Web browser modificare il collegamento per usare **https** invece di **http**, quindi accedere alla pagina.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b2f3d-166">Se si usa un certificato autofirmato, quando si passa a un endpoint HTTPS con il certificato autofirmato associato, è possibile che nel browser venga visualizzato un errore del certificato.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="b2f3d-167">L'uso di un certificato firmato da un'Autorità di certificazione attendibile eliminerà il problema. Nel frattempo l'errore può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="b2f3d-168">Un'altra opzione consiste nell'aggiungere il certificato autofirmato nell'archivio certificati dell'Autorità di certificazione attendibile dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Anteprima del sito](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="b2f3d-170">Se si desidera utilizzare SSL per una distribuzione di gestione temporanea anziché di produzione, è necessario innanzitutto determinare l'URL usato per la distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="b2f3d-171">Una volta distribuito il servizio cloud, l'URL dell'ambiente di gestione temporanea è determinato dal GUID **ID distribuzione** nel formato seguente: `https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="b2f3d-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="b2f3d-172">Creare un certificato con il nome comune (CN) uguale all'URL basato su GUID, ad esempio,**328187776e774ceda8fc57609d404462.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="b2f3d-173">Usare il portale per aggiungere il certificato al servizio cloud di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="b2f3d-174">Aggiungere le informazioni del certificato ai file CSDEF e CSCFG, ricreare il pacchetto dell'applicazione e aggiornare la distribuzione di gestione temporanea per usare il nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b2f3d-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="b2f3d-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2f3d-175">Next steps</span></span>
* <span data-ttu-id="b2f3d-176">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="b2f3d-177">Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="b2f3d-178">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="b2f3d-179">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2f3d-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
