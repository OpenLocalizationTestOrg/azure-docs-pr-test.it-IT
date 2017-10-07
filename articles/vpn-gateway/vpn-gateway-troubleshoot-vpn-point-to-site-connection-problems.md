---
title: problemi di connessione aaaTroubleshoot Azure point-to-site | Documenti Microsoft
description: Informazioni su come i problemi di connessione point-to-site tootroubleshoot.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="a3603-103">Risoluzione dei problemi: problemi di connessione da punto a sito di Azure</span><span class="sxs-lookup"><span data-stu-id="a3603-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="a3603-104">Questo articolo elenca i problemi comuni di connessione da punto a sito che l'utente potrebbe riscontrare.</span><span class="sxs-lookup"><span data-stu-id="a3603-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="a3603-105">e le possibili cause e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="a3603-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="a3603-106">Errore del client VPN: Impossibile trovare un certificato</span><span class="sxs-lookup"><span data-stu-id="a3603-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-107">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-107">Symptom</span></span>

<span data-ttu-id="a3603-108">Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-109">**Impossibile trovare un certificato utilizzabile con il protocollo EAP (Extensible Authentication Protocol). (Errore 798)**</span><span class="sxs-lookup"><span data-stu-id="a3603-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-110">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-110">Cause</span></span>

<span data-ttu-id="a3603-111">Questo problema si verifica se manca il certificato di client hello **certificati - corrente\Personale\Certificati**.</span><span class="sxs-lookup"><span data-stu-id="a3603-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-112">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-112">Solution</span></span>

<span data-ttu-id="a3603-113">Verificare che il certificato client hello sia installato nel seguente percorso dell'archivio certificati hello (Certmgr.msc) hello:</span><span class="sxs-lookup"><span data-stu-id="a3603-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="a3603-114">**Certificati - Utente corrente\Personale\Certificati**</span><span class="sxs-lookup"><span data-stu-id="a3603-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="a3603-115">Per ulteriori informazioni su come tooinstall hello certificato client, vedere [generare ed esportare i certificati per le connessioni point-to-site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="a3603-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a3603-116">Quando si importa certificato client hello, non selezionare hello **Abilita protezione avanzata chiave privata** opzione.</span><span class="sxs-lookup"><span data-stu-id="a3603-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="a3603-117">Errore del client VPN: il messaggio hello ricevuto è imprevisto o non formattato correttamente</span><span class="sxs-lookup"><span data-stu-id="a3603-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-118">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-118">Symptom</span></span>

<span data-ttu-id="a3603-119">Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-120">**messaggio ricevuto è imprevisto o non formattato correttamente. (Errore 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="a3603-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-121">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-121">Cause</span></span>

<span data-ttu-id="a3603-122">Questo problema si verifica se non è stata caricata chiave pubblica del certificato radice hello in gateway VPN di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="a3603-123">Può verificarsi anche se la chiave hello è danneggiata o scaduta.</span><span class="sxs-lookup"><span data-stu-id="a3603-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-124">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-124">Solution</span></span>

