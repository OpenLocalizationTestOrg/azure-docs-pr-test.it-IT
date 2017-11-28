---
title: aaaAdd SSL certificato app di Azure App Service tooyour | Documenti Microsoft
description: Informazioni su come tooadd SSL certificato tooyour app del servizio App.
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="53754-103">Acquistare e configurare un certificato SSL per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="53754-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="53754-104">In questa esercitazione, si intende proteggere l'app Web tramite l'acquisto di un certificato SSL per il  **[servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, archiviandolo in modo sicuro nell'[ Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associandolo a un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="53754-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="53754-105">Passaggio 1 - Log in tooAzure</span><span class="sxs-lookup"><span data-stu-id="53754-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="53754-106">Accedi toohello portale di Azure all'indirizzo http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="53754-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="53754-107">Passaggio 2: eseguire un ordine per un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="53754-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="53754-108">È possibile inserire un ordine di certificato SSL creando un nuovo [certificato di servizio App](https://portal.azure.com/#create/Microsoft.SSL) In hello **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="53754-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Creazione del certificato](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="53754-110">Immettere un nome **nome** per il SSL di certificato e immettere hello **nome di dominio**</span><span class="sxs-lookup"><span data-stu-id="53754-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="53754-111">Si tratta di una delle parti principali di hello del processo di acquisto hello.</span><span class="sxs-lookup"><span data-stu-id="53754-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="53754-112">Verificare che tooenter correggere il nome host (dominio personalizzato) che si desidera tooprotect con questo certificato.</span><span class="sxs-lookup"><span data-stu-id="53754-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="53754-113">**NON** aggiungere il nome Host hello con WWW.</span><span class="sxs-lookup"><span data-stu-id="53754-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="53754-114">Selezionare la **Sottoscrizione**, il **Gruppo di risorse** e lo **SKU del certificato**</span><span class="sxs-lookup"><span data-stu-id="53754-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="53754-115">Certificati di servizio App possono essere usati solo da altri servizi di App all'interno di hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="53754-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="53754-116">Passaggio 3: Archivia certificato hello nell'insieme di credenziali chiave di Azure</span><span class="sxs-lookup"><span data-stu-id="53754-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="53754-117">Il [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) è un servizio di Azure che consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="53754-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="53754-118">Una volta hello acquisto di certificati SSL, è necessario tooopen [i certificati di servizio App](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) pannello della risorsa.</span><span class="sxs-lookup"><span data-stu-id="53754-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![inserire un'immagine di toostore pronto in KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="53754-120">Si noterà che lo stato di certificato **"Rilascio in sospeso"** vi sono alcuni altri passaggi toocomplete è necessario prima di iniziare a usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="53754-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="53754-121">Fare clic su **configurazione dei certificati** all'interno di pannello delle proprietà del certificato e fare clic su **passaggio 1: archivio** toostore questo certificato nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="53754-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="53754-122">Da **lo stato dell'insieme di credenziali chiave** pannello, fare clic su **Repository dell'insieme di credenziali chiave** toochoose un toostore insieme di credenziali chiave esistente questo certificato **o creare nuovo insieme di credenziali chiave** toocreate nuova chiave dell'insieme di credenziali all'interno delle stesso gruppo di risorse e di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="53754-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="53754-123">L' Azure Key Vault prevede addebiti minimi per l'archiviazione di questo certificato.</span><span class="sxs-lookup"><span data-stu-id="53754-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="53754-124">Per altre informazioni, vedere **[Prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="53754-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="53754-125">Dopo aver selezionato hello Repository dell'insieme di credenziali chiave toostore questo certificato, hello **archivio** opzione deve visualizzare l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="53754-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![inserimento immagine per la riuscita dell'archiviazione in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="53754-127">Passaggio 4: verificare hello proprietario del dominio</span><span class="sxs-lookup"><span data-stu-id="53754-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="53754-128">Esistono 3 tipi di verifica del dominio supportati da Certificati del servizio app: Domain, Mail, Manual Verification.</span><span class="sxs-lookup"><span data-stu-id="53754-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="53754-129">Questi sono spiegati in dettaglio nell'hello [avanzate sezione](#advanced).</span><span class="sxs-lookup"><span data-stu-id="53754-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="53754-130">Da hello stesso **configurazione dei certificati** blade utilizzata nel passaggio 3, fare clic su **passaggio 2: verificare**.</span><span class="sxs-lookup"><span data-stu-id="53754-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="53754-131">**Verifica del dominio** si tratta di processo più semplice hello **solo se** è  **[acquistato il dominio personalizzato da servizio App di Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="53754-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="53754-132">Fare clic su **verificare** pulsante toocomplete questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="53754-132">Click on **Verify** button toocomplete this step.</span></span>

![inserimento immagine della verifica del dominio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="53754-134">Dopo aver fatto clic **verificare**, utilizzare hello **aggiornamento** pulsante finché hello **verificare** opzione deve visualizzare l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="53754-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![inserimento immagine per la riuscita della verifica in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="53754-136">Passaggio 5: assegnare tooApp certificato del servizio App</span><span class="sxs-lookup"><span data-stu-id="53754-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="53754-137">Prima di eseguire i passaggi di hello in questa sezione, è necessario aver associato un nome di dominio personalizzato con l'app.</span><span class="sxs-lookup"><span data-stu-id="53754-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="53754-138">Per altre informazioni, vedere **[Configurare un nome di dominio personalizzato nel servizio app di Azure.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="53754-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="53754-139">In hello  **[portale di Azure](https://portal.azure.com/)**, fare clic su hello **servizio App** opzione a sinistra di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="53754-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="53754-140">Fare clic sul nome hello di toowhich l'app si desidera tooassign questo certificato.</span><span class="sxs-lookup"><span data-stu-id="53754-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="53754-141">In hello **impostazioni**, fare clic su **i certificati SSL**.</span><span class="sxs-lookup"><span data-stu-id="53754-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="53754-142">Fare clic su **Importa certificato di servizio App** e certificato selezionare hello appena acquistato.</span><span class="sxs-lookup"><span data-stu-id="53754-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![inserimento immagine dell'importazione del certificato](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="53754-144">In hello **associazioni ssl** sezione fare clic su **aggiungere associazioni**, utilizzare hello elenchi a discesa tooselect hello dominio nome toosecure con SSL e hello toouse certificato.</span><span class="sxs-lookup"><span data-stu-id="53754-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="53754-145">È inoltre possibile selezionare se toouse  **[indicazione nome Server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o SSL basato su IP.</span><span class="sxs-lookup"><span data-stu-id="53754-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![inserimento immagine di associazioni SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="53754-147">Fare clic su **aggiungere un Binding** toosave hello modifiche e abilitare SSL.</span><span class="sxs-lookup"><span data-stu-id="53754-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="53754-148">Se si seleziona **SSL basato su IP** e il dominio personalizzato viene configurato usando un record A, è necessario eseguire passaggi aggiuntivi hello.</span><span class="sxs-lookup"><span data-stu-id="53754-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="53754-149">Questi sono spiegati in dettaglio nell'hello [avanzate sezione](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="53754-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="53754-150">A questo punto, si deve essere in grado di toovisit l'app utilizzando `HTTPS://` anziché `HTTP://` tooverify che hello certificato è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="53754-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="53754-151">Passaggio 6: attività di gestione</span><span class="sxs-lookup"><span data-stu-id="53754-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="53754-152">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="53754-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="53754-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53754-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="53754-154">Avanzate</span><span class="sxs-lookup"><span data-stu-id="53754-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="53754-155">Verifica della la proprietà del dominio</span><span class="sxs-lookup"><span data-stu-id="53754-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="53754-156">Esistono altri due tipi di verifica del dominio supportati da Certificati del servizio app: Mail e Manual Verification.</span><span class="sxs-lookup"><span data-stu-id="53754-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="53754-157">Verifica tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="53754-157">Mail Verification</span></span>

<span data-ttu-id="53754-158">Messaggio di verifica è stata inviata toohello che indirizzi di posta elettronica associato al dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="53754-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="53754-159">passaggio di verifica tramite posta elettronica hello toocomplete, aprire il messaggio hello e fare clic sul collegamento di verifica hello.</span><span class="sxs-lookup"><span data-stu-id="53754-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![inserimento immagine della verifica dell'indirizzo di posta elettronica](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="53754-161">Se è necessario posta elettronica di verifica hello tooresend, fare clic su hello **invia di nuovo messaggio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="53754-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="53754-162">Verifica manuale</span><span class="sxs-lookup"><span data-stu-id="53754-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53754-163">Verifica della pagina Web HTML (funziona solo con lo SKU del certificato standard)</span><span class="sxs-lookup"><span data-stu-id="53754-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="53754-164">Creare un file HTML denominato **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="53754-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="53754-165">Contenuto di questo file deve essere hello esatto nome di dominio verifica Token hello.</span><span class="sxs-lookup"><span data-stu-id="53754-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="53754-166">(È possibile copiare il token hello da hello dominio verifica stato pannello)</span><span class="sxs-lookup"><span data-stu-id="53754-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="53754-167">Caricare questo file nella directory principale di hello del server web hello che ospita il dominio`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="53754-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="53754-168">Fare clic su **aggiornamento** stato del certificato hello tooupdate dopo il completamento della verifica.</span><span class="sxs-lookup"><span data-stu-id="53754-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="53754-169">Potrebbe richiedere alcuni minuti per toocomplete di verifica.</span><span class="sxs-lookup"><span data-stu-id="53754-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="53754-170">Verificare in un terminal utilizzando `curl -G http://<domain>/.well-known/pki-validation/starfield.html` risposta hello deve contenere hello `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="53754-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="53754-171">Verifica del record TXT DNS</span><span class="sxs-lookup"><span data-stu-id="53754-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="53754-172">Utilizzando il gestore DNS, creare un record TXT in hello `@` sottodominio con valore uguale toohello Token di verifica del dominio.</span><span class="sxs-lookup"><span data-stu-id="53754-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="53754-173">Fare clic su **"Aggiorna"** tooupdate hello stato del certificato dopo aver completata la verifica.</span><span class="sxs-lookup"><span data-stu-id="53754-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="53754-174">È necessario un record TXT toocreate su `@.<domain>` con valore `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="53754-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="53754-175">Assegnare tooApp certificato del servizio App</span><span class="sxs-lookup"><span data-stu-id="53754-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="53754-176">Se si seleziona **SSL basato su IP** e il dominio personalizzato viene configurato usando un record A, è necessario eseguire passaggi aggiuntivi hello:</span><span class="sxs-lookup"><span data-stu-id="53754-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="53754-177">Dopo aver configurato l'associazione SSL basata su un indirizzo IP, un indirizzo IP dedicato assegnato tooyour app.</span><span class="sxs-lookup"><span data-stu-id="53754-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="53754-178">È possibile trovare questo indirizzo IP su hello **dominio personalizzato** pagina nelle impostazioni dell'app, proprio sopra hello **i nomi host** sezione.</span><span class="sxs-lookup"><span data-stu-id="53754-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="53754-179">È elencato come **Indirizzo IP esterno**</span><span class="sxs-lookup"><span data-stu-id="53754-179">It is listed as **External IP Address**</span></span>

![inserimento immagine di IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="53754-181">Si noti che questo indirizzo IP diverso indirizzo IP virtuale hello utilizzato in precedenza tooconfigure hello un record a per il dominio.</span><span class="sxs-lookup"><span data-stu-id="53754-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="53754-182">Se la configurazione di toouse SSL basato su SNI o non sono configurati toouse SSL, questa voce è elencato alcun indirizzo.</span><span class="sxs-lookup"><span data-stu-id="53754-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="53754-183">Utilizzando gli strumenti di hello forniti dal registrar di nomi di dominio, modificare un record per l'indirizzo IP di toohello toopoint di nome dominio personalizzato dal passaggio precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="53754-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="53754-184">Reimpostazione delle chiavi e sincronizzazione hello certificato</span><span class="sxs-lookup"><span data-stu-id="53754-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="53754-185">Se avrai bisogno di tooRekey il certificato, selezionare **reimpostazione delle chiavi e sincronizzazione** opzione **proprietà certificato** Blade.</span><span class="sxs-lookup"><span data-stu-id="53754-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="53754-186">Fare clic su **reimpostazione** pulsante processo hello tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="53754-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="53754-187">Questo processo può richiedere toocomplete 1-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="53754-187">This process can take 1-10 minutes toocomplete.</span></span>

![inserimento immagine della reimpostazione SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="53754-189">Rigenerazione delle chiavi del certificato esegue il rollup certificato hello con un nuovo certificato rilasciato dall'autorità di certificazione hello.</span><span class="sxs-lookup"><span data-stu-id="53754-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53754-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53754-190">Next Steps</span></span>

* [<span data-ttu-id="53754-191">Aggiungere una Rete per la distribuzione di contenuti (CDN)</span><span class="sxs-lookup"><span data-stu-id="53754-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)