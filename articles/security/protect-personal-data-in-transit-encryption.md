---
title: dati personali aaaProtect in transito con la crittografia in Azure | Documenti Microsoft
description: Usare la crittografia dei dati personali tooprotect Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="ba36d-103">Tecnologie di crittografia di Azure: proteggere i dati personali in transito con la crittografia</span><span class="sxs-lookup"><span data-stu-id="ba36d-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="ba36d-104">In questo articolo consentono di comprendere e utilizzare dati toosecure di tecnologie Azure crittografia in transito.</span><span class="sxs-lookup"><span data-stu-id="ba36d-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="ba36d-105">Durante il trasferimento in rete hello privacy hello protezione dei dati personali è una parte essenziale di una strategia di sicurezza a più livelli di difesa in profondità.</span><span class="sxs-lookup"><span data-stu-id="ba36d-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="ba36d-106">La crittografia in transito è tooprevent progettato un utente malintenzionato intercetta le trasmissioni di dati in grado di hello tooview oppure utilizzare il.</span><span class="sxs-lookup"><span data-stu-id="ba36d-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="ba36d-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="ba36d-107">Scenario</span></span>

<span data-ttu-id="ba36d-108">Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico.</span><span class="sxs-lookup"><span data-stu-id="ba36d-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="ba36d-109">toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito</span><span class="sxs-lookup"><span data-stu-id="ba36d-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="ba36d-110">la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="ba36d-111">Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale,</span><span class="sxs-lookup"><span data-stu-id="ba36d-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="ba36d-112">Include inoltre informazioni reparto risorse umane tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="ba36d-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="ba36d-113">riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.</span><span class="sxs-lookup"><span data-stu-id="ba36d-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="ba36d-114">Dati personali di clienti viene inseriti nel database hello da sedi remote della società hello e dagli agenti di viaggio presenti in ogni HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="ba36d-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="ba36d-115">Documenti che contengono informazioni sul cliente vengono trasferiti attraverso l'archiviazione di tooAzure rete hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="ba36d-116">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="ba36d-116">Problem statement</span></span>

<span data-ttu-id="ba36d-117">società Hello necessario proteggere la privacy hello di clienti e dati personali dei dipendenti mentre sono in transito tooand dai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba36d-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="ba36d-118">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="ba36d-118">Company goal</span></span>

<span data-ttu-id="ba36d-119">Hello tooensure obiettivo aziendale che i dati personali vengono crittografati quando dal disco.</span><span class="sxs-lookup"><span data-stu-id="ba36d-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="ba36d-120">Se gli utenti non autorizzati intercettano i dati personali di hello off disco, deve essere in un formato che verrà eseguito il rendering illeggibile.</span><span class="sxs-lookup"><span data-stu-id="ba36d-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="ba36d-121">L'applicazione della crittografia deve essere facile o completamente trasparente per utenti e amministratori.</span><span class="sxs-lookup"><span data-stu-id="ba36d-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="ba36d-122">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="ba36d-122">Solutions</span></span>

<span data-ttu-id="ba36d-123">Servizi di Azure forniscono più toohelp strumenti e tecnologie proteggere i dati personali in transito.</span><span class="sxs-lookup"><span data-stu-id="ba36d-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="ba36d-124">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-124">Azure Storage</span></span>

<span data-ttu-id="ba36d-125">I dati archiviati nel cloud hello devono essere spostata dal client hello, che possono essere collocati fisicamente ovunque nel mondo hello, toohello data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba36d-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="ba36d-126">Quando i dati vengono recuperati dagli utenti, viene trasferito di nuovo, in hello opposto direzione.</span><span class="sxs-lookup"><span data-stu-id="ba36d-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="ba36d-127">Dati in transito su hello rete Internet pubblica vengono sempre al rischio di intercettazione da utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="ba36d-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="ba36d-128">È importante tooprotect sulla privacy di hello dei dati personali utilizzando la crittografia a livello di trasporto toosecure come si sposta tra i percorsi.</span><span class="sxs-lookup"><span data-stu-id="ba36d-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="ba36d-129">il protocollo HTTPS Hello fornisce un canale di comunicazione protetto e crittografato su hello Internet.</span><span class="sxs-lookup"><span data-stu-id="ba36d-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="ba36d-130">HTTPS deve essere utilizzato tooaccess oggetti nell'archiviazione di Azure e quando si chiama l'API REST.</span><span class="sxs-lookup"><span data-stu-id="ba36d-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="ba36d-131">Imporre l'uso del protocollo HTTPS hello quando si utilizza [firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) oggetti di archiviazione tooAzure accesso toodelegate (SAS).</span><span class="sxs-lookup"><span data-stu-id="ba36d-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="ba36d-132">Esistono due tipi di firma di accesso condiviso: del servizio e dell'account.</span><span class="sxs-lookup"><span data-stu-id="ba36d-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="ba36d-133">Come creare una firma di accesso condiviso del servizio</span><span class="sxs-lookup"><span data-stu-id="ba36d-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="ba36d-134">Servizio SAS delegati accesso tooa risorsa in uno dei servizi di archiviazione hello (servizio blob, coda, tabella o file).</span><span class="sxs-lookup"><span data-stu-id="ba36d-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="ba36d-135">un servizio di firma di accesso condiviso, tooconstruct hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba36d-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="ba36d-136">Specificare hello firmato il campo della versione</span><span class="sxs-lookup"><span data-stu-id="ba36d-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="ba36d-137">Specificare hello risorse firmato (Blob e File solo servizio)</span><span class="sxs-lookup"><span data-stu-id="ba36d-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="ba36d-138">Specificare i parametri di Query le intestazioni di risposta tooOverride (servizio Blob e File solo servizio)</span><span class="sxs-lookup"><span data-stu-id="ba36d-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="ba36d-139">Specificare il nome di tabella (solo servizio tabella) hello</span><span class="sxs-lookup"><span data-stu-id="ba36d-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="ba36d-140">Specificare i criteri di accesso hello</span><span class="sxs-lookup"><span data-stu-id="ba36d-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="ba36d-141">Specificare l'intervallo di validità della firma hello</span><span class="sxs-lookup"><span data-stu-id="ba36d-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="ba36d-142">Specificare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="ba36d-142">Specify Permissions</span></span>

9. <span data-ttu-id="ba36d-143">Specificare l'indirizzo IP o l'intervallo IP</span><span class="sxs-lookup"><span data-stu-id="ba36d-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="ba36d-144">Specificare il protocollo HTTP hello</span><span class="sxs-lookup"><span data-stu-id="ba36d-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="ba36d-145">Specificare gli intervalli di accesso delle tabelle</span><span class="sxs-lookup"><span data-stu-id="ba36d-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="ba36d-146">Specificare l'identificatore firmato hello</span><span class="sxs-lookup"><span data-stu-id="ba36d-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="ba36d-147">Specificare hello firma</span><span class="sxs-lookup"><span data-stu-id="ba36d-147">Specify hello Signature</span></span>

<span data-ttu-id="ba36d-148">Per istruzioni più dettagliate, vedere [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN) (Creazione di una firma di accesso condiviso del servizio).</span><span class="sxs-lookup"><span data-stu-id="ba36d-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="ba36d-149">Come creare una firma di accesso condiviso dell'account</span><span class="sxs-lookup"><span data-stu-id="ba36d-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="ba36d-150">Una firma di accesso condiviso delega accesso tooresources in uno o più dei servizi di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="ba36d-151">È inoltre possibile delegare accesso tooread, scrittura e le operazioni di eliminazione in contenitori blob, tabelle, code e le condivisioni di file che non sono consentite con un firma di accesso condiviso del servizio.</span><span class="sxs-lookup"><span data-stu-id="ba36d-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="ba36d-152">Costruzione di una firma di accesso condiviso è simile toothat una firma di accesso condiviso del servizio.</span><span class="sxs-lookup"><span data-stu-id="ba36d-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="ba36d-153">Per istruzioni dettagliate, vedere [Constructing an Account SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN) (Creazione di una firma di accesso condiviso dell'account).</span><span class="sxs-lookup"><span data-stu-id="ba36d-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="ba36d-154">Come imporre HTTPS nella chiamata di API REST</span><span class="sxs-lookup"><span data-stu-id="ba36d-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="ba36d-155">tooenforce hello l'uso di HTTPS durante la chiamata di oggetti di API REST tooaccess negli account di archiviazione è possibile abilitare Secure trasferimento necessari per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="ba36d-156">Nel portale di Azure hello, selezionare **crea Account di archiviazione**, o per un account di archiviazione esistente, selezionare **impostazioni** e quindi **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="ba36d-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="ba36d-157">In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="ba36d-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Creazione di un account di archiviazione](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="ba36d-159">Per istruzioni più dettagliate, incluso come tooenable Secure trasferimento necessarie a livello di codice, vedere [richiedono Secure trasferimento](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="ba36d-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="ba36d-160">Come crittografare i dati in Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="ba36d-161">tooencrypt dati in transito con [archiviazione File di Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), è possibile utilizzare SMB 3. x con Windows 8, 8.1 e 10 e Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ba36d-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="ba36d-162">Quando si utilizza il servizio di Azure file hello, qualsiasi connessione senza crittografia ha esito negativo quando la "Protezione di trasferimento richiesto" è abilitate.</span><span class="sxs-lookup"><span data-stu-id="ba36d-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="ba36d-163">Sono inclusi scenari con alcune varianti di hello client Linux SMB, SMB 2.1 e SMB 3.0 senza crittografia.</span><span class="sxs-lookup"><span data-stu-id="ba36d-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="ba36d-164">Crittografia lato client di Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="ba36d-165">Un'altra opzione per proteggere i dati personali durante il trasferimento tra un'applicazione client e Archiviazione di Azure è la [crittografia lato client](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="ba36d-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="ba36d-166">Hello dati vengono crittografati prima di essere trasferiti nell'archiviazione di Azure e quando si recuperano dati hello da archiviazione di Azure, dati hello viene decrittografati dopo la ricezione sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="ba36d-167">VPN da sito a sito di Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="ba36d-168">Un modo efficace tooprotect personali di dati in transito tra una rete aziendale o utente e hello rete virtuale di Azure sono toouse un [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) o [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) rete privata virtuale (VPN, Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="ba36d-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="ba36d-169">Una connessione VPN crea un canale crittografato protetto tra hello Internet.</span><span class="sxs-lookup"><span data-stu-id="ba36d-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="ba36d-170">Come creare una connessione VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="ba36d-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="ba36d-171">Una VPN da sito a sito si connette a più utenti su hello tooAzure di rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="ba36d-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="ba36d-172">una connessione site-to-site nel portale di Azure hello toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba36d-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="ba36d-173">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba36d-173">Create a virtual network.</span></span>

2. <span data-ttu-id="ba36d-174">Specificare un server DNS</span><span class="sxs-lookup"><span data-stu-id="ba36d-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="ba36d-175">Creare subnet del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="ba36d-176">Creare il gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="ba36d-177">Creare il gateway di rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="ba36d-178">Configurare il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ba36d-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="ba36d-179">Creare la connessione VPN hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="ba36d-180">Verificare una connessione VPN hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="ba36d-181">Per istruzioni dettagliate su come connessione toocreate una site-to-site in hello Azure portale, vedere [connessione di creare un sito a sito nel portale di Azure hello]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="ba36d-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="ba36d-182">Come creare una connessione VPN da punto a sito</span><span class="sxs-lookup"><span data-stu-id="ba36d-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="ba36d-183">Una VPN Point-to-Site consente di creare una connessione sicura da una rete virtuale di computer tooa singoli client.</span><span class="sxs-lookup"><span data-stu-id="ba36d-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="ba36d-184">Ciò è utile quando si desidera tooAzure tooconnect da una posizione remota, ad esempio dall'area home o un hotel conferenza.</span><span class="sxs-lookup"><span data-stu-id="ba36d-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="ba36d-185">una connessione point-to-site nel portale di Azure hello toocreate</span><span class="sxs-lookup"><span data-stu-id="ba36d-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="ba36d-186">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba36d-186">Create a virtual network.</span></span>

2. <span data-ttu-id="ba36d-187">Aggiungere una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="ba36d-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="ba36d-188">Specificare un server DNS</span><span class="sxs-lookup"><span data-stu-id="ba36d-188">Specify a DNS server.</span></span> <span data-ttu-id="ba36d-189">(facoltativo).</span><span class="sxs-lookup"><span data-stu-id="ba36d-189">(optional)</span></span>

4. <span data-ttu-id="ba36d-190">Creare un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba36d-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="ba36d-191">Generare i certificati.</span><span class="sxs-lookup"><span data-stu-id="ba36d-191">Generate certificates.</span></span>

6. <span data-ttu-id="ba36d-192">Aggiungere pool di indirizzi hello client.</span><span class="sxs-lookup"><span data-stu-id="ba36d-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="ba36d-193">Caricare dati certificato pubblica del certificato radice hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="ba36d-194">Generare e installare il pacchetto di configurazione client VPN di hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="ba36d-195">Installare un certificato client esportato.</span><span class="sxs-lookup"><span data-stu-id="ba36d-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="ba36d-196">Connettersi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ba36d-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="ba36d-197">Verificare la connessione.</span><span class="sxs-lookup"><span data-stu-id="ba36d-197">Verify your connection.</span></span>

<span data-ttu-id="ba36d-198">Per istruzioni dettagliate, vedere [configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: portale di Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="ba36d-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="ba36d-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="ba36d-199">SSL/TLS</span></span>

<span data-ttu-id="ba36d-200">Si consiglia di utilizzare sempre dati tooexchange di protocolli SSL/TLS in posizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="ba36d-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="ba36d-201">Le organizzazioni che scelgono toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandi set di dati in un collegamento WAN ad alta velocità dedicato inoltre possibile crittografare i dati hello hello utilizzando SSL/TLS o altri protocolli per una maggiore protezione a livello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba36d-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="ba36d-202">Crittografia predefinita</span><span class="sxs-lookup"><span data-stu-id="ba36d-202">Encryption by default</span></span>

<span data-ttu-id="ba36d-203">Microsoft utilizza i dati di tooprotect crittografia in transito tra clienti e i servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba36d-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="ba36d-204">Se si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ba36d-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="ba36d-205">[Livello di sicurezza del trasporto](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) è protocollo hello che data center Microsoft tenterà toonegotiate con i sistemi client che si connettono a servizi cloud tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="ba36d-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="ba36d-206">TLS offre autenticazione avanzata, privacy e integrità dei messaggi (supportando il rilevamento di manomissioni, intercettazioni e falsificazioni di messaggi), interoperabilità, flessibilità degli algoritmi e facilità di distribuzione e uso.</span><span class="sxs-lookup"><span data-stu-id="ba36d-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="ba36d-207">Viene anche usata la funzionalità [Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) affinché ogni connessione tra i sistemi client dei clienti e i servizi cloud Microsoft usi chiavi univoche.</span><span class="sxs-lookup"><span data-stu-id="ba36d-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="ba36d-208">Servizi cloud di connessioni tooMicrosoft inoltre sfruttare basato su RSA 2048 bit crittografia lunghezze di chiave.</span><span class="sxs-lookup"><span data-stu-id="ba36d-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="ba36d-209">combinazione di TLS, lunghezze delle chiavi RSA 2048 bit, Hello e PFS rende molto più difficile a qualcuno toointercept e accedere ai dati in transito tra clienti e i servizi cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ba36d-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="ba36d-210">I dati in transito sono sempre crittografati in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="ba36d-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="ba36d-211">Inoltre supporto toopersistent toostoring precedenti dati tooencrypting hello dati vengono sempre anche protetti in transito tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ba36d-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="ba36d-212">HTTPS è l'unico protocollo hello è supportato per hello che interfacce REST di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ba36d-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="ba36d-213">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ba36d-213">Summary</span></span>

<span data-ttu-id="ba36d-214">Per eseguire l'obiettivo di protezione sulla privacy di hello e dati personale di tali dati dall'applicazione tooAzure connessioni HTTPS archiviazione, tramite firme di accesso condiviso e l'abilitazione di Secure trasferimento necessarie sugli account di archiviazione hello società Hello.</span><span class="sxs-lookup"><span data-stu-id="ba36d-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="ba36d-215">Può anche proteggere i dati personali usando connessioni SMB 3.0 e implementando la crittografia lato client.</span><span class="sxs-lookup"><span data-stu-id="ba36d-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="ba36d-216">Le connessioni VPN da sito a sito da hello rete aziendale toohello rete virtuale di Azure e le connessioni VPN point-to-site da singoli utenti creerà un tunnel sicuro tramite cui possono essere trasmessi in modo sicuro i dati personali.</span><span class="sxs-lookup"><span data-stu-id="ba36d-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="ba36d-217">Procedure consigliate di crittografia predefinita di Microsoft verranno proteggere ulteriormente privacy hello dei dati personali.</span><span class="sxs-lookup"><span data-stu-id="ba36d-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba36d-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba36d-218">Next steps</span></span>

- [<span data-ttu-id="ba36d-219">Procedure consigliate per la sicurezza dei dati e la crittografia in Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="ba36d-220">Pianificazione e progettazione per il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="ba36d-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="ba36d-221">Domande frequenti sul gateway VPN</span><span class="sxs-lookup"><span data-stu-id="ba36d-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="ba36d-222">Acquistare e configurare un certificato SSL per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ba36d-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
