---
title: Abilitare HTTPS in un dominio personalizzato della rete CDN di Azure | Documentazione Microsoft
description: Informazioni su come abilitare HTTPS nell'endpoint della rete CDN di Azure con un dominio personalizzato.
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="2456f-103">Abilitare HTTPS in un dominio personalizzato della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="2456f-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="2456f-104">Il supporto di HTTPS per i domini personalizzati della rete CDN di Azure consente di distribuire contenuto protetto tramite SSL usando il nome del proprio dominio per una maggiore sicurezza dei dati in transito.</span><span class="sxs-lookup"><span data-stu-id="2456f-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="2456f-105">Il flusso di lavoro end-to-end per abilitare il protocollo HTTPS per il dominio personalizzato è più semplice grazie all'abilitazione con un unico clic e alla gestione completa dei certificati, il tutto senza costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2456f-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="2456f-106">È fondamentale garantire la riservatezza e l'integrità di tutti i dati sensibili delle applicazioni Web in transito.</span><span class="sxs-lookup"><span data-stu-id="2456f-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="2456f-107">Il protocollo HTTPS garantisce la crittografia dei dati sensibili inviati su Internet.</span><span class="sxs-lookup"><span data-stu-id="2456f-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="2456f-108">Assicura attendibilità, autenticazione e protezione delle applicazioni Web da attacchi.</span><span class="sxs-lookup"><span data-stu-id="2456f-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="2456f-109">La rete CDN di Azure supporta attualmente il protocollo HTTPS su un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="2456f-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="2456f-110">Ad esempio, se si crea un endpoint CDN dalla rete CDN di Azure, ad esempio https://contoso.azureedge.net, il protocollo HTTPS è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2456f-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="2456f-111">A questo punto, con la funzionalità HTTPS per il dominio personalizzato è possibile anche abilitare la distribuzione sicura per un dominio personalizzato, ad esempio https://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2456f-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="2456f-112">Alcuni attributi chiave della funzionalità HTTPS sono:</span><span class="sxs-lookup"><span data-stu-id="2456f-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="2456f-113">Assenza di costi aggiuntivi: non sono previsti costi per l'acquisizione o il rinnovo di certificati o per il traffico HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2456f-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="2456f-114">L'addebito è relativo solo ai GB in uscita dalla rete CDN.</span><span class="sxs-lookup"><span data-stu-id="2456f-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="2456f-115">Abilitazione semplice: il provisioning è disponibile con un unico clic nel [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2456f-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2456f-116">È possibile anche usare l'API REST o altri strumenti per sviluppatori per abilitare la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2456f-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="2456f-117">Gestione completa dei certificati: tutta la fase di approvvigionamento e gestione di certificati viene gestita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2456f-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="2456f-118">Il provisioning e il rinnovo dei certificati vengono eseguiti automaticamente prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="2456f-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="2456f-119">In questo modo si riduce completamente il rischio di interruzione del servizio a causa della scadenza di un certificato.</span><span class="sxs-lookup"><span data-stu-id="2456f-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="2456f-120">Prima di abilitare il supporto di HTTPS, è necessario avere già definito un [dominio personalizzato della rete CDN di Azure](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="2456f-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="2456f-121">Passaggio 1: abilitazione della funzionalità</span><span class="sxs-lookup"><span data-stu-id="2456f-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="2456f-122">Nel [portale di Azure](https://portal.azure.com) passare al profilo della rete CDN Standard o Premium di Verizon.</span><span class="sxs-lookup"><span data-stu-id="2456f-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="2456f-123">Nell'elenco di endpoint fare clic sull'endpoint contenente il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2456f-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="2456f-124">Selezionare il dominio personalizzato per il quale si vuole abilitare la funzionalità HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2456f-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Pannello Endpoint](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="2456f-126">Fare clic su **Attiva** per abilitare la funzionalità HTTPS e salvare la modifica.</span><span class="sxs-lookup"><span data-stu-id="2456f-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="2456f-128">Passaggio 2: convalida del dominio</span><span class="sxs-lookup"><span data-stu-id="2456f-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="2456f-129">Prima che la funzionalità HTTPS sia attiva nel dominio personalizzato, è necessario completare la convalida del dominio.</span><span class="sxs-lookup"><span data-stu-id="2456f-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="2456f-130">Per l'approvazione del dominio sono disponibili 6 giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="2456f-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="2456f-131">La richiesta verrà annullata se non si riceve l'approvazione entro 6 giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="2456f-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="2456f-132">Dopo l'abilitazione di HTTPS nel dominio personalizzato, DigiCert, il provider del certificato HTTPS, convaliderà la proprietà del dominio contattando il registrante per il dominio usando le informazioni sul registrante WHOIS tramite posta elettronica (per impostazione predefinita) o telefono.</span><span class="sxs-lookup"><span data-stu-id="2456f-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="2456f-133">DigiCert invierà l'email di verifica anche agli indirizzi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2456f-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="2456f-134">Se le informazioni sui registranti WHOIS sono private, assicurarsi di poterle approvare direttamente da uno di questi indirizzi.</span><span class="sxs-lookup"><span data-stu-id="2456f-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="2456f-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="2456f-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="2456f-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="2456f-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="2456f-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="2456f-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="2456f-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="2456f-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="2456f-139">Alla ricezione del messaggio di posta elettronica sono disponibili due opzioni di verifica:</span><span class="sxs-lookup"><span data-stu-id="2456f-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="2456f-140">È possibile approvare tutti gli ordini futuri eseguiti con lo stesso account per lo stesso dominio radice, ad esempio contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2456f-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="2456f-141">Questo approccio è consigliato se si prevede di aggiungere altri domini personalizzati in futuro per lo stesso dominio radice.</span><span class="sxs-lookup"><span data-stu-id="2456f-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="2456f-142">È possibile approvare solo il nome host specifico usato in questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="2456f-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="2456f-143">Le richieste successive richiederanno un'approvazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="2456f-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="2456f-144">Posta elettronica di esempio:</span><span class="sxs-lookup"><span data-stu-id="2456f-144">Example email:</span></span>
    
    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="2456f-146">Dopo l'approvazione, DigiCert aggiungerà il nome del dominio personalizzato al certificato SAN.</span><span class="sxs-lookup"><span data-stu-id="2456f-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="2456f-147">Il certificato sarà valido per un anno e verrà rinnovato automaticamente prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="2456f-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="2456f-148">Passaggio 3: attendere la propagazione, quindi iniziare a usare la funzionalità</span><span class="sxs-lookup"><span data-stu-id="2456f-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="2456f-149">Dopo la convalida del nome di dominio sono necessarie a 6-8 ore per l'attivazione della funzionalità HTTPS nel dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2456f-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="2456f-150">Al termine del processo, lo stato del protocollo "HTTPS personalizzato" nel portale di Azure verrà impostato su "Abilitato".</span><span class="sxs-lookup"><span data-stu-id="2456f-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="2456f-151">La funzionalità HTTPS con il dominio personalizzato è ora pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="2456f-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="2456f-152">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="2456f-152">Frequently asked questions</span></span>

