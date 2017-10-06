---
title: aaa "abilitare HTTPS in un dominio personalizzato CDN di Azure | Documenti di Microsoft"
description: Informazioni su come tooenable HTTPS nell'endpoint rete CDN di Azure con un dominio personalizzato.
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
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="04746-103">Abilitare HTTPS in un dominio personalizzato della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="04746-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="04746-104">Supporto HTTPS per i domini personalizzati rete CDN di Azure consente toodeliver contenuto protetto tramite SSL utilizzando la propria sicurezza di hello tooimprove nome dominio dei dati in transito.</span><span class="sxs-lookup"><span data-stu-id="04746-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="04746-105">Hello end-to-end del flusso di lavoro tooenable HTTPS per il dominio personalizzato è semplificata tramite un solo clic abilitazione, la gestione dei certificati completato e tutti i dati con senza alcun costo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="04746-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="04746-106">È critico tooensure sulla privacy di hello e l'integrità dei dati di tutti i dati sensibili di applicazioni web in transito.</span><span class="sxs-lookup"><span data-stu-id="04746-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="04746-107">Utilizzando il protocollo HTTPS garantisce che i dati sensibili vengono crittografati quando vengono inviate in hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="04746-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="04746-108">Assicura attendibilità, autenticazione e protezione delle applicazioni Web da attacchi.</span><span class="sxs-lookup"><span data-stu-id="04746-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="04746-109">La rete CDN di Azure supporta attualmente il protocollo HTTPS su un endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="04746-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="04746-110">Ad esempio, se si crea un endpoint CDN dalla rete CDN di Azure, ad esempio https://contoso.azureedge.net, il protocollo HTTPS è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="04746-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="04746-111">A questo punto, con la funzionalità HTTPS per il dominio personalizzato è possibile anche abilitare la distribuzione sicura per un dominio personalizzato, ad esempio https://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="04746-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="04746-112">Alcuni degli attributi della chiave hello di funzionalità HTTPS sono:</span><span class="sxs-lookup"><span data-stu-id="04746-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="04746-113">Assenza di costi aggiuntivi: non sono previsti costi per l'acquisizione o il rinnovo di certificati o per il traffico HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04746-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="04746-114">Si paga solo per GB in uscita dalla rete CDN hello.</span><span class="sxs-lookup"><span data-stu-id="04746-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="04746-115">Abilitazione della semplice: il provisioning di un clic è disponibile da hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04746-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="04746-116">È inoltre possibile utilizzare API REST o altre funzionalità di hello tooenable strumenti per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="04746-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="04746-117">Gestione completa dei certificati: tutta la fase di approvvigionamento e gestione di certificati viene gestita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="04746-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="04746-118">I certificati vengono automaticamente il provisioning e rinnovato tooexpiration precedente.</span><span class="sxs-lookup"><span data-stu-id="04746-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="04746-119">Questo rimuove completamente rischi hello dell'interruzione del servizio a causa della scadenza di un certificato.</span><span class="sxs-lookup"><span data-stu-id="04746-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="04746-120">Supporta HTTPS tooenabling precedente, è necessario avere già stabilito un [dominio personalizzato CDN Azure](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="04746-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="04746-121">Passaggio 1: Abilitare la funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="04746-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="04746-122">In hello [portale di Azure](https://portal.azure.com), Sfoglia Verizon tooyour standard o premium profilo CDN.</span><span class="sxs-lookup"><span data-stu-id="04746-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="04746-123">Nell'elenco di hello degli endpoint, fare clic sull'endpoint hello contenente il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="04746-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="04746-124">Fare clic su dominio di hello personalizzato per il quale si desidera tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04746-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Pannello Endpoint](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="04746-126">Fare clic su **su** tooenable HTTPS e salvare la modifica hello.</span><span class="sxs-lookup"><span data-stu-id="04746-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="04746-128">Passaggio 2: convalida del dominio</span><span class="sxs-lookup"><span data-stu-id="04746-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="04746-129">Prima che la funzionalità HTTPS sia attiva nel dominio personalizzato, è necessario completare la convalida del dominio.</span><span class="sxs-lookup"><span data-stu-id="04746-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="04746-130">Si dispone di 6 business giorni tooapprove hello dominio.</span><span class="sxs-lookup"><span data-stu-id="04746-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="04746-131">La richiesta verrà annullata se non si riceve l'approvazione entro 6 giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="04746-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="04746-132">Dopo aver abilitato HTTPS nel dominio personalizzato, il provider del certificato HTTPS DigiCert convaliderà la proprietà del dominio, contattare la persona hello per il dominio, in base alle informazioni di persona WHOIS, tramite posta elettronica (per impostazione predefinita) o telefono.</span><span class="sxs-lookup"><span data-stu-id="04746-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="04746-133">DigiCert anche invierà hello verifica posta elettronica toohello sotto indirizzi.</span><span class="sxs-lookup"><span data-stu-id="04746-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="04746-134">Se le informazioni sui registranti WHOIS sono private, assicurarsi di poterle approvare direttamente da uno di questi indirizzi.</span><span class="sxs-lookup"><span data-stu-id="04746-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="04746-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="04746-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="04746-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="04746-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="04746-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="04746-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="04746-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="04746-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="04746-139">Alla ricezione di posta elettronica hello, sono disponibili due opzioni di verifica:</span><span class="sxs-lookup"><span data-stu-id="04746-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="04746-140">È possibile approvare tutte le future ordini tramite hello stesso account per hello stesso dominio radice, ad esempio consoto.com. Questo è un approccio consigliato se si intende tooadd ulteriori domini personalizzati in futuro per hello hello nello stesso dominio radice.</span><span class="sxs-lookup"><span data-stu-id="04746-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="04746-141">È possibile approvare solo nome host specifico hello utilizzato in questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="04746-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="04746-142">Le richieste successive richiederanno un'approvazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="04746-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="04746-143">Posta elettronica di esempio:</span><span class="sxs-lookup"><span data-stu-id="04746-143">Example email:</span></span>
    
    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="04746-145">Dopo l'approvazione, DigiCert verrà aggiunto il certificato di SAN toohello nome dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="04746-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="04746-146">il certificato Hello sarà valido per un anno e venga automaticamente rinnovato prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="04746-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="04746-147">Passaggio 3: Attendere per la propagazione di hello quindi iniziare a usare le funzionalità</span><span class="sxs-lookup"><span data-stu-id="04746-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="04746-148">Al termine della convalida di nome di dominio hello richiederà too6 8 ore per hello dominio personalizzato HTTPS funzionalità toobe attivo.</span><span class="sxs-lookup"><span data-stu-id="04746-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="04746-149">Una volta completato il processo di hello, lo stato di "HTTPS personalizzati" hello in hello portale di Azure verrà impostato troppo "Enabled".</span><span class="sxs-lookup"><span data-stu-id="04746-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="04746-150">La funzionalità HTTPS con il dominio personalizzato è ora pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="04746-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="04746-151">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="04746-151">Frequently asked questions</span></span>

1. <span data-ttu-id="04746-152">*Chi è il provider certificate hello e viene utilizzato il tipo di certificato?*</span><span class="sxs-lookup"><span data-stu-id="04746-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="04746-153">Viene usato il certificato dei nomi alternativi soggetto (SAN) fornito da DigiCert.</span><span class="sxs-lookup"><span data-stu-id="04746-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="04746-154">Un certificato SAN può proteggere più nomi di dominio completi con un certificato.</span><span class="sxs-lookup"><span data-stu-id="04746-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="04746-155">*È possibile usare il certificato dedicato personale?*</span><span class="sxs-lookup"><span data-stu-id="04746-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="04746-156">Non attualmente, ma è on hello Guida di orientamento.</span><span class="sxs-lookup"><span data-stu-id="04746-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="04746-157">*Cosa accade se non si riceve posta elettronica di verifica dominio hello da DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="04746-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="04746-158">Se non si riceve un messaggio di posta elettronica entro 24 ore, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04746-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="04746-159">*L'uso di un certificato SAN è meno sicuro rispetto a un certificato dedicato?*</span><span class="sxs-lookup"><span data-stu-id="04746-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="04746-160">Un certificato SAN segue hello standard di crittografia e protezione stesso come un certificato dedicato. Tutti i certificati SSL emessi usano l'algoritmo SHA-256 per la protezione avanzata di server.</span><span class="sxs-lookup"><span data-stu-id="04746-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="04746-161">*È possibile usare la funzionalità HTTPS del dominio personalizzato con la rete CDN di Azure fornita da Akamai?*</span><span class="sxs-lookup"><span data-stu-id="04746-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="04746-162">Attualmente questa funzionalità è disponibile solo con la rete CDN di Azure fornita da Verizon.</span><span class="sxs-lookup"><span data-stu-id="04746-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="04746-163">Stiamo lavorando sul supporto di questa funzionalità con la rete CDN Azure da Akamai nei prossimi mesi hello.</span><span class="sxs-lookup"><span data-stu-id="04746-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="04746-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04746-164">Next steps</span></span>

- <span data-ttu-id="04746-165">Informazioni su come tooset backup un [dominio personalizzato per l'endpoint rete CDN di Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="04746-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


