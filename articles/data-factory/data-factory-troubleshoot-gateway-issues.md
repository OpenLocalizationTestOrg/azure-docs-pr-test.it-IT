---
title: problemi di Gateway di gestione dati aaaTroubleshoot | Documenti Microsoft
description: Fornisce suggerimenti tootroubleshoot problemi correlati tooData Gateway di gestione.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="da962-103">Risolvere i problemi nell'uso del gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="da962-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="da962-104">Questo articolo offre informazioni sulla risoluzione dei problemi nell'uso del gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="da962-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="da962-105">Vedere hello [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per informazioni dettagliate sul gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="da962-106">Vedere hello [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per una procedura dettagliata di spostare i dati da un tooMicrosoft di database di SQL Server locale nell'archiviazione Blob di Azure tramite gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="da962-107">Gateway tooinstall o registrare non riuscito</span><span class="sxs-lookup"><span data-stu-id="da962-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="da962-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-108">1. Problem</span></span>
<span data-ttu-id="da962-109">Viene visualizzato questo messaggio di errore durante l'installazione e la registrazione di un gateway, in particolare, durante il download dei file di installazione di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="da962-110">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-110">Cause</span></span>
<span data-ttu-id="da962-111">macchina Hello in cui si sta tentando di gateway hello tooinstall non riuscita toodownload hello ultimo gateway file di installazione dall'area download hello a causa di problemi di rete tooa.</span><span class="sxs-lookup"><span data-stu-id="da962-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-112">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-112">Resolution</span></span>
<span data-ttu-id="da962-113">Verificare toosee di impostazioni del firewall proxy server se la connessione di rete hello da hello computer toohello il bambino hello [area download](https://download.microsoft.com/)e aggiornare le impostazioni di hello di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="da962-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="da962-114">In alternativa, è possibile scaricare i file di installazione hello gateway più recente di hello da hello [area download](https://www.microsoft.com/download/details.aspx?id=39717) in altri computer che possono accedere area download hello.</span><span class="sxs-lookup"><span data-stu-id="da962-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="da962-115">È possibile quindi gateway di toohello file di programma di installazione di copia hello computer host e lo si esegue manualmente gateway hello tooinstall e update.</span><span class="sxs-lookup"><span data-stu-id="da962-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="da962-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-116">2. Problem</span></span>
<span data-ttu-id="da962-117">Questo errore viene visualizzato quando si tenta un gateway tooinstall facendo **installare direttamente in questo computer** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="da962-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="da962-118">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-118">Cause</span></span>
<span data-ttu-id="da962-119">Un gateway è già installato nel computer di hello.</span><span class="sxs-lookup"><span data-stu-id="da962-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-120">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-120">Resolution</span></span>
<span data-ttu-id="da962-121">Disinstallare hello gateway esistente nel computer di hello e fare clic su hello **installare direttamente in questo computer** collegare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="da962-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="da962-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-122">3. Problem</span></span>
<span data-ttu-id="da962-123">Questo errore può verificarsi quando si registra un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="da962-124">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-124">Cause</span></span>
<span data-ttu-id="da962-125">Verrà visualizzato questo messaggio per uno dei seguenti motivi hello:</span><span class="sxs-lookup"><span data-stu-id="da962-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="da962-126">formato Hello della chiave del gateway hello è valido.</span><span class="sxs-lookup"><span data-stu-id="da962-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="da962-127">chiave del gateway Hello è stata invalidata.</span><span class="sxs-lookup"><span data-stu-id="da962-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="da962-128">chiave del gateway Hello è stata rigenerata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="da962-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="da962-129">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-129">Resolution</span></span>
<span data-ttu-id="da962-130">Verificare se si utilizza una chiave di gateway corretto hello dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="da962-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="da962-131">Se è necessario rigenerare una chiave e utilizzare hello tooregister chiave hello gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="da962-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-132">4. Problem</span></span>
<span data-ttu-id="da962-133">È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Il contenuto o il formato della chiave non è valido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="da962-135">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-135">Cause</span></span>
<span data-ttu-id="da962-136">Hello contenuto o il formato della chiave del gateway input hello non è corretto.</span><span class="sxs-lookup"><span data-stu-id="da962-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="da962-137">Uno dei motivi hello è possibile che solo una parte della chiave hello copiato dal portale hello o si usa una chiave non valida.</span><span class="sxs-lookup"><span data-stu-id="da962-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-138">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-138">Resolution</span></span>
<span data-ttu-id="da962-139">Generare una chiave del gateway nel portale di hello e utilizzare hello copia pulsante toocopy hello intera chiave.</span><span class="sxs-lookup"><span data-stu-id="da962-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="da962-140">Quindi incollarlo in questo gateway di hello tooregister finestra.</span><span class="sxs-lookup"><span data-stu-id="da962-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="da962-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-141">5. Problem</span></span>
<span data-ttu-id="da962-142">È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="da962-144">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-144">Cause</span></span>
<span data-ttu-id="da962-145">è stata rigenerata la chiave del gateway Hello o gateway hello è stato eliminato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="da962-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="da962-146">Può inoltre verificarsi se il programma di installazione di hello Gateway di gestione dati non è più recente.</span><span class="sxs-lookup"><span data-stu-id="da962-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-147">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-147">Resolution</span></span>
<span data-ttu-id="da962-148">Controllare se l'installazione di Gateway di gestione dati hello è la versione più recente di hello, è possibile trovare la versione più recente di hello in hello Microsoft [area download](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="da962-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="da962-149">Se dell'installazione corrente / più recente e gateway esiste ancora nel portale, rigenerare la chiave di gateway hello in hello portale di Azure, utilizzare hello copia pulsante toocopy hello intera chiave e quindi incollarlo in questo gateway di hello tooregister finestra.</span><span class="sxs-lookup"><span data-stu-id="da962-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="da962-150">In caso contrario, ricreare il gateway di hello e ricominciare.</span><span class="sxs-lookup"><span data-stu-id="da962-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="da962-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-151">6. Problem</span></span>
<span data-ttu-id="da962-152">È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="da962-154">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-154">Cause</span></span>
<span data-ttu-id="da962-155">Questo errore potrebbe verificarsi perché hello gateway è stato eliminato o è stata rigenerata la chiave del gateway associato hello.</span><span class="sxs-lookup"><span data-stu-id="da962-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-156">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-156">Resolution</span></span>
<span data-ttu-id="da962-157">Se il gateway hello è stato eliminato, ricreare il gateway hello dal portale di hello, fare clic su **registrare**, copiare hello chiave dal portale di hello, incollare il codice e provare il gateway di hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="da962-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="da962-158">Se il gateway hello esiste ancora, ma è stata rigenerata la chiave, usare hello nuova chiave tooregister hello gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="da962-159">Se non si dispone di chiave hello, rigenerare la chiave hello nuovamente dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="da962-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="da962-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-160">7. Problem</span></span>
<span data-ttu-id="da962-161">Quando si sta registrando un gateway, potrebbe essere necessario tooenter percorso e la password di un certificato.</span><span class="sxs-lookup"><span data-stu-id="da962-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="da962-163">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-163">Cause</span></span>
<span data-ttu-id="da962-164">Hello gateway è stato registrato in altri computer prima di.</span><span class="sxs-lookup"><span data-stu-id="da962-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="da962-165">Durante la registrazione iniziale di hello del gateway, un certificato di crittografia è stato associato al gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="da962-166">certificato Hello può essere automatico generato dal gateway hello o specificato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="da962-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="da962-167">Questo certificato è usato tooencrypt le credenziali dell'archivio dati hello (servizio collegato).</span><span class="sxs-lookup"><span data-stu-id="da962-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Esportare il certificato](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="da962-169">Quando il ripristino di gateway hello in un computer host diverso, hello registrazione guidata per questo toodecrypt certificato credenziali precedentemente crittografati con questo certificato.</span><span class="sxs-lookup"><span data-stu-id="da962-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="da962-170">Senza questo certificato, credenziali hello non possono essere decrittografate dal nuovo gateway hello e associate a questo nuovo gateway esecuzioni di attività di copia successive avranno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="da962-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="da962-171">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-171">Resolution</span></span>
<span data-ttu-id="da962-172">Se è stata esportata certificato delle credenziali hello dal computer gateway originale hello utilizzando hello **esportare** pulsante hello **impostazioni** scheda in Data Management Gateway Configuration Manager, utilizzare hello certificato.</span><span class="sxs-lookup"><span data-stu-id="da962-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="da962-173">Non è possibile ignorare questo passaggio quando si recupera un gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="da962-174">Se il certificato di hello è presente, è necessario toodelete hello gateway dal portale hello e ricreare un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="da962-175">Inoltre, aggiornare tutti i servizi collegati che sono correlati toohello gateway da reinserimento le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="da962-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="da962-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-176">8. Problem</span></span>
<span data-ttu-id="da962-177">È possibile visualizzare hello seguente messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="da962-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="da962-178">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-178">Cause</span></span>
<span data-ttu-id="da962-179">Questo errore si verifica quando il gateway è in un ambiente che richiede un tooaccess proxy HTTP risorse Internet, o viene modificata la password di autenticazione del proxy, ma non viene aggiornata di conseguenza nel gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-180">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-180">Resolution</span></span>
<span data-ttu-id="da962-181">Seguire le istruzioni hello hello [considerazioni sui server Proxy](#proxy-server-considerations) sezione di questo articolo e configurare le impostazioni del proxy con dati Gestione Gateway di Gestione configurazione.</span><span class="sxs-lookup"><span data-stu-id="da962-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="da962-182">Il gateway è online con funzionalità limitate</span><span class="sxs-lookup"><span data-stu-id="da962-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="da962-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-183">1. Problem</span></span>
<span data-ttu-id="da962-184">Verranno visualizzati lo stato di hello del gateway hello online con funzionalità limitate.</span><span class="sxs-lookup"><span data-stu-id="da962-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="da962-185">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-185">Cause</span></span>
<span data-ttu-id="da962-186">È visualizzato lo stato di hello del gateway hello online con funzionalità limitate per uno dei seguenti motivi hello:</span><span class="sxs-lookup"><span data-stu-id="da962-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="da962-187">Gateway non è possibile connettersi toocloud servizio tramite il Bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="da962-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="da962-188">Servizio cloud non può connettersi toogateway tramite Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="da962-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="da962-189">Quando il gateway di hello è online con funzionalità limitate, potrebbe non essere in grado di toouse pipeline di dati toocreate di Data Factory Copia guidata hello per la copia dei dati tooor dagli archivi dati locali.</span><span class="sxs-lookup"><span data-stu-id="da962-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="da962-190">In alternativa, è possibile utilizzare l'Editor delle Data Factory nel portale di hello, Visual Studio o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da962-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-191">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-191">Resolution</span></span>
<span data-ttu-id="da962-192">Risoluzione di questo problema (online con funzionalità limitate) si basa sul se gateway hello non può connettersi toohello del servizio cloud o hello altro modo.</span><span class="sxs-lookup"><span data-stu-id="da962-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="da962-193">Hello le sezioni seguenti fornisce queste risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="da962-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="da962-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-194">2. Problem</span></span>
<span data-ttu-id="da962-195">Viene visualizzato il seguente errore hello.</span><span class="sxs-lookup"><span data-stu-id="da962-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway non è possibile connettersi toocloud servizio](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="da962-197">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-197">Cause</span></span>
<span data-ttu-id="da962-198">Gateway non è possibile connettersi servizio cloud toohello tramite Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="da962-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-199">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-199">Resolution</span></span>
<span data-ttu-id="da962-200">Seguire un gateway a questi hello tooget di passaggi in linea:</span><span class="sxs-lookup"><span data-stu-id="da962-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="da962-201">Consenti indirizzi IP regole in uscita sul computer del gateway hello e firewall aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="da962-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="da962-202">È possibile trovare gli indirizzi IP dal registro eventi di Windows hello (ID = = 401): è stato eseguito un tentativo effettuato tooaccess un socket in modo non è consentito dalle relative autorizzazioni di accesso XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="da962-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="da962-203">Configurare le impostazioni proxy nel gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="da962-204">Vedere hello [considerazioni sui server Proxy](#proxy-server-considerations) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="da962-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="da962-205">Abilitare le porte in uscita 5671 e 9350-9354 su entrambi hello Windows Firewall nel computer del gateway hello e firewall aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="da962-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="da962-206">Vedere hello [porte e firewall](#ports-and-firewall) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="da962-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="da962-207">Questo passaggio è facoltativo, ma consigliato per considerazioni relative alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="da962-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="da962-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="da962-208">3. Problem</span></span>
<span data-ttu-id="da962-209">Viene visualizzato il seguente errore hello.</span><span class="sxs-lookup"><span data-stu-id="da962-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="da962-210">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-210">Cause</span></span>
<span data-ttu-id="da962-211">Errore temporaneo nella connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="da962-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-212">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-212">Resolution</span></span>
<span data-ttu-id="da962-213">Seguire un gateway a questi hello tooget di passaggi in linea:</span><span class="sxs-lookup"><span data-stu-id="da962-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="da962-214">Attendere un paio di minuti, la connettività di hello verrà ripristinata automaticamente quando non viene più visualizzato errore hello.</span><span class="sxs-lookup"><span data-stu-id="da962-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="da962-215">Se hello errore persiste, riavviare il servizio gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="da962-216">Servizio non riuscite tooauthor collegato</span><span class="sxs-lookup"><span data-stu-id="da962-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="da962-217">Problema</span><span class="sxs-lookup"><span data-stu-id="da962-217">Problem</span></span>
<span data-ttu-id="da962-218">Si potrebbe essere visualizzato questo errore quando si tenta di toouse Gestione credenziali le credenziali di portale tooinput hello per un servizio collegato di nuovo o aggiornare le credenziali per un servizio collegato esistente.</span><span class="sxs-lookup"><span data-stu-id="da962-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="da962-219">Quando viene visualizzato questo errore, pagina Impostazioni hello di Data Management Gateway Configuration Manager potrebbe essere simile hello seguente schermata.</span><span class="sxs-lookup"><span data-stu-id="da962-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Impossibile raggiungere il database](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="da962-221">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-221">Cause</span></span>
<span data-ttu-id="da962-222">certificato SSL Hello possibile abbia perso nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="da962-223">Impossibile caricare il computer gateway Hello hello certificato attualmente utilizzato per la crittografia SSL.</span><span class="sxs-lookup"><span data-stu-id="da962-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="da962-224">È inoltre potrebbe essere visualizzato un messaggio di errore nel registro eventi di hello che è simile toohello seguente messaggio.</span><span class="sxs-lookup"><span data-stu-id="da962-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="da962-225">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-225">Resolution</span></span>
<span data-ttu-id="da962-226">Seguire questi problema hello toosolve di passaggi:</span><span class="sxs-lookup"><span data-stu-id="da962-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="da962-227">Avviare Gestione configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="da962-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="da962-228">Passare toohello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="da962-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="da962-229">Fare clic su hello **modifica** certificato SSL di hello toochange pulsante.</span><span class="sxs-lookup"><span data-stu-id="da962-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Pulsate Cambia per cambiare il certificato](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="da962-231">Selezionare un nuovo certificato come certificato SSL hello.</span><span class="sxs-lookup"><span data-stu-id="da962-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="da962-232">È possibile usare qualsiasi certificato SSL generato dall'utente o da qualsiasi organizzazione.</span><span class="sxs-lookup"><span data-stu-id="da962-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="da962-234">L'attività di copia ha esito negativo</span><span class="sxs-lookup"><span data-stu-id="da962-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="da962-235">Problema</span><span class="sxs-lookup"><span data-stu-id="da962-235">Problem</span></span>
<span data-ttu-id="da962-236">È possibile riscontrare hello seguito a un errore di "UserErrorFailedToConnectToSqlserver" dopo aver impostato una pipeline nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="da962-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="da962-237">Causa</span><span class="sxs-lookup"><span data-stu-id="da962-237">Cause</span></span>
<span data-ttu-id="da962-238">Questo problema può verificarsi per diversi motivi e la mitigazione varia di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="da962-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="da962-239">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="da962-239">Resolution</span></span>
<span data-ttu-id="da962-240">Consentire le connessioni TCP in uscita sulla porta TCP/1433 sul lato client di Gateway di gestione dati hello prima della connessione di database SQL tooan.</span><span class="sxs-lookup"><span data-stu-id="da962-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="da962-241">Se il database di destinazione hello è un database SQL di Azure, verificare SQL Server impostazioni del firewall per Azure nonché.</span><span class="sxs-lookup"><span data-stu-id="da962-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="da962-242">Vedere hello seguendo l'archivio di dati di sezione tootest hello connessione toohello locale.</span><span class="sxs-lookup"><span data-stu-id="da962-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="da962-243">Errori correlati alla connessione all'archivio dati o al driver</span><span class="sxs-lookup"><span data-stu-id="da962-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="da962-244">Se i dati visualizzati archiviare connessione o errori correlati al driver, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="da962-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="da962-245">Avviare Gestione configurazione di Gateway di gestione di dati nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="da962-246">Passare toohello **diagnostica** scheda.</span><span class="sxs-lookup"><span data-stu-id="da962-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="da962-247">In **Test connessione**, aggiungere i valori del gruppo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="da962-248">Fare clic su **Test** toosee se è possibile connettersi toohello locale origine dati dal computer del gateway hello utilizzando le informazioni di connessione hello e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="da962-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="da962-249">Se la connessione di prova hello non riesce dopo aver installato un driver, riavvio hello gateway per tale toopick modifica più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="da962-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Test connessione nella scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="da962-251">Log del gateway</span><span class="sxs-lookup"><span data-stu-id="da962-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="da962-252">Inviare tooMicrosoft registri gateway</span><span class="sxs-lookup"><span data-stu-id="da962-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="da962-253">Quando si contatta Guida tooget supporto alla risoluzione dei problemi del gateway, potrebbe essere necessario tooshare i registri del gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="da962-254">Con la versione di hello del gateway hello, è possibile condividere i log necessari gateway con due pulsanti in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="da962-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="da962-255">Passare toohello **diagnostica** scheda in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="da962-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Gateway di gestione dati - Scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="da962-257">Fare clic su **inviare i log** hello toosee seguendo la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="da962-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Gateway di gestione dati - Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="da962-259">(Facoltativo) Fare clic su **visualizzare log** tooreview registra nel Visualizzatore eventi hello.</span><span class="sxs-lookup"><span data-stu-id="da962-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="da962-260">(Facoltativo) Fare clic su **privacy** informativa sulla privacy dei servizi web di Microsoft tooreview.</span><span class="sxs-lookup"><span data-stu-id="da962-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="da962-261">Quando si è soddisfatti cosa si sta tooupload, fare clic su **inviare i log** tooactually inviare i log di hello dal hello ultimi sette giorni tooMicrosoft per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="da962-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="da962-262">Stato di hello dell'operazione di invio log hello verrà visualizzato come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="da962-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="da962-264">Al termine operazione hello, come illustrato nella seguente schermata hello è visualizzata una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="da962-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="da962-266">Salvare hello **ID Report** e condividerlo con il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da962-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="da962-267">ID report Hello è toolocate utilizzati registri del gateway hello caricato per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="da962-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="da962-268">ID report Hello viene salvato anche nel Visualizzatore eventi hello.</span><span class="sxs-lookup"><span data-stu-id="da962-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="da962-269">È possibile trovarlo esaminando l'ID evento hello "25" e verificare hello data e ora.</span><span class="sxs-lookup"><span data-stu-id="da962-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Gateway di gestione dati - ID report dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="da962-271">Archiviare i log del gateway nel computer host del gateway</span><span class="sxs-lookup"><span data-stu-id="da962-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="da962-272">Esistono dei casi in cui si verificano problemi con il gateway e non è possibile condividere direttamente i log del gateway:</span><span class="sxs-lookup"><span data-stu-id="da962-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="da962-273">Installare il gateway hello manualmente e registrare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="da962-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="da962-274">Si tenta di gateway hello tooregister con una chiave rigenerata in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="da962-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="da962-275">Si tenta di registri toosend e non è possibile connettere il servizio host di hello gateway.</span><span class="sxs-lookup"><span data-stu-id="da962-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="da962-276">In questi casi, è possibile salvare i log del gateway come file zip e condividerlo quando si contatta il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da962-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="da962-277">Ad esempio, se viene visualizzato un errore mentre si registra il gateway hello come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="da962-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Gateway di gestione dati - Errore di registrazione](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="da962-279">Fare clic su hello **archiviare log gateway** collegamento tooarchive e salvare i registri e quindi di condividere file con estensione zip hello con il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da962-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Gateway di gestione dati - Archivia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="da962-281">Trovare i log del gateway</span><span class="sxs-lookup"><span data-stu-id="da962-281">Locate gateway logs</span></span>
<span data-ttu-id="da962-282">Per informazioni dettagliate gateway log nei registri eventi di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="da962-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="da962-283">Avviare il **Visualizzatore eventi** di Windows.</span><span class="sxs-lookup"><span data-stu-id="da962-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="da962-284">Individuare i log in hello **registri applicazioni e servizi** > **Gateway di gestione dati** cartella.</span><span class="sxs-lookup"><span data-stu-id="da962-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="da962-285">Quando si sta risolvendo problemi relativi al gateway, cercare gli eventi a livello di errore nel Visualizzatore eventi hello.</span><span class="sxs-lookup"><span data-stu-id="da962-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Gateway di gestione dati - Log nel Visualizzatore eventi](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