<span data-ttu-id="a3603-125">tooresolve questo problema, controllare lo stato di hello della radice hello in hello toosee portale Azure certificato se è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="a3603-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="a3603-126">Se non si è revocato, provare a reupload e un certificato radice di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="a3603-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="a3603-127">Per altre informazioni, vedere [Creare certificati](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="a3603-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="a3603-128">Errore del client VPN: Una catena di certificati è stata elaborata correttamente, ma termina</span><span class="sxs-lookup"><span data-stu-id="a3603-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="a3603-129">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-129">Symptom</span></span> 

<span data-ttu-id="a3603-130">Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-131">**Una catena di certificati elaborata, ma termina con un certificato radice considerato non attendibile dal provider di attendibilità hello.**</span><span class="sxs-lookup"><span data-stu-id="a3603-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-132">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-132">Solution</span></span>

1. <span data-ttu-id="a3603-133">Verificare che tale hello seguendo i certificati siano nella posizione corretta hello:</span><span class="sxs-lookup"><span data-stu-id="a3603-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="a3603-134">Certificate</span><span class="sxs-lookup"><span data-stu-id="a3603-134">Certificate</span></span> | <span data-ttu-id="a3603-135">Località</span><span class="sxs-lookup"><span data-stu-id="a3603-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="a3603-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="a3603-136">AzureClient.pfx</span></span>  | <span data-ttu-id="a3603-137">Utente corrente\Personale\Certificati</span><span class="sxs-lookup"><span data-stu-id="a3603-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="a3603-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="a3603-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="a3603-139">Utente corrente\Autorità di certificazione radice attendibili</span><span class="sxs-lookup"><span data-stu-id="a3603-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="a3603-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="a3603-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="a3603-141">Computer locale\Autorità di certificazione radice attendibili</span><span class="sxs-lookup"><span data-stu-id="a3603-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="a3603-142">Se sono già nel percorso hello certificati hello, provare a certificati hello toodelete e reinstallarlo.</span><span class="sxs-lookup"><span data-stu-id="a3603-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="a3603-143">Hello  **azuregateway -*GUID*. cloudapp.net** certificato è nel pacchetto di configurazione con i client VPN hello che è stato scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="a3603-144">È possibile utilizzare file archivers tooextract hello del file dal pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="a3603-145">Errore di download del file: L'URI di destinazione non è specificato</span><span class="sxs-lookup"><span data-stu-id="a3603-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-146">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-146">Symptom</span></span>

<span data-ttu-id="a3603-147">Viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-147">You receive hello following error message:</span></span>

<span data-ttu-id="a3603-148">**Errore di download del file. L'URI di destinazione non è specificato.**</span><span class="sxs-lookup"><span data-stu-id="a3603-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-149">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-149">Cause</span></span> 

<span data-ttu-id="a3603-150">Questo problema si verifica a causa di un tipo di gateway non corretto.</span><span class="sxs-lookup"><span data-stu-id="a3603-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="a3603-151">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-151">Solution</span></span>

<span data-ttu-id="a3603-152">deve essere il tipo di gateway VPN Hello **VPN**, e deve essere di tipo VPN hello **tipo RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="a3603-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="a3603-153">Errore del client VPN: Azure VPN custom script failed (Impossibile eseguire lo script personalizzato per la VPN di Azure)</span><span class="sxs-lookup"><span data-stu-id="a3603-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="a3603-154">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-154">Symptom</span></span>

<span data-ttu-id="a3603-155">Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-156">**Script personalizzato (tooupdate la tabella di routing.) non è riuscita. (Errore 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="a3603-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-157">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-157">Cause</span></span>

<span data-ttu-id="a3603-158">Questo problema può verificarsi se la connessione VPN site-to-point di hello tooopen utilizzando un collegamento.</span><span class="sxs-lookup"><span data-stu-id="a3603-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-159">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-159">Solution</span></span> 

<span data-ttu-id="a3603-160">Aprire il pacchetto VPN hello direttamente anziché aprirlo dal collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="a3603-161">Non è possibile installare i client VPN hello</span><span class="sxs-lookup"><span data-stu-id="a3603-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-162">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-162">Cause</span></span> 

<span data-ttu-id="a3603-163">Gateway VPN di hello tootrust necessarie per la rete virtuale non è un certificato aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="a3603-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="a3603-164">certificato Hello è incluso nel pacchetto di configurazione con i client VPN hello che viene generato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3603-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-165">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-165">Solution</span></span>

<span data-ttu-id="a3603-166">Estrarre il pacchetto di configurazione client VPN di hello e trovare il file con estensione cer hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="a3603-167">tooinstall hello del certificato, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a3603-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="a3603-168">Aprire mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="a3603-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="a3603-169">Aggiungere hello **certificati** snap-in.</span><span class="sxs-lookup"><span data-stu-id="a3603-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="a3603-170">Seleziona hello **Computer** account per il computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="a3603-171">Pulsante destro del mouse hello **autorità di certificazione radice attendibili** nodo.</span><span class="sxs-lookup"><span data-stu-id="a3603-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="a3603-172">Fare clic su **All attività** > **importazione**e i file con estensione cer toohello Sfoglia estratti dal pacchetto di configurazione client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="a3603-173">Riavviare il computer di hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="a3603-174">Provare a eseguire tooinstall hello VPN client.</span><span class="sxs-lookup"><span data-stu-id="a3603-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="a3603-175">Errore del portale di Azure: Impossibile gateway VPN di toosave hello e dati hello non validi</span><span class="sxs-lookup"><span data-stu-id="a3603-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-176">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-176">Symptom</span></span>

<span data-ttu-id="a3603-177">Quando si tenta di modifiche hello toosave per il gateway VPN hello in hello portale di Azure, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-178">**Gateway di rete virtuale non riuscita toosave &lt;* nome del gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="a3603-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="a3603-179">Data for certificate &lt;*certificate ID*&gt; is invalid.** (I dati per il certificato ID certificato non sono validi.)</span><span class="sxs-lookup"><span data-stu-id="a3603-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-180">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-180">Cause</span></span> 

<span data-ttu-id="a3603-181">Questo problema può verificarsi se hello radice certificato chiave pubblica è stata caricata contiene un carattere non valido, ad esempio uno spazio.</span><span class="sxs-lookup"><span data-stu-id="a3603-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-182">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-182">Solution</span></span>

<span data-ttu-id="a3603-183">Assicurarsi che i dati di hello nel certificato hello non contengano caratteri non validi, ad esempio le interruzioni di riga (ritorno a capo).</span><span class="sxs-lookup"><span data-stu-id="a3603-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="a3603-184">valore intero di Hello deve essere una riga lunga.</span><span class="sxs-lookup"><span data-stu-id="a3603-184">hello entire value should be one long line.</span></span> <span data-ttu-id="a3603-185">Dopo il testo Hello è riportato un esempio del certificato hello:</span><span class="sxs-lookup"><span data-stu-id="a3603-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="a3603-186">Errore del portale di Azure: Impossibile gateway VPN di toosave hello e nome risorsa hello non valido</span><span class="sxs-lookup"><span data-stu-id="a3603-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-187">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-187">Symptom</span></span>

<span data-ttu-id="a3603-188">Quando si tenta di modifiche hello toosave per il gateway VPN hello in hello portale di Azure, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="a3603-189">**Gateway di rete virtuale non riuscita toosave &lt;* nome del gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="a3603-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="a3603-190">Nome della risorsa &lt; *nome certificato si tenta di tooupload* &gt; è valido * *.</span><span class="sxs-lookup"><span data-stu-id="a3603-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-191">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-191">Cause</span></span>

<span data-ttu-id="a3603-192">Questo problema si verifica perché il nome di hello del certificato hello contiene un carattere non valido, ad esempio uno spazio.</span><span class="sxs-lookup"><span data-stu-id="a3603-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="a3603-193">Errore del portale di Azure: VPN package file download error 503 (Errore 503 relativo al download del file del pacchetto VPN)</span><span class="sxs-lookup"><span data-stu-id="a3603-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-194">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-194">Symptom</span></span>

<span data-ttu-id="a3603-195">Quando si tenta di pacchetto di configurazione client VPN hello toodownload, viene visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="a3603-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="a3603-196">**Nel file hello toodownload non riuscita. Dettagli errore: errore 503. Hello server è occupato.**</span><span class="sxs-lookup"><span data-stu-id="a3603-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="a3603-197">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-197">Solution</span></span>

<span data-ttu-id="a3603-198">Questo errore può essere causato da un problema di rete temporaneo.</span><span class="sxs-lookup"><span data-stu-id="a3603-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="a3603-199">Riprovare pacchetto VPN di hello toodownload dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a3603-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="a3603-200">Aggiornamento di Gateway VPN di Azure: client P2S tutti sono tooconnect Impossibile</span><span class="sxs-lookup"><span data-stu-id="a3603-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-201">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-201">Cause</span></span>

<span data-ttu-id="a3603-202">Se il certificato di hello è più del 50% tramite la relativa durata, il certificato di hello venga eseguito il rollover.</span><span class="sxs-lookup"><span data-stu-id="a3603-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-203">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-203">Solution</span></span>

<span data-ttu-id="a3603-204">tooresolve questo problema, creare e ridistribuire i nuovi certificati toohello VPN client.</span><span class="sxs-lookup"><span data-stu-id="a3603-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="a3603-205">Troppi client VPN connessi contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="a3603-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="a3603-206">Per ogni gateway VPN, numero massimo di hello di connessioni consentite è 128.</span><span class="sxs-lookup"><span data-stu-id="a3603-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="a3603-207">È possibile visualizzare numero totale di hello di client connessi in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3603-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="a3603-208">Point-to-site VPN aggiunge in modo non corretto di una route per tabella di route toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="a3603-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-209">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-209">Symptom</span></span>

<span data-ttu-id="a3603-210">Quando si effettua la connessione VPN nel client point-to-site hello hello, i client VPN hello deve aggiungere una route verso hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3603-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="a3603-211">servizio di supporto IP Hello deve aggiungere una route per la subnet hello del client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="a3603-212">intervallo di client VPN Hello appartiene tooa subnet più piccole di 10.0.0.0/8, ad esempio 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="a3603-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="a3603-213">Invece di una route per 10.0.12.0/24, viene aggiunta una route per 10.0.0.0/8 con priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="a3603-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="a3603-214">Questa route non corretta viene interrotta la connettività con altre reti locali che potrebbe appartenere a subnet tooanother nell'intervallo 10.0.0.0/8 hello, ad esempio 10.50.0.0/24, che non dispongono di una route specifica definita.</span><span class="sxs-lookup"><span data-stu-id="a3603-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="a3603-215">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-215">Cause</span></span>

<span data-ttu-id="a3603-216">Questo è il comportamento da progettazione per i client Windows.</span><span class="sxs-lookup"><span data-stu-id="a3603-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="a3603-217">Quando il client di hello Usa protocollo PPP IPCP hello, ottenuta indirizzo IP hello interfaccia tunnel hello dal server hello (gateway VPN di hello in questo caso).</span><span class="sxs-lookup"><span data-stu-id="a3603-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="a3603-218">Tuttavia, a causa di restrizioni nel protocollo hello, client hello è la subnet mask di hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="a3603-219">Poiché non esiste alcun altro tooget modo, client hello tenta tooguess hello la subnet mask basata sulla classe hello di indirizzo IP dell'interfaccia tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="a3603-220">Pertanto, viene aggiunta una route in base a hello dopo un mapping statico:</span><span class="sxs-lookup"><span data-stu-id="a3603-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="a3603-221">Se l'indirizzo appartiene A tooclass--> applicare valore/8</span><span class="sxs-lookup"><span data-stu-id="a3603-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="a3603-222">Se l'indirizzo appartiene tooclass--> B applicare /16</span><span class="sxs-lookup"><span data-stu-id="a3603-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="a3603-223">Se l'indirizzo appartiene tooclass--> C applicare /24</span><span class="sxs-lookup"><span data-stu-id="a3603-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="a3603-224">Il client VPN non riesce ad accedere alle condivisioni file di rete</span><span class="sxs-lookup"><span data-stu-id="a3603-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-225">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-225">Symptom</span></span>

<span data-ttu-id="a3603-226">client VPN Hello è connesso toohello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3603-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="a3603-227">Client hello tuttavia non è possibile accedere a condivisioni di rete.</span><span class="sxs-lookup"><span data-stu-id="a3603-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="a3603-228">Causa</span><span class="sxs-lookup"><span data-stu-id="a3603-228">Cause</span></span>

<span data-ttu-id="a3603-229">protocollo SMB Hello viene utilizzato per l'accesso alla condivisione file.</span><span class="sxs-lookup"><span data-stu-id="a3603-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="a3603-230">Quando viene avviata la connessione hello, client VPN hello aggiunge credenziali sessione hello e si verifica un errore di hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="a3603-231">Dopo aver stabilita la connessione hello, hello client deve le credenziali nella cache di hello toouse per l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a3603-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="a3603-232">Questo processo viene avviato query toohello Centro distribuzione chiavi (un controller di dominio) tooget un token.</span><span class="sxs-lookup"><span data-stu-id="a3603-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="a3603-233">Poiché client hello si connette da hello Internet, potrebbe non essere in grado di tooreach controller di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="a3603-234">Pertanto, client hello possibile eseguire il failover da tooNTLM Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a3603-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="a3603-235">Hello solo ora, tale client hello è richiesto per una credenziale è quando si dispone di un certificato valido (con SAN = UPN) rilasciato da toowhich dominio hello viene unita in join.</span><span class="sxs-lookup"><span data-stu-id="a3603-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="a3603-236">client Hello deve essere connessa fisicamente toohello rete di dominio.</span><span class="sxs-lookup"><span data-stu-id="a3603-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="a3603-237">In questo caso, i client hello tenta certificato hello toouse e raggiunge toohello controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="a3603-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="a3603-238">Restituirà un errore di "KDC_ERR_C_PRINCIPAL_UNKNOWN" hello Centro distribuzione chiavi.</span><span class="sxs-lookup"><span data-stu-id="a3603-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="a3603-239">client hello è forzato toofail su tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="a3603-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="a3603-240">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-240">Solution</span></span>

<span data-ttu-id="a3603-241">toowork problema hello, disabilitare la memorizzazione nella cache di hello delle credenziali di dominio da hello seguente sottochiave del Registro di sistema:</span><span class="sxs-lookup"><span data-stu-id="a3603-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="a3603-242">Impossibile trovare la connessione VPN point-to-site di hello in Windows dopo la reinstallazione di client VPN hello</span><span class="sxs-lookup"><span data-stu-id="a3603-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="a3603-243">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a3603-243">Symptom</span></span>

<span data-ttu-id="a3603-244">Rimuovere la connessione VPN point-to-site di hello e quindi reinstallare i client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="a3603-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="a3603-245">In questo caso, hello connessione VPN non è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a3603-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="a3603-246">Non è presente connessione VPN hello in hello **connessioni di rete** impostazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="a3603-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="a3603-247">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a3603-247">Solution</span></span>

<span data-ttu-id="a3603-248">problema di hello tooresolve, delete hello precedente VPN client i file di configurazione **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, quindi eseguire nuovamente il programma di installazione di hello VPN client.</span><span class="sxs-lookup"><span data-stu-id="a3603-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