1. <span data-ttu-id="2456f-153">*Chi è il provider di certificati e quale tipo di certificato viene usato?*</span><span class="sxs-lookup"><span data-stu-id="2456f-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="2456f-154">Viene usato il certificato dei nomi alternativi soggetto (SAN) fornito da DigiCert.</span><span class="sxs-lookup"><span data-stu-id="2456f-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="2456f-155">Un certificato SAN può proteggere più nomi di dominio completi con un certificato.</span><span class="sxs-lookup"><span data-stu-id="2456f-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="2456f-156">*È possibile usare il certificato dedicato personale?*</span><span class="sxs-lookup"><span data-stu-id="2456f-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="2456f-157">Non attualmente, ma questa possibilità è prevista nel piano d'azione.</span><span class="sxs-lookup"><span data-stu-id="2456f-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="2456f-158">*Cosa accade se non si riceve il messaggio di verifica del dominio da DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="2456f-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="2456f-159">Se non si riceve un messaggio di posta elettronica entro 24 ore, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2456f-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="2456f-160">*L'uso di un certificato SAN è meno sicuro rispetto a un certificato dedicato?*</span><span class="sxs-lookup"><span data-stu-id="2456f-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="2456f-161">Un certificato SAN applica gli stessi standard di crittografia e protezione di un certificato dedicato.</span><span class="sxs-lookup"><span data-stu-id="2456f-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="2456f-162">Tutti i certificati SSL emessi usano l'algoritmo SHA-256 per la protezione avanzata di server.</span><span class="sxs-lookup"><span data-stu-id="2456f-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="2456f-163">*È possibile usare la funzionalità HTTPS del dominio personalizzato con la rete CDN di Azure fornita da Akamai?*</span><span class="sxs-lookup"><span data-stu-id="2456f-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="2456f-164">Attualmente questa funzionalità è disponibile solo con la rete CDN di Azure fornita da Verizon.</span><span class="sxs-lookup"><span data-stu-id="2456f-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="2456f-165">Siamo impegnati nel fornire il supporto di questa funzionalità con la rete CDN di Azure fornita da Akamai nei prossimi mesi.</span><span class="sxs-lookup"><span data-stu-id="2456f-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2456f-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2456f-166">Next steps</span></span>

- <span data-ttu-id="2456f-167">Informazioni su come configurare un [dominio personalizzato nell'endpoint della rete CDN di Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="2456f-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


