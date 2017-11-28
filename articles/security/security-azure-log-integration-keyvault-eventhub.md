---
title: registri aaaIntegrate dall'insieme di credenziali chiave di Azure tramite gli hub di eventi | Documenti Microsoft
description: Esercitazione hello necessarie toomake insieme di credenziali chiave registri disponibile tooa SIEM tramite l'integrazione di Log di Azure
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="39bda-103">Esercitazione sull'integrazione dei log di Azure: elaborazione degli eventi di Azure Key Vault tramite Hub eventi</span><span class="sxs-lookup"><span data-stu-id="39bda-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="39bda-104">È possibile utilizzare gli eventi registrati tooretrieve integrazione di Log di Azure e renderli disponibili tooyour sicurezza informazioni ed eventi (SIEM) sistema di gestione.</span><span class="sxs-lookup"><span data-stu-id="39bda-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="39bda-105">Questa esercitazione viene illustrato un esempio di come integrazione di Log di Azure può essere utilizzato tooprocess registri acquisite tramite hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="39bda-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="39bda-106">Utilizzare questa esercitazione tooget familiarità con la modalità di integrazione di Log di Azure e hub eventi lavoro insieme dal seguente hello procedure di esempio e comprensione del modo in cui ogni passaggio supporta soluzioni hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="39bda-107">Quindi è possibile eseguire ciò che si è appreso qui toocreate proprio toosupport passaggi requisiti univoci della società.</span><span class="sxs-lookup"><span data-stu-id="39bda-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="39bda-108">Hello passaggi e comandi in questa esercitazione non sono previsti toobe copiati e incollati.</span><span class="sxs-lookup"><span data-stu-id="39bda-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="39bda-109">Si tratta solo di esempi.</span><span class="sxs-lookup"><span data-stu-id="39bda-109">They're examples only.</span></span> <span data-ttu-id="39bda-110">Non utilizzare i comandi di PowerShell hello "così com'è" nell'ambiente in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="39bda-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="39bda-111">in quanto devono essere personalizzati in base all'ambiente univoco.</span><span class="sxs-lookup"><span data-stu-id="39bda-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="39bda-112">In questa esercitazione viene illustrato il processo di hello di recupero di hub di eventi registrati tooan attività insieme credenziali chiavi Azure e rende disponibile come sistema SIEM tooyour file JSON.</span><span class="sxs-lookup"><span data-stu-id="39bda-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="39bda-113">È quindi possibile configurare i file JSON di SIEM sistema tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="39bda-114">La maggior parte dei passaggi di hello in questa esercitazione implica la configurazione di insiemi di credenziali chiave, gli account di archiviazione e gli hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="39bda-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="39bda-115">passaggi per l'integrazione di Log di Azure specifici Hello sono alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="39bda-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="39bda-116">Non eseguire questi passaggi in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="39bda-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="39bda-117">Sono concepiti solo per un ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="39bda-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="39bda-118">Prima di utilizzarli nell'ambiente di produzione, è necessario personalizzare i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="39bda-119">Informazioni fornite lungo hello modo consente che comprendere motivazioni hello alla base di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="39bda-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="39bda-120">Gli articoli tooother collegamenti forniscono maggiori dettagli su determinati argomenti.</span><span class="sxs-lookup"><span data-stu-id="39bda-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="39bda-121">Per ulteriori informazioni sui servizi hello menzionato in questa esercitazione, vedere:</span><span class="sxs-lookup"><span data-stu-id="39bda-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="39bda-122">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="39bda-123">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="39bda-124">Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="39bda-125">Configurazione iniziale</span><span class="sxs-lookup"><span data-stu-id="39bda-125">Initial setup</span></span>

<span data-ttu-id="39bda-126">Prima di poter completare i passaggi di hello in questo articolo, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="39bda-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="39bda-127">Una sottoscrizione di Azure e l'account per tale sottoscrizione con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="39bda-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="39bda-128">Se non si ha una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="39bda-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="39bda-129">Un sistema con accesso toohello internet che soddisfa i requisiti di hello per l'installazione di integrazione di Log di Azure.</span><span class="sxs-lookup"><span data-stu-id="39bda-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="39bda-130">sistema Hello può trovarsi su un servizio cloud oppure ospitato in locale.</span><span class="sxs-lookup"><span data-stu-id="39bda-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="39bda-131">[Integrazione dei log di Azure](https://www.microsoft.com/download/details.aspx?id=53324) installato.</span><span class="sxs-lookup"><span data-stu-id="39bda-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="39bda-132">tooinstall è:</span><span class="sxs-lookup"><span data-stu-id="39bda-132">tooinstall it:</span></span>

   <span data-ttu-id="39bda-133">a.</span><span class="sxs-lookup"><span data-stu-id="39bda-133">a.</span></span> <span data-ttu-id="39bda-134">Utilizzare Desktop remoto tooconnect toohello sistema indicato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="39bda-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="39bda-135">b.</span><span class="sxs-lookup"><span data-stu-id="39bda-135">b.</span></span> <span data-ttu-id="39bda-136">Copiare sistema toohello programma di installazione di hello integrazione di Log di Azure.</span><span class="sxs-lookup"><span data-stu-id="39bda-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="39bda-137">È possibile [scaricare il file di installazione di hello](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="39bda-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="39bda-138">c.</span><span class="sxs-lookup"><span data-stu-id="39bda-138">c.</span></span> <span data-ttu-id="39bda-139">Avviare Installazione guidata di hello e accettazione delle condizioni di licenza Software Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="39bda-140">d.</span><span class="sxs-lookup"><span data-stu-id="39bda-140">d.</span></span> <span data-ttu-id="39bda-141">Se si fornisce informazioni di telemetria, lasciare selezionata hello casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="39bda-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="39bda-142">Se invece non inviare tooMicrosoft informazioni sull'utilizzo, deselezionare la casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="39bda-143">Per ulteriori informazioni sull'integrazione di Log di Azure e come tooinstall, vedere [integrazione di Log di Azure con la registrazione di diagnostica di Azure e l'inoltro degli eventi di Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39bda-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="39bda-144">Hello PowerShell più recente.</span><span class="sxs-lookup"><span data-stu-id="39bda-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="39bda-145">Se è installato Windows Server 2016 e la versione disponibile di PowerShell è almeno la versione 5.0.</span><span class="sxs-lookup"><span data-stu-id="39bda-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="39bda-146">Se si usa qualsiasi altra versione di Windows Server, l'utente potrebbe aver installato una versione precedente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39bda-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="39bda-147">È possibile controllare la versione hello immettendo ```get-host``` in una finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39bda-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="39bda-148">Se PowerShell 5.0 non è installato, è possibile [scaricarlo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="39bda-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="39bda-149">Dopo aver creato almeno PowerShell 5.0, è possibile passare una versione più recente di tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="39bda-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="39bda-150">a.</span><span class="sxs-lookup"><span data-stu-id="39bda-150">a.</span></span> <span data-ttu-id="39bda-151">In una finestra di PowerShell, immettere hello ```Install-Module Azure``` comando.</span><span class="sxs-lookup"><span data-stu-id="39bda-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="39bda-152">Completare i passaggi di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="39bda-153">b.</span><span class="sxs-lookup"><span data-stu-id="39bda-153">b.</span></span> <span data-ttu-id="39bda-154">Immettere hello ```Install-Module AzureRM``` comando.</span><span class="sxs-lookup"><span data-stu-id="39bda-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="39bda-155">Completare i passaggi di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="39bda-156">Per altre informazioni, vedere [Installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="39bda-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="39bda-157">Creare elementi dell'infrastruttura di supporto</span><span class="sxs-lookup"><span data-stu-id="39bda-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="39bda-158">Aprire una finestra di PowerShell con privilegi elevata e passare troppo**C:\Program Files\Microsoft Azure Log integrazione**.</span><span class="sxs-lookup"><span data-stu-id="39bda-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="39bda-159">Importare i cmdlet AzLog hello eseguendo script hello LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="39bda-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="39bda-160">Immettere hello `.\LoadAzLogModule.ps1` comando.</span><span class="sxs-lookup"><span data-stu-id="39bda-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="39bda-161">(Hello notifica ". \" in quel comando.) Verrà visualizzata una schermata analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="39bda-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Elenco dei moduli caricati](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="39bda-163">Immettere hello `Login-AzureRmAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="39bda-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="39bda-164">Nella finestra di accesso hello, immettere le informazioni sulle credenziali hello per sottoscrizione hello che verrà utilizzato per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="39bda-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="39bda-165">Se si tratta hello prima volta che ci si connette in tooAzure da questo computer, si verrà visualizzato un messaggio su come consentire i dati di utilizzo di PowerShell toocollect Microsoft.</span><span class="sxs-lookup"><span data-stu-id="39bda-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="39bda-166">È consigliabile abilitare questa raccolta di dati in quanto sarà tooimprove usato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39bda-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="39bda-167">Dopo l'autenticazione, si è connessi e visualizzati informazioni hello in hello seguente schermata.</span><span class="sxs-lookup"><span data-stu-id="39bda-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="39bda-168">Prendere nota del nome della sottoscrizione hello ID e la sottoscrizione, poiché sarà necessario toocomplete i passaggi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="39bda-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Finestra di PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="39bda-170">Creare variabili valori toostore che verranno utilizzati in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="39bda-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="39bda-171">Immettere ogni hello seguendo le linee di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39bda-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="39bda-172">Potrebbe essere necessario tooadjust hello valori toomatch l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="39bda-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="39bda-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` Il nome della sottoscrizione potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="39bda-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="39bda-174">È possibile visualizzarlo come parte dell'output di hello del comando precedente hello.)</span><span class="sxs-lookup"><span data-stu-id="39bda-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="39bda-175">```$location = 'West US'```(Questa variabile è il percorso di hello toopass utilizzati in cui le risorse devono essere create.</span><span class="sxs-lookup"><span data-stu-id="39bda-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="39bda-176">È possibile modificare questa variabile toobe qualsiasi posizione di propria scelta.)</span><span class="sxs-lookup"><span data-stu-id="39bda-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="39bda-177">``` $name = 'azlogtest' + $random```(possibile scegliere qualsiasi nome hello, ma deve includere solo lettere minuscole e numeri).</span><span class="sxs-lookup"><span data-stu-id="39bda-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="39bda-178">``` $storageName = $name```(Verrà utilizzata questa variabile per il nome di account di archiviazione hello).</span><span class="sxs-lookup"><span data-stu-id="39bda-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="39bda-179">```$rgname = $name ```(Verrà utilizzata questa variabile per nome gruppo di risorse hello).</span><span class="sxs-lookup"><span data-stu-id="39bda-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="39bda-180">``` $eventHubNameSpaceName = $name```(Si tratta di nome hello dello spazio dei nomi di hub eventi hello).</span><span class="sxs-lookup"><span data-stu-id="39bda-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="39bda-181">Specificare una sottoscrizione di hello che verranno usate con:</span><span class="sxs-lookup"><span data-stu-id="39bda-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="39bda-182">Creare un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="39bda-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="39bda-183">Se si immette `$rg` a questo punto, dovrebbe essere simile schermata di toothis output:</span><span class="sxs-lookup"><span data-stu-id="39bda-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Output dopo la creazione di un gruppo di risorse](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="39bda-185">Creare un account di archiviazione che verrà utilizzato tookeep traccia delle informazioni sullo stato:</span><span class="sxs-lookup"><span data-stu-id="39bda-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="39bda-186">Creare spazio dei nomi hub di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-186">Create hello event hub namespace.</span></span> <span data-ttu-id="39bda-187">Questo è necessario toocreate un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="39bda-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="39bda-188">Ottenere l'ID regola hello che verrà utilizzato con il provider di insights hello:</span><span class="sxs-lookup"><span data-stu-id="39bda-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="39bda-189">Ottenere tutti i possibili percorsi di Azure e aggiungere hello nomi tooa variabile può essere utilizzato in un passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="39bda-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="39bda-190">a.</span><span class="sxs-lookup"><span data-stu-id="39bda-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="39bda-191">b.</span><span class="sxs-lookup"><span data-stu-id="39bda-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="39bda-192">Se si immette `$locations` a questo punto, verranno visualizzati i nomi di percorso di hello senza informazioni aggiuntive di hello restituite da Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="39bda-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="39bda-193">Creare un profilo di log di Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="39bda-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="39bda-194">Per ulteriori informazioni su hello profilo log di Azure, vedere [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="39bda-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="39bda-195">È possibile che venga visualizzato un messaggio di errore quando si tenta di toocreate un profilo di log.</span><span class="sxs-lookup"><span data-stu-id="39bda-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="39bda-196">È quindi possibile controllare la documentazione di hello per Get-AzureRmLogProfile e Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="39bda-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="39bda-197">Se si esegue Get AzureRmLogProfile, vedrai informazioni sul profilo log hello.</span><span class="sxs-lookup"><span data-stu-id="39bda-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="39bda-198">È possibile eliminare il profilo di log esistente hello immettendo hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.</span><span class="sxs-lookup"><span data-stu-id="39bda-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Errore del profilo di Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="39bda-200">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="39bda-200">Create a key vault</span></span>

1. <span data-ttu-id="39bda-201">Creare l'insieme di credenziali chiave di hello:</span><span class="sxs-lookup"><span data-stu-id="39bda-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="39bda-202">Configurare la registrazione per l'insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="39bda-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="39bda-203">Generare l'attività di log</span><span class="sxs-lookup"><span data-stu-id="39bda-203">Generate log activity</span></span>

<span data-ttu-id="39bda-204">Le richieste devono toobe inviati tooKey attività del log toogenerate insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="39bda-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="39bda-205">Azioni quali la generazione di chiavi, l'archiviazione di segreti o la lettura di segreti da Key Vault creeranno le voci dei log.</span><span class="sxs-lookup"><span data-stu-id="39bda-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="39bda-206">Visualizzare le chiavi di archiviazione corrente hello:</span><span class="sxs-lookup"><span data-stu-id="39bda-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="39bda-207">Generare un nuovo **key2**:</span><span class="sxs-lookup"><span data-stu-id="39bda-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="39bda-208">Visualizzare nuovamente le chiavi di hello e verificare che **key2** contiene un valore diverso:</span><span class="sxs-lookup"><span data-stu-id="39bda-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="39bda-209">Impostare e leggere un segreto toogenerate voci di log aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="39bda-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="39bda-210">a.</span><span class="sxs-lookup"><span data-stu-id="39bda-210">a.</span></span> <span data-ttu-id="39bda-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="39bda-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segreto restituito](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="39bda-213">Configurare Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="39bda-214">Dopo aver configurato tutti hello elementi obbligatori toohave registrazione insieme credenziali chiavi tooan hub eventi, è necessario tooconfigure integrazione di Log di Azure:</span><span class="sxs-lookup"><span data-stu-id="39bda-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="39bda-215">Eseguire il comando AzLog hello per ogni hub eventi:</span><span class="sxs-lookup"><span data-stu-id="39bda-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="39bda-216">Dopo un minuto e dell'esecuzione hello ultimi due comandi, verrà visualizzato il file JSON generati.</span><span class="sxs-lookup"><span data-stu-id="39bda-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="39bda-217">È possibile confermare che il monitoraggio directory hello **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="39bda-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39bda-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39bda-218">Next steps</span></span>

- [<span data-ttu-id="39bda-219">Domande frequenti su Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="39bda-220">Introduzione all'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="39bda-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="39bda-221">Integrare i log delle risorse di Azure nei sistemi SIEM</span><span class="sxs-lookup"><span data-stu-id="39bda-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
