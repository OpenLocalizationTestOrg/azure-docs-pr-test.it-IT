---
title: Integrare i log da Azure Key Vault tramite Hub eventi | Microsoft Docs
description: Esercitazione che illustra la procedura necessaria per rendere i log di Key Vault disponibili per un SIEM tramite l'integrazione dei log di Azure
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
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="32c96-103">Esercitazione sull'integrazione dei log di Azure: elaborazione degli eventi di Azure Key Vault tramite Hub eventi</span><span class="sxs-lookup"><span data-stu-id="32c96-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="32c96-104">È possibili usare l'integrazione dei log di Azure per recuperare gli eventi registrati e renderli disponibili per il sistema di gestione delle informazioni e degli eventi di sicurezza (SIEM).</span><span class="sxs-lookup"><span data-stu-id="32c96-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="32c96-105">Questa esercitazione illustra un esempio di come usare l'integrazione dei log di Azure per elaborare i log acquisiti tramite 	Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c96-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="32c96-106">Usare questa esercitazione per acquisire familiarità con l'interazione tra l'integrazione dei log di Azure e Hub eventi seguendo la procedura di esempio e comprendendo in che modo ogni passaggio supporta la soluzione.</span><span class="sxs-lookup"><span data-stu-id="32c96-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="32c96-107">È quindi possibile applicare quanto appreso qui per creare i passaggi personalizzati per supportare i requisiti specifici della propria azienda.</span><span class="sxs-lookup"><span data-stu-id="32c96-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="32c96-108">Non copiare o incollare i passaggi e i comandi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="32c96-109">Si tratta solo di esempi.</span><span class="sxs-lookup"><span data-stu-id="32c96-109">They're examples only.</span></span> <span data-ttu-id="32c96-110">Non usare i comandi di PowerShell "così come sono" nell'ambiente live,</span><span class="sxs-lookup"><span data-stu-id="32c96-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="32c96-111">in quanto devono essere personalizzati in base all'ambiente univoco.</span><span class="sxs-lookup"><span data-stu-id="32c96-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="32c96-112">Questa esercitazione illustra il processo per estrarre l'attività di Azure Key Vault registrata in un hub eventi e renderla disponibile come file JSON nel sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="32c96-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="32c96-113">È quindi possibile configurare il sistema SIEM per elaborare i file JSON.</span><span class="sxs-lookup"><span data-stu-id="32c96-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="32c96-114">La maggior parte dei passaggi in questa esercitazione implica la configurazione dell'insieme di credenziali delle chiavi, degli account di archiviazione e degli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="32c96-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="32c96-115">La procedura di integrazione dei log di Azure specifica si trova alla fine di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="32c96-116">Non eseguire questi passaggi in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="32c96-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="32c96-117">Sono concepiti solo per un ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="32c96-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="32c96-118">È necessario personalizzare la procedura prima di usarla nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="32c96-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="32c96-119">Le informazioni offerte consentono di comprendere i motivi di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="32c96-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="32c96-120">I collegamenti ad altri articoli offrono maggiori dettagli su determinati argomenti.</span><span class="sxs-lookup"><span data-stu-id="32c96-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="32c96-121">Per altre informazioni sui servizi citati in questa esercitazione, vedere:</span><span class="sxs-lookup"><span data-stu-id="32c96-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="32c96-122">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="32c96-123">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="32c96-124">Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="32c96-125">Configurazione iniziale</span><span class="sxs-lookup"><span data-stu-id="32c96-125">Initial setup</span></span>

<span data-ttu-id="32c96-126">Per poter completare la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="32c96-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="32c96-127">Una sottoscrizione di Azure e l'account per tale sottoscrizione con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="32c96-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="32c96-128">Se non si ha una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="32c96-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="32c96-129">Un sistema con accesso a Internet che soddisfi i requisiti per l'installazione del servizio di integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c96-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="32c96-130">Il sistema può trovarsi su un servizio cloud o essere ospitato in locale.</span><span class="sxs-lookup"><span data-stu-id="32c96-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="32c96-131">[Integrazione dei log di Azure](https://www.microsoft.com/download/details.aspx?id=53324) installato.</span><span class="sxs-lookup"><span data-stu-id="32c96-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="32c96-132">Per l'installazione:</span><span class="sxs-lookup"><span data-stu-id="32c96-132">To install it:</span></span>

   <span data-ttu-id="32c96-133">a.</span><span class="sxs-lookup"><span data-stu-id="32c96-133">a.</span></span> <span data-ttu-id="32c96-134">Usare il desktop remoto per connettersi al sistema citato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="32c96-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="32c96-135">b.</span><span class="sxs-lookup"><span data-stu-id="32c96-135">b.</span></span> <span data-ttu-id="32c96-136">Copiarvi il programma di installazione di Integrazione dei Log di Azure nel sistema.</span><span class="sxs-lookup"><span data-stu-id="32c96-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="32c96-137">È possibile [scaricare i file di installazione](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="32c96-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="32c96-138">c.</span><span class="sxs-lookup"><span data-stu-id="32c96-138">c.</span></span> <span data-ttu-id="32c96-139">Avviare il programma di installazione e accettare le Condizioni di licenza software Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32c96-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="32c96-140">d.</span><span class="sxs-lookup"><span data-stu-id="32c96-140">d.</span></span> <span data-ttu-id="32c96-141">Se si intende inserire informazioni di telemetria, lasciare selezionata la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="32c96-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="32c96-142">Se invece si preferisce non inviare le informazioni sull'uso a Microsoft, deselezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="32c96-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="32c96-143">Per altre informazioni sul servizio di integrazione dei log di Azure e su come installarlo, vedere [Integrazione dei log di Azure con la registrazione di Diagnostica di Azure e l'inoltro di eventi di Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="32c96-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="32c96-144">Versione più recente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="32c96-145">Se è installato Windows Server 2016 e la versione disponibile di PowerShell è almeno la versione 5.0.</span><span class="sxs-lookup"><span data-stu-id="32c96-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="32c96-146">Se si usa qualsiasi altra versione di Windows Server, l'utente potrebbe aver installato una versione precedente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="32c96-147">È possibile controllare la versione immettendo ```get-host``` in una finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="32c96-148">Se PowerShell 5.0 non è installato, è possibile [scaricarlo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="32c96-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="32c96-149">Dopo aver installato almeno la versione di PowerShell 5.0, è possibile procedere con l'installazione della versione più recente:</span><span class="sxs-lookup"><span data-stu-id="32c96-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="32c96-150">a.</span><span class="sxs-lookup"><span data-stu-id="32c96-150">a.</span></span> <span data-ttu-id="32c96-151">In una finestra di PowerShell immettere il comando ```Install-Module Azure```.</span><span class="sxs-lookup"><span data-stu-id="32c96-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="32c96-152">Completare la procedura d'installazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="32c96-153">b.</span><span class="sxs-lookup"><span data-stu-id="32c96-153">b.</span></span> <span data-ttu-id="32c96-154">Immettere il comando ```Install-Module AzureRM```.</span><span class="sxs-lookup"><span data-stu-id="32c96-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="32c96-155">Completare la procedura d'installazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-155">Complete the installation steps.</span></span>

   <span data-ttu-id="32c96-156">Per altre informazioni, vedere [Installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="32c96-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="32c96-157">Creare elementi dell'infrastruttura di supporto</span><span class="sxs-lookup"><span data-stu-id="32c96-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="32c96-158">Aprire una finestra di PowerShell con privilegi elevati e passare a **C:\Programmi\Integrazione log di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="32c96-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="32c96-159">Importare i cmdlet AzLog eseguendo lo script LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="32c96-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="32c96-160">Immettere il comando `.\LoadAzLogModule.ps1`.</span><span class="sxs-lookup"><span data-stu-id="32c96-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="32c96-161">Si noti l'uso di ".\" in questo comando. Verrà visualizzata una schermata analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="32c96-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Elenco dei moduli caricati](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="32c96-163">Immettere il comando `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="32c96-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="32c96-164">Nella finestra di accesso inserire le informazioni sulle credenziali per la sottoscrizione che verrà usata per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="32c96-165">Se questa è la prima volta che si accede ad Azure da questo computer, allora si visualizzerà un messaggio su come consentire a Microsoft di raccogliere dati sull'uso di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="32c96-166">È consigliabile abilitare la raccolta dati perché verrà usata per migliorare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="32c96-167">Con la corretta autenticazione si accede e vengono visualizzate le informazioni nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="32c96-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="32c96-168">Annotare l'ID e il nome della sottoscrizione, necessari per completare i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="32c96-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![Finestra di PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="32c96-170">Creare variabili per archiviare i valori che verranno usati successivamente.</span><span class="sxs-lookup"><span data-stu-id="32c96-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="32c96-171">Immettere ognuna delle seguenti righe di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c96-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="32c96-172">Potrebbe essere necessario regolare i valori per adattarli all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="32c96-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="32c96-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` Il nome della sottoscrizione potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="32c96-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="32c96-174">È possibile visualizzarlo come parte dell'output del comando precedente.</span><span class="sxs-lookup"><span data-stu-id="32c96-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="32c96-175">```$location = 'West US'``` (Verrà usata questa variabile per passare la posizione in cui si devono creare le risorse.</span><span class="sxs-lookup"><span data-stu-id="32c96-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="32c96-176">È possibile modificare questa variabile con qualsiasi località di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="32c96-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="32c96-177">``` $name = 'azlogtest' + $random``` Si può indicare qualsiasi nome, ma deve contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="32c96-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="32c96-178">``` $storageName = $name``` Questa variabile verrà usata per il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="32c96-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="32c96-179">```$rgname = $name ``` Questa variabile verrà usata per il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="32c96-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="32c96-180">``` $eventHubNameSpaceName = $name``` Nome dello spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="32c96-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="32c96-181">Specificare la sottoscrizione che si userà:</span><span class="sxs-lookup"><span data-stu-id="32c96-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="32c96-182">Creare un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="32c96-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="32c96-183">Se si immette `$rg` a questo punto, verrà visualizzato un output simile a quello della schermata di seguito:</span><span class="sxs-lookup"><span data-stu-id="32c96-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Output dopo la creazione di un gruppo di risorse](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="32c96-185">Creare un account di archiviazione che verrà usato per tenere traccia delle informazioni sullo stato:</span><span class="sxs-lookup"><span data-stu-id="32c96-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="32c96-186">Creare lo spazio dei nomi dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="32c96-186">Create the event hub namespace.</span></span> <span data-ttu-id="32c96-187">necessario per creare un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="32c96-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="32c96-188">Ottenere l'ID della regola che verrà usato con il provider di informazioni:</span><span class="sxs-lookup"><span data-stu-id="32c96-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="32c96-189">Ottenere tutte le possibili posizioni di Azure e aggiungere i nomi a una variabile che può essere usata in un passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="32c96-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="32c96-190">a.</span><span class="sxs-lookup"><span data-stu-id="32c96-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="32c96-191">b.</span><span class="sxs-lookup"><span data-stu-id="32c96-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="32c96-192">A questo punto, se si immette `$locations`, verranno visualizzati i nomi delle località senza le informazioni aggiuntive restituite da Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="32c96-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="32c96-193">Creare un profilo di log di Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="32c96-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="32c96-194">Per altre informazioni sui profili log di Azure, vedere [Panoramica del log attività di Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="32c96-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="32c96-195">È possibile ricevere un messaggio di errore quando si tenta di creare un profilo di log.</span><span class="sxs-lookup"><span data-stu-id="32c96-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="32c96-196">È possibile consultare quindi la documentazione relativa a Get-AzureRmLogProfile e Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="32c96-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="32c96-197">Se si esegue Get-AzureRmLogProfile verranno visualizzate le informazioni sul profilo di log.</span><span class="sxs-lookup"><span data-stu-id="32c96-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="32c96-198">È possibile eliminare il profilo di log esistente immettendo il comando ```Remove-AzureRmLogProfile -name 'Log Profile Name' ```.</span><span class="sxs-lookup"><span data-stu-id="32c96-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Errore del profilo di Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="32c96-200">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="32c96-200">Create a key vault</span></span>

1. <span data-ttu-id="32c96-201">Creare l'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="32c96-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="32c96-202">Configurare la registrazione per l'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="32c96-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="32c96-203">Generare l'attività di log</span><span class="sxs-lookup"><span data-stu-id="32c96-203">Generate log activity</span></span>

<span data-ttu-id="32c96-204">Le richieste devono essere inviate a Key Vault per generare l'attività dei log.</span><span class="sxs-lookup"><span data-stu-id="32c96-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="32c96-205">Azioni quali la generazione di chiavi, l'archiviazione di segreti o la lettura di segreti da Key Vault creeranno le voci dei log.</span><span class="sxs-lookup"><span data-stu-id="32c96-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="32c96-206">Visualizzare le chiavi di archiviazione corrente:</span><span class="sxs-lookup"><span data-stu-id="32c96-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="32c96-207">Generare un nuovo **key2**:</span><span class="sxs-lookup"><span data-stu-id="32c96-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="32c96-208">Visualizzare nuovamente le chiavi e vedere che **key2** contiene un valore diverso:</span><span class="sxs-lookup"><span data-stu-id="32c96-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="32c96-209">Impostare e leggere un segreto per generare voci di log aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="32c96-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="32c96-210">a.</span><span class="sxs-lookup"><span data-stu-id="32c96-210">a.</span></span> <span data-ttu-id="32c96-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="32c96-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segreto restituito](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="32c96-213">Configurare Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="32c96-214">Dopo aver configurato tutti gli elementi necessari per la registrazione di Key Vault in un hub eventi, è necessario configurare Integrazione dei log di Azure:</span><span class="sxs-lookup"><span data-stu-id="32c96-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="32c96-215">Eseguire il comando AzLog per ogni hub eventi:</span><span class="sxs-lookup"><span data-stu-id="32c96-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="32c96-216">Dopo circa un minuto di esecuzione degli ultimi comandi, verranno visualizzati i file JSON generati.</span><span class="sxs-lookup"><span data-stu-id="32c96-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="32c96-217">È possibile verificarlo monitorando la directory **C:\Utenti\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="32c96-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32c96-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32c96-218">Next steps</span></span>

- [<span data-ttu-id="32c96-219">Domande frequenti su Integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="32c96-220">Introduzione all'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="32c96-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="32c96-221">Integrare i log delle risorse di Azure nei sistemi SIEM</span><span class="sxs-lookup"><span data-stu-id="32c96-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
