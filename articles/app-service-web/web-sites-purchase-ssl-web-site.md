---
title: Aggiungere un certificato SSL all'app del Servizio app di Azure | Documentazione Microsoft
description: Informazioni su come aggiungere un certificato SSL all'app del Servizio app.
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="dc121-103">Acquistare e configurare un certificato SSL per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="dc121-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="dc121-104">In questa esercitazione, si intende proteggere l'app Web tramite l'acquisto di un certificato SSL per il  **[servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, archiviandolo in modo sicuro nell'[ Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associandolo a un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc121-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="dc121-105">Passaggio 1: Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="dc121-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="dc121-106">Accedere al portale di Azure all'indirizzo http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="dc121-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="dc121-107">Passaggio 2: eseguire un ordine per un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="dc121-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="dc121-108">È possibile ordinare un certificato SSL creando un nuovo [certificato di servizio App](https://portal.azure.com/#create/Microsoft.SSL) nel **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc121-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Creazione del certificato](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="dc121-110">Immettere un **nome descrittivo** per il certificato SSL e immettere il **nome del dominio**</span><span class="sxs-lookup"><span data-stu-id="dc121-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-111">Questa è una delle parti più importanti del processo di acquisto.</span><span class="sxs-lookup"><span data-stu-id="dc121-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="dc121-112">Assicurarsi di immettere il nome host corretto (dominio personalizzato) che si desidera proteggere con il certificato.</span><span class="sxs-lookup"><span data-stu-id="dc121-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="dc121-113">**NON** aggiungere WWW al nome host.</span><span class="sxs-lookup"><span data-stu-id="dc121-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="dc121-114">Selezionare la **Sottoscrizione**, il **Gruppo di risorse** e lo **SKU del certificato**</span><span class="sxs-lookup"><span data-stu-id="dc121-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="dc121-115">I certificati del servizio App possono essere usati solo da altri servizi App nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dc121-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="dc121-116">Passaggio 3: archiviare il certificato nell'Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc121-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-117">Il [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) è un servizio di Azure che consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="dc121-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="dc121-118">Dopo aver completato l'acquisto del certificato SSL, è necessario aprire il pannello delle risorse [Certificati del servizio app](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders).</span><span class="sxs-lookup"><span data-stu-id="dc121-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![inserimento immagine stato di pronto per l'archiviazione in un insieme di credenziali delle chiavi](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="dc121-120">Si noterà che lo stato del certificato è **"Rilascio in sospeso"** dal momento che sono previsti pochi altri passaggi da completare prima di iniziare a usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="dc121-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="dc121-121">Fare clic su **Configurazione del certificato** nel pannello Proprietà del certificato e fare clic su **Passaggio 1: archiviare** per archiviare il certificato nell'Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dc121-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="dc121-122">Nel pannello **Stato del Key Vault** fare clic su **Archivio del Key Vault** per scegliere un insieme esistente in cui archiviare il certificato **O Crea nuovo Key Vault** per creare un nuovo insieme all'interno della stessa sottoscrizione e dello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="dc121-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-123">L' Azure Key Vault prevede addebiti minimi per l'archiviazione di questo certificato.</span><span class="sxs-lookup"><span data-stu-id="dc121-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="dc121-124">Per altre informazioni, vedere **[Prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="dc121-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="dc121-125">Dopo aver selezionato l'archivio del Key Vault in cui archiviare il certificato, selezionare il pulsante **Archivia**.</span><span class="sxs-lookup"><span data-stu-id="dc121-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![inserimento immagine per la riuscita dell'archiviazione in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="dc121-127">Passaggio 4: verificare la proprietà del dominio</span><span class="sxs-lookup"><span data-stu-id="dc121-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-128">Esistono 3 tipi di verifica del dominio supportati da Certificati del servizio app: Domain, Mail, Manual Verification.</span><span class="sxs-lookup"><span data-stu-id="dc121-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="dc121-129">Sono illustrati più dettagliatamente nella [sezione Avanzate](#advanced).</span><span class="sxs-lookup"><span data-stu-id="dc121-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="dc121-130">Dallo stesso pannello **configurazione certificato** utilizzato nel passaggio 3, fare clic su **Passaggio 2: verificare**.</span><span class="sxs-lookup"><span data-stu-id="dc121-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="dc121-131">La **verifica del dominio** è il processo più semplice **SOLO IN CASO DI**acquisto **[del dominio personalizzato dal Servizio app di Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="dc121-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="dc121-132">Fare clic sul pulsante **Verifica** per completare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="dc121-132">Click on **Verify** button to complete this step.</span></span>

![inserimento immagine della verifica del dominio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="dc121-134">Dopo aver fatto clic su **Verifica**, utilizzare il pulsante **Aggiorna** fino a quando l'opzione **Verifica** non avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="dc121-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![inserimento immagine per la riuscita della verifica in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="dc121-136">Passaggio 5: Assegnare il certificato all'app del servizio app</span><span class="sxs-lookup"><span data-stu-id="dc121-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-137">Prima di eseguire la procedura inclusa in questa sezione, è necessario avere associato un nome di dominio personalizzato all'app.</span><span class="sxs-lookup"><span data-stu-id="dc121-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="dc121-138">Per altre informazioni, vedere **[Configurare un nome di dominio personalizzato nel servizio app di Azure.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="dc121-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="dc121-139">Nel **[portale di Azure](https://portal.azure.com/)** fare clic sull'opzione **Servizio app** a sinistra nella pagina.</span><span class="sxs-lookup"><span data-stu-id="dc121-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="dc121-140">Fare clic sul nome dell'app a cui si desidera assegnare il certificato.</span><span class="sxs-lookup"><span data-stu-id="dc121-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="dc121-141">In **Impostazioni** fare clic su **Certificati SSL**.</span><span class="sxs-lookup"><span data-stu-id="dc121-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="dc121-142">Fare clic su **Importa il certificato di servizio app** e selezionare il certificato appena acquistato.</span><span class="sxs-lookup"><span data-stu-id="dc121-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![inserimento immagine dell'importazione del certificato](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="dc121-144">Nella sezione **associazione SSL** fare clic su **Aggiungi associazioni** e usare gli elenchi a discesa per selezionare il nome di dominio da proteggere con SSL e il certificato da usare.</span><span class="sxs-lookup"><span data-stu-id="dc121-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="dc121-145">È possibile anche stabilire se usare il metodo SSL basato su **[Indicazione nome server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** o su IP.</span><span class="sxs-lookup"><span data-stu-id="dc121-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![inserimento immagine di associazioni SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="dc121-147">Fare clic su **Aggiungi l'associazione** per salvare le modifiche e abilitare SSL.</span><span class="sxs-lookup"><span data-stu-id="dc121-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="dc121-148">Se è stata selezionata l'opzione **SSL basato su IP** e il dominio personalizzato è stato configurato usando un record A, sarà necessario eseguire i passaggi aggiuntivi seguenti.</span><span class="sxs-lookup"><span data-stu-id="dc121-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="dc121-149">Sono illustrati più dettagliatamente nella [sezione Avanzata](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="dc121-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="dc121-150">A questo punto si dovrebbe poter andare all'app usando `HTTPS://` anziché `HTTP://` per verificare che il certificato sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="dc121-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="dc121-151">Passaggio 6: attività di gestione</span><span class="sxs-lookup"><span data-stu-id="dc121-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="dc121-152">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dc121-152">Azure CLI</span></span>

<span data-ttu-id="dc121-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associare un certificato SSL personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="dc121-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="dc121-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc121-154">PowerShell</span></span>

<span data-ttu-id="dc121-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Associare un certificato SSL personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="dc121-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="dc121-156">Avanzate</span><span class="sxs-lookup"><span data-stu-id="dc121-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="dc121-157">Verifica della la proprietà del dominio</span><span class="sxs-lookup"><span data-stu-id="dc121-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="dc121-158">Esistono altri due tipi di verifica del dominio supportati da Certificati del servizio app: Mail e Manual Verification.</span><span class="sxs-lookup"><span data-stu-id="dc121-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="dc121-159">Verifica tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="dc121-159">Mail Verification</span></span>

<span data-ttu-id="dc121-160">Un messaggio di posta elettronica di verifica è già stato inviato agli indirizzi di posta elettronica associati al dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc121-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="dc121-161">Per completare il passaggio di verifica tramite posta elettronica, aprire la posta elettronica e fare clic sul collegamento di verifica.</span><span class="sxs-lookup"><span data-stu-id="dc121-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![inserimento immagine della verifica dell'indirizzo di posta elettronica](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="dc121-163">Se è necessario un nuovo invio del messaggio di verifica, fare clic sul pulsante **Invia di nuovo il messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="dc121-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="dc121-164">Verifica manuale</span><span class="sxs-lookup"><span data-stu-id="dc121-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc121-165">Verifica della pagina Web HTML (funziona solo con lo SKU del certificato standard)</span><span class="sxs-lookup"><span data-stu-id="dc121-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="dc121-166">Creare un file HTML denominato **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="dc121-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="dc121-167">Il contenuto di questo file deve corrispondere esattamente al nome del token di verifica del dominio.</span><span class="sxs-lookup"><span data-stu-id="dc121-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="dc121-168">È possibile copiare il token dal pannello dello Stato di verifica del dominio.</span><span class="sxs-lookup"><span data-stu-id="dc121-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="dc121-169">Caricare il file nella radice del server Web che ospita il dominio `/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="dc121-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="dc121-170">Fare clic su **Aggiorna** per aggiornare lo stato del certificato dopo aver completato la verifica.</span><span class="sxs-lookup"><span data-stu-id="dc121-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="dc121-171">Il completamento della verifica potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="dc121-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="dc121-172">Verificare in un terminale mediante `curl -G http://<domain>/.well-known/pki-validation/starfield.html` la risposta deve contenere il `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="dc121-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="dc121-173">Verifica del record TXT DNS</span><span class="sxs-lookup"><span data-stu-id="dc121-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="dc121-174">Usando il gestore DNS, creare un record TXT nel sottodominio `@` con valore uguale al token di verifica del dominio.</span><span class="sxs-lookup"><span data-stu-id="dc121-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="dc121-175">Fare clic su **"Aggiorna"** per aggiornare lo stato del certificato dopo aver completato la verifica.</span><span class="sxs-lookup"><span data-stu-id="dc121-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="dc121-176">È necessario creare un record TXT su `@.<domain>` con valore `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="dc121-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="dc121-177">Assegnare il certificato all'app del servizio app</span><span class="sxs-lookup"><span data-stu-id="dc121-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="dc121-178">Se è stata selezionata l'opzione **SSL basato su IP** e il dominio personalizzato è stato configurato usando un record A, sarà necessario eseguire i passaggi aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc121-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="dc121-179">Dopo la configurazione di un'associazione SSL basata su IP, un indirizzo IP dedicato viene assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="dc121-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="dc121-180">È possibile trovare questo indirizzo IP nella pagina **Dominio personalizzato** nelle impostazioni dell'app, proprio sotto la sezione **Nomi host**.</span><span class="sxs-lookup"><span data-stu-id="dc121-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="dc121-181">È elencato come **Indirizzo IP esterno**</span><span class="sxs-lookup"><span data-stu-id="dc121-181">It is listed as **External IP Address**</span></span>

![inserimento immagine di IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="dc121-183">Si noti che questo indirizzo IP è diverso rispetto all'indirizzo IP virtuale utilizzato in precedenza per la configurazione del record A per il dominio.</span><span class="sxs-lookup"><span data-stu-id="dc121-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="dc121-184">Se è stato impostato l'uso del metodo SSL basato su SNI o se non è stato impostato l'uso del metodo SSL, per questa voce non è elencato alcun indirizzo.</span><span class="sxs-lookup"><span data-stu-id="dc121-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="dc121-185">Usando gli strumenti forniti dal registrar, modificare il record A per il nome di dominio personalizzato, in modo che faccia riferimento all'indirizzo IP riportato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="dc121-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="dc121-186">Reimpostare e sincronizzare il certificato</span><span class="sxs-lookup"><span data-stu-id="dc121-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="dc121-187">Sarà possibile reimpostare il certificato selezionando l'opzione **"Reimposta e sincronizza"** nel pannello **"Proprietà del certificato"**.</span><span class="sxs-lookup"><span data-stu-id="dc121-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="dc121-188">Fare clic sul pulsante **Reimposta** per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="dc121-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="dc121-189">Questo processo può richiedere da 1 a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dc121-189">This process can take 1-10 minutes to complete.</span></span>

![inserimento immagine della reimpostazione SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="dc121-191">Con la reimpostazione viene emesso un nuovo certificato da parte dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="dc121-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc121-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc121-192">Next Steps</span></span>

* [<span data-ttu-id="dc121-193">Aggiungere una Rete per la distribuzione di contenuti (CDN)</span><span class="sxs-lookup"><span data-stu-id="dc121-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)