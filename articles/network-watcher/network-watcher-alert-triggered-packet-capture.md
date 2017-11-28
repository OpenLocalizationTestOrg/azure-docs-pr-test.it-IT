---
title: con le funzioni di Azure e gli avvisi di monitoraggio di rete aaaUse pacchetto acquisizione toodo proattiva | Documenti Microsoft
description: In questo articolo viene descritto come un avviso toocreate attivata acquisizione pacchetto con il Watcher di rete di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="32493-103">Usare l'acquisizione di pacchetti per il monitoraggio proattivo della rete con avvisi e Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="32493-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="32493-104">Acquisizione di pacchetti di rete controllo crea le sessioni di acquisizione tootrack traffico da e verso le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="32493-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="32493-105">Hello file di acquisizione può avere un filtro definito tootrack hello solo il traffico che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="32493-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="32493-106">Questi dati vengono quindi archiviati in un blob di archiviazione o in locale nella macchina guest hello.</span><span class="sxs-lookup"><span data-stu-id="32493-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="32493-107">Questa funzionalità può essere avviata in remoto da altri scenari di automazione, ad esempio Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="32493-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="32493-108">Consente di acquisizione di pacchetti a che Hello proattiva acquisizioni toorun funzionalità in base definito anomalie di rete.</span><span class="sxs-lookup"><span data-stu-id="32493-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="32493-109">Altri utilizzi comprendono la raccolta di statistiche di rete, l'ottenimento di informazioni sulle intrusioni nella rete, il debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="32493-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="32493-110">Le risorse distribuite in Azure sono in esecuzione 24 ore su 24, 7 giorni su 7.</span><span class="sxs-lookup"><span data-stu-id="32493-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="32493-111">I tecnici non è possibile monitorare attivamente lo stato di hello di tutte le risorse 24/7.</span><span class="sxs-lookup"><span data-stu-id="32493-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="32493-112">Si pensi a cosa può accadere se si verifica un problema alle 2 del mattino.</span><span class="sxs-lookup"><span data-stu-id="32493-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="32493-113">Utilizzando Watcher di rete, avvisi e funzioni dall'interno di hello ecosistema di Azure, è possibile in modo proattivo rispondere con problemi di toosolve hello strumenti e i dati nella rete.</span><span class="sxs-lookup"><span data-stu-id="32493-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Scenario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="32493-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32493-115">Prerequisites</span></span>

* <span data-ttu-id="32493-116">versione più recente di Hello di [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="32493-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="32493-117">Un'istanza esistente di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="32493-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="32493-118">Se non è già presente, creare un'[istanza di Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="32493-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="32493-119">Una macchina virtuale esistente in hello stessa area Watcher di rete con hello [estensione Windows](../virtual-machines/windows/extensions-nwa.md) o [estensione della macchina virtuale Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="32493-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="32493-120">Scenario</span><span class="sxs-lookup"><span data-stu-id="32493-120">Scenario</span></span>

<span data-ttu-id="32493-121">In questo esempio, la macchina virtuale invia più segmenti TCP superiore al normale e si desidera toobe un avviso.</span><span class="sxs-lookup"><span data-stu-id="32493-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="32493-122">Come esempio qui vengono usati i segmenti TCP, ma è possibile usare qualsiasi condizione di avviso.</span><span class="sxs-lookup"><span data-stu-id="32493-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="32493-123">Quando viene generato un avviso, è opportuno tooreceive toounderstand di dati a livello di pacchetto perché la comunicazione è è aumentato.</span><span class="sxs-lookup"><span data-stu-id="32493-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="32493-124">È quindi possibile eseguire passaggi comunicazione tooregular della macchina virtuale tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="32493-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="32493-125">Questo scenario presuppone che esistano già un'istanza di Network Watcher e un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="32493-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="32493-126">Hello seguente elenco viene fornita una panoramica del flusso di lavoro hello che ha luogo:</span><span class="sxs-lookup"><span data-stu-id="32493-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="32493-127">Nella macchina virtuale viene attivato un avviso.</span><span class="sxs-lookup"><span data-stu-id="32493-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="32493-128">avviso di Hello chiama la funzione di Azure tramite un webhook.</span><span class="sxs-lookup"><span data-stu-id="32493-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="32493-129">La funzione Azure elabora avviso hello e avvia una sessione di acquisizione pacchetto Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="32493-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="32493-130">acquisizione di pacchetti Hello viene eseguito su hello VM e raccoglie il traffico.</span><span class="sxs-lookup"><span data-stu-id="32493-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="32493-131">Hello file di acquisizione pacchetto viene caricato tooa account di archiviazione per la revisione e la diagnosi.</span><span class="sxs-lookup"><span data-stu-id="32493-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="32493-132">tooautomate questo processo, viene creata e la connessione di un avviso nel nostro tootrigger VM quando si verifica l'evento imprevisto di hello.</span><span class="sxs-lookup"><span data-stu-id="32493-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="32493-133">È inoltre possibile creare toocall una funzione in Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="32493-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="32493-134">Questo scenario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="32493-134">This scenario does hello following:</span></span>

* <span data-ttu-id="32493-135">Crea una funzione di Azure che avvia un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="32493-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="32493-136">Crea una regola di avviso in una macchina virtuale e configura hello toocall di regola di avviso hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="32493-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="32493-137">Creare una funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="32493-137">Create an Azure function</span></span>

<span data-ttu-id="32493-138">primo passaggio Hello è toocreate un avviso di hello tooprocess funzione Azure e creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="32493-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="32493-139">In hello [portale di Azure](https://portal.azure.com)selezionare **New** > **calcolo** > **funzione App**.</span><span class="sxs-lookup"><span data-stu-id="32493-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Creazione di un'app per le funzioni][1-1]

2. <span data-ttu-id="32493-141">In hello **funzione App** pannello, immettere i seguenti valori hello e quindi selezionare **OK** toocreate hello app:</span><span class="sxs-lookup"><span data-stu-id="32493-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="32493-142">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="32493-142">**Setting**</span></span> | <span data-ttu-id="32493-143">**Valore**</span><span class="sxs-lookup"><span data-stu-id="32493-143">**Value**</span></span> | <span data-ttu-id="32493-144">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="32493-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="32493-145">**Nome app**</span><span class="sxs-lookup"><span data-stu-id="32493-145">**App name**</span></span>|<span data-ttu-id="32493-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="32493-146">PacketCaptureExample</span></span>|<span data-ttu-id="32493-147">nome Hello di hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="32493-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="32493-148">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="32493-148">**Subscription**</span></span>|<span data-ttu-id="32493-149">[La sottoscrizione] hello sottoscrizione per le app di funzione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="32493-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="32493-150">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="32493-150">**Resource Group**</span></span>|<span data-ttu-id="32493-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="32493-151">PacketCaptureRG</span></span>|<span data-ttu-id="32493-152">Hello risorsa gruppo toocontain hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="32493-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="32493-153">**Piano di hosting**</span><span class="sxs-lookup"><span data-stu-id="32493-153">**Hosting Plan**</span></span>|<span data-ttu-id="32493-154">Piano a consumo</span><span class="sxs-lookup"><span data-stu-id="32493-154">Consumption Plan</span></span>| <span data-ttu-id="32493-155">tipo Hello di pianificare l'applicazione utilizzi (funzione).</span><span class="sxs-lookup"><span data-stu-id="32493-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="32493-156">Le opzioni sono Consumo e Piano di servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="32493-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="32493-157">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="32493-157">**Location**</span></span>|<span data-ttu-id="32493-158">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="32493-158">Central US</span></span>| <span data-ttu-id="32493-159">area Hello nella quale app di funzione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="32493-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="32493-160">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="32493-160">**Storage Account**</span></span>|<span data-ttu-id="32493-161">{generato automaticamente}</span><span class="sxs-lookup"><span data-stu-id="32493-161">{autogenerated}</span></span>| <span data-ttu-id="32493-162">account di archiviazione Hello necessarie funzioni di Azure per l'archiviazione di uso generale.</span><span class="sxs-lookup"><span data-stu-id="32493-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="32493-163">In hello **PacketCaptureExample funzione app** pannello seleziona **funzioni** > **funzione personalizzata**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="32493-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="32493-164">Selezionare **HttpTrigger Powershell**, quindi immettere hello rimanenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="32493-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="32493-165">Infine, toocreate hello funzione, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="32493-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="32493-166">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="32493-166">**Setting**</span></span> | <span data-ttu-id="32493-167">**Valore**</span><span class="sxs-lookup"><span data-stu-id="32493-167">**Value**</span></span> | <span data-ttu-id="32493-168">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="32493-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="32493-169">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="32493-169">**Scenario**</span></span>|<span data-ttu-id="32493-170">Sperimentale</span><span class="sxs-lookup"><span data-stu-id="32493-170">Experimental</span></span>|<span data-ttu-id="32493-171">Tipo di scenario</span><span class="sxs-lookup"><span data-stu-id="32493-171">Type of scenario</span></span>|
    |<span data-ttu-id="32493-172">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="32493-172">**Name your function**</span></span>|<span data-ttu-id="32493-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="32493-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="32493-174">Nome della funzione hello</span><span class="sxs-lookup"><span data-stu-id="32493-174">Name of hello function</span></span>|
    |<span data-ttu-id="32493-175">**Livello di autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="32493-175">**Authorization level**</span></span>|<span data-ttu-id="32493-176">Funzione</span><span class="sxs-lookup"><span data-stu-id="32493-176">Function</span></span>|<span data-ttu-id="32493-177">Livello di autorizzazione per la funzione hello</span><span class="sxs-lookup"><span data-stu-id="32493-177">Authorization level for hello function</span></span>|

![Esempio di funzioni][functions1]

> [!NOTE]
> <span data-ttu-id="32493-179">modello di PowerShell Hello è sperimentale e non dispone del supporto completo.</span><span class="sxs-lookup"><span data-stu-id="32493-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="32493-180">Le personalizzazioni sono necessari per questo esempio e vengono spiegate in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="32493-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="32493-181">Aggiungere moduli</span><span class="sxs-lookup"><span data-stu-id="32493-181">Add modules</span></span>

<span data-ttu-id="32493-182">cmdlet di PowerShell Watcher di rete, toouse caricare hello app più recente di PowerShell modulo toohello (funzione).</span><span class="sxs-lookup"><span data-stu-id="32493-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="32493-183">Nel computer locale con hello più recente di Azure PowerShell i moduli installati, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="32493-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="32493-184">In questo modo di esempio hello percorso locale dei moduli di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32493-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="32493-185">Queste cartelle verranno usate in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="32493-185">These folders are used in a later step.</span></span> <span data-ttu-id="32493-186">i moduli di Hello che vengono utilizzati in questo scenario sono:</span><span class="sxs-lookup"><span data-stu-id="32493-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="32493-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="32493-187">AzureRM.Network</span></span>

    * <span data-ttu-id="32493-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="32493-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="32493-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="32493-189">AzureRM.Resources</span></span>

    ![Cartelle di PowerShell][functions5]

1. <span data-ttu-id="32493-191">Selezionare **funzione impostazioni app** > **passare tooApp servizio Editor**.</span><span class="sxs-lookup"><span data-stu-id="32493-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Impostazioni dell'app per le funzioni][functions2]

1. <span data-ttu-id="32493-193">Pulsante destro del mouse hello **AlertPacketCapturePowershell** cartella, quindi creare una cartella denominata **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="32493-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="32493-194">Creare una sottocartella per ogni modulo necessario.</span><span class="sxs-lookup"><span data-stu-id="32493-194">Create a subfolder for each module that you need.</span></span>

    ![Cartelle e sottocartelle][functions3]

    * <span data-ttu-id="32493-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="32493-196">AzureRM.Network</span></span>

    * <span data-ttu-id="32493-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="32493-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="32493-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="32493-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="32493-199">Pulsante destro del mouse hello **AzureRM.Network** sottocartella e quindi selezionare **Carica file**.</span><span class="sxs-lookup"><span data-stu-id="32493-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="32493-200">Passare tooyour Azure i moduli.</span><span class="sxs-lookup"><span data-stu-id="32493-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="32493-201">Hello locale **AzureRM.Network** cartella, selezionare tutti i file hello nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="32493-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="32493-202">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="32493-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="32493-203">Ripetere questi passaggi per **AzureRM.Profile** e **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="32493-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Caricare file][functions6]

1. <span data-ttu-id="32493-205">Dopo aver completato, ogni cartella deve disporre di file di modulo di PowerShell hello dal computer locale.</span><span class="sxs-lookup"><span data-stu-id="32493-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![File di PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="32493-207">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="32493-207">Authentication</span></span>

<span data-ttu-id="32493-208">i cmdlet di PowerShell toouse hello, è necessario eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="32493-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="32493-209">Configurare l'autenticazione nell'app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="32493-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="32493-210">l'autenticazione tooconfigure, è necessario configurare le variabili di ambiente e caricare un'app di funzione toohello file della chiave crittografata.</span><span class="sxs-lookup"><span data-stu-id="32493-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="32493-211">Questo scenario fornisce solo un esempio di come l'autenticazione tooimplement con le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="32493-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="32493-212">Esistono altri modi toodo questo.</span><span class="sxs-lookup"><span data-stu-id="32493-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="32493-213">Credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="32493-213">Encrypted credentials</span></span>

<span data-ttu-id="32493-214">Hello lo script di PowerShell seguente crea un file di chiave denominato **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="32493-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="32493-215">Fornisce inoltre una versione crittografata della password hello fornito.</span><span class="sxs-lookup"><span data-stu-id="32493-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="32493-216">Questa password è hello stessa password definita per un'applicazione hello Azure Active Directory che viene utilizzata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="32493-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="32493-217">Nell'Editor di servizio App di app di funzione hello hello, creare una cartella denominata **chiavi** in **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="32493-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="32493-218">Caricare quindi hello **PassEncryptKey.key** file creato nel precedente esempio di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="32493-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Chiave delle funzioni][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="32493-220">Recuperare i valori per le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="32493-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="32493-221">requisito finale Hello è tooset variabili di ambiente hello che sono valori hello tooaccess necessarie per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="32493-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="32493-222">Hello elenco seguente mostra le variabili di ambiente hello creati:</span><span class="sxs-lookup"><span data-stu-id="32493-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="32493-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="32493-223">AzureClientID</span></span>

* <span data-ttu-id="32493-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="32493-224">AzureTenant</span></span>

* <span data-ttu-id="32493-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="32493-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="32493-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="32493-226">AzureClientID</span></span>

<span data-ttu-id="32493-227">ID client hello è hello ID applicazione di un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32493-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="32493-228">Se si dispone già di un'applicazione toouse, eseguire un'applicazione hello toocreate riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="32493-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="32493-229">password di Hello utilizzati durante la creazione di un'applicazione hello deve essere hello stessa password creato in precedenza durante il salvataggio dei file di chiave hello.</span><span class="sxs-lookup"><span data-stu-id="32493-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="32493-230">Nel portale di Azure hello, selezionare **sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="32493-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="32493-231">Selezionare hello toouse di sottoscrizione, quindi **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="32493-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![IAM delle funzioni][functions9]

1. <span data-ttu-id="32493-233">Scegliere toouse account hello e quindi selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="32493-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="32493-234">Copiare l'ID applicazione hello</span><span class="sxs-lookup"><span data-stu-id="32493-234">Copy hello Application ID.</span></span>

    ![ID applicazione per le funzioni][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="32493-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="32493-236">AzureTenant</span></span>

<span data-ttu-id="32493-237">Ottenere l'ID tenant hello eseguendo hello seguente esempio di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="32493-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="32493-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="32493-238">AzureCredPassword</span></span>

<span data-ttu-id="32493-239">valore di Hello della variabile di ambiente AzureCredPassword hello è valore hello ottenute dall'esecuzione hello seguente esempio di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32493-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="32493-240">In questo esempio è hello corrisponde a quello illustrato nella precedente hello **le credenziali crittografate** sezione.</span><span class="sxs-lookup"><span data-stu-id="32493-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="32493-241">valore che è necessario Hello hello output di hello `$Encryptedpassword` variabile.</span><span class="sxs-lookup"><span data-stu-id="32493-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="32493-242">Si tratta di hello principale password del servizio che si è crittografato tramite script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="32493-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="32493-243">Archiviare le variabili di ambiente hello</span><span class="sxs-lookup"><span data-stu-id="32493-243">Store hello environment variables</span></span>

1. <span data-ttu-id="32493-244">Passare toohello funzione app.</span><span class="sxs-lookup"><span data-stu-id="32493-244">Go toohello function app.</span></span> <span data-ttu-id="32493-245">Selezionare quindi **Impostazioni dell'app per le funzioni** > **Configurare le impostazioni dell'app**.</span><span class="sxs-lookup"><span data-stu-id="32493-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configurare le impostazioni applicazione][functions11]

1. <span data-ttu-id="32493-247">Aggiungere le variabili di ambiente hello e le relative impostazioni di app toohello di valori e quindi selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="32493-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Impostazioni app][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="32493-249">Aggiungi funzione toohello di PowerShell</span><span class="sxs-lookup"><span data-stu-id="32493-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="32493-250">È in corso tempo toomake chiama Watcher di rete all'interno di hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="32493-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="32493-251">A seconda dei requisiti di hello, l'implementazione di hello di questa funzione può variare.</span><span class="sxs-lookup"><span data-stu-id="32493-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="32493-252">Tuttavia, il flusso generale di hello di codice hello è:</span><span class="sxs-lookup"><span data-stu-id="32493-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="32493-253">Elaborare i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="32493-253">Process input parameters.</span></span>
2. <span data-ttu-id="32493-254">Pacchetto esistente query acquisisce tooverify limiti e risolvere i conflitti di nome.</span><span class="sxs-lookup"><span data-stu-id="32493-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="32493-255">Creare un'acquisizione di pacchetti con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="32493-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="32493-256">Eseguire periodicamente il polling dell'acquisizione di pacchetti fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="32493-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="32493-257">Notifica utente hello che sessione di acquisizione di pacchetti hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="32493-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="32493-258">Hello esempio seguente il codice di PowerShell che può essere utilizzato nella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="32493-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="32493-259">Sono presenti valori che devono toobe sostituito per **subscriptionId**, **resourceGroupName**, e **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="32493-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="32493-260">Recuperare l'URL di hello (funzione)</span><span class="sxs-lookup"><span data-stu-id="32493-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="32493-261">Dopo aver creato la funzione, è possibile configurare l'URL di hello toocall avviso associato a funzione hello.</span><span class="sxs-lookup"><span data-stu-id="32493-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="32493-262">tooget questo valore, l'URL di funzione hello copia dall'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="32493-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![URL di individuazione hello (funzione)][functions13]

2. <span data-ttu-id="32493-264">Copia URL funzione hello per l'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="32493-264">Copy hello function URL for your function app.</span></span>

    ![Copia l'URL di hello (funzione)][2]

<span data-ttu-id="32493-266">Se si richiedono proprietà personalizzate nel payload hello della richiesta POST per hello webhook, fare riferimento troppo[configurare un webhook su un avviso di metrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="32493-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="32493-267">Configurare un avviso in una VM</span><span class="sxs-lookup"><span data-stu-id="32493-267">Configure an alert on a VM</span></span>

<span data-ttu-id="32493-268">Gli avvisi possono essere singoli utenti configurato toonotify quando una metrica specifica supera una soglia assegnato tooit.</span><span class="sxs-lookup"><span data-stu-id="32493-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="32493-269">In questo esempio è di avviso hello in hello segmenti TCP inviati, ma hello avviso può essere attivato per molte altre metriche.</span><span class="sxs-lookup"><span data-stu-id="32493-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="32493-270">In questo esempio, un avviso è configurata toocall una funzione di hello toocall webhook.</span><span class="sxs-lookup"><span data-stu-id="32493-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="32493-271">Creare una regola di avviso hello</span><span class="sxs-lookup"><span data-stu-id="32493-271">Create hello alert rule</span></span>

<span data-ttu-id="32493-272">Macchina virtuale esistente tooan go e quindi aggiungere una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="32493-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="32493-273">Per informazioni più dettagliate sulla configurazione di avvisi, vedere [Creazione di avvisi in Monitoraggio di Azure per i servizi Azure - Portale di Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32493-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="32493-274">Immettere i seguenti valori hello hello **regola di avviso** blade e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="32493-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="32493-275">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="32493-275">**Setting**</span></span> | <span data-ttu-id="32493-276">**Valore**</span><span class="sxs-lookup"><span data-stu-id="32493-276">**Value**</span></span> | <span data-ttu-id="32493-277">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="32493-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="32493-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="32493-278">**Name**</span></span>|<span data-ttu-id="32493-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="32493-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="32493-280">Nome della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="32493-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="32493-281">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="32493-281">**Description**</span></span>|<span data-ttu-id="32493-282">Soglia superata segmenti TCP inviati</span><span class="sxs-lookup"><span data-stu-id="32493-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="32493-283">descrizione di Hello per regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="32493-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="32493-284">**Metrica**</span><span class="sxs-lookup"><span data-stu-id="32493-284">**Metric**</span></span>|<span data-ttu-id="32493-285">Segmenti TCP inviati</span><span class="sxs-lookup"><span data-stu-id="32493-285">TCP segments sent</span></span>| <span data-ttu-id="32493-286">Hello toouse metrica tootrigger hello dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="32493-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="32493-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="32493-287">**Condition**</span></span>|<span data-ttu-id="32493-288">Maggiore di</span><span class="sxs-lookup"><span data-stu-id="32493-288">Greater than</span></span>| <span data-ttu-id="32493-289">Hello toouse condizione durante la valutazione della metrica hello.</span><span class="sxs-lookup"><span data-stu-id="32493-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="32493-290">**Soglia**</span><span class="sxs-lookup"><span data-stu-id="32493-290">**Threshold**</span></span>|<span data-ttu-id="32493-291">100</span><span class="sxs-lookup"><span data-stu-id="32493-291">100</span></span>| <span data-ttu-id="32493-292">valore di Hello della metrica hello che Attiva avviso hello.</span><span class="sxs-lookup"><span data-stu-id="32493-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="32493-293">Questo valore deve essere impostato tooa valore valido per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="32493-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="32493-294">**Periodo**</span><span class="sxs-lookup"><span data-stu-id="32493-294">**Period**</span></span>|<span data-ttu-id="32493-295">Su hello ultimi 5 minuti</span><span class="sxs-lookup"><span data-stu-id="32493-295">Over hello last five minutes</span></span>| <span data-ttu-id="32493-296">Determina il periodo di hello in cui toolook per soglia hello in metrica hello.</span><span class="sxs-lookup"><span data-stu-id="32493-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="32493-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="32493-297">**Webhook**</span></span>|<span data-ttu-id="32493-298">[URL webhook dell'app per le funzioni]</span><span class="sxs-lookup"><span data-stu-id="32493-298">[webhook URL from function app]</span></span>| <span data-ttu-id="32493-299">URL del webhook Hello da app di funzione hello creato nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="32493-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="32493-300">metrica di segmenti TCP Hello non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="32493-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="32493-301">Per ulteriori informazioni su tooenable altre metriche visitando [attivazione del monitoraggio e diagnostica](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="32493-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="32493-302">Esaminare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="32493-302">Review hello results</span></span>

<span data-ttu-id="32493-303">Dopo aver criteri hello per i trigger di avviso hello, viene creata un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="32493-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="32493-304">Passare tooNetwork controllo e quindi selezionare **acquisizione pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="32493-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="32493-305">In questa pagina, è possibile selezionare hello acquisizione file collegamento toodownload hello pacchetto acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="32493-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Visualizzare l'acquisizione di pacchetti][functions14]

<span data-ttu-id="32493-307">Se il file di acquisizione hello è archiviato in locale, è possibile recuperare, effettuando l'accesso alla macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="32493-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="32493-308">Per istruzioni relative al download di file dagli account di archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="32493-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="32493-309">Un altro strumento è [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="32493-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="32493-310">Dopo il download dell'acquisizione, è possibile visualizzarla con qualsiasi strumento per la lettura di un file **.cap**.</span><span class="sxs-lookup"><span data-stu-id="32493-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="32493-311">Di seguito sono collegamenti tootwo di questi strumenti:</span><span class="sxs-lookup"><span data-stu-id="32493-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="32493-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="32493-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="32493-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="32493-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="32493-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32493-314">Next steps</span></span>

<span data-ttu-id="32493-315">Informazioni su come tooview acquisisce il pacchetto, visitare il sito [analysis acquisizione pacchetto con Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="32493-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
