---
title: Replicare le macchine virtuali Hyper-V in Azure nel portale classico con PowerShell | Documentazione Microsoft
description: Automatizzare la replica delle macchine virtuali Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell nel portale classico
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="f337d-103">Replicare le macchine virtuali Hyper-V in Azure con PowerShell nel portale classico</span><span class="sxs-lookup"><span data-stu-id="f337d-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f337d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f337d-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="f337d-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="f337d-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="f337d-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="f337d-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="f337d-107">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="f337d-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="f337d-108">Overview</span><span class="sxs-lookup"><span data-stu-id="f337d-108">Overview</span></span>
<span data-ttu-id="f337d-109">Azure Site Recovery favorisce la strategia di continuità aziendale e ripristino di emergenza (BCDR) gestendo la replica, il failover e il ripristino delle macchine virtuali in diversi scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f337d-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="f337d-110">Per un elenco completo degli scenari di distribuzione, vedere [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f337d-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="f337d-111">In questo articolo viene illustrato come utilizzare PowerShell per automatizzare attività comuni, che è necessario eseguire quando si configura Azure Site Recovery per replicare le macchine virtuali Hyper-V nei cloud VMM di System Center VMM nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="f337d-112">L’articolo include i prerequisiti per lo scenario e mostra come configurare un insieme di credenziali di Azure Site Recovery, installare il provider di Azure Site Recovery sul server VMM di origine, registrare il server nell'insieme di credenziali, aggiungere un account di archiviazione di Azure, installare l'agente di Servizi di ripristino di Azure nei server host Hyper-V, configurare le impostazioni di protezione per i cloud VMM che verranno applicate a tutte le macchine virtuali protette e quindi abilitare la protezione per tali macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f337d-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="f337d-113">Terminare con il test del failover, per accertarsi che tutti gli elementi funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="f337d-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="f337d-114">Nel caso di problemi di configurazione di questo scenario, inviare le proprie domande al [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f337d-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="f337d-115">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f337d-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f337d-116">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f337d-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="f337d-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f337d-117">Before you start</span></span>
<span data-ttu-id="f337d-118">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f337d-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="f337d-119">Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="f337d-119">Azure prerequisites</span></span>
* <span data-ttu-id="f337d-120">È necessario un account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="f337d-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="f337d-121">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f337d-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f337d-122">Per archiviare i dati replicati, sarà necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="f337d-123">Nell'account deve essere abilitata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="f337d-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="f337d-124">Dovrà trovarsi nella stessa area dell'insieme di credenziali di Azure Site Recovery ed essere associato alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f337d-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="f337d-125">[Altre informazioni sull'Archiviazione di Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f337d-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="f337d-126">È necessario assicurarsi che le macchine virtuali da proteggere soddisfino i [prerequisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="f337d-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="f337d-127">Prerequisiti di VMM</span><span class="sxs-lookup"><span data-stu-id="f337d-127">VMM prerequisites</span></span>
* <span data-ttu-id="f337d-128">È necessario un server VMM in esecuzione su System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f337d-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="f337d-129">È necessario almeno un cloud nel server VMM da proteggere.</span><span class="sxs-lookup"><span data-stu-id="f337d-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="f337d-130">Il cloud deve contenere:</span><span class="sxs-lookup"><span data-stu-id="f337d-130">The cloud should contain:</span></span>
  * <span data-ttu-id="f337d-131">Uno o più gruppi host VMM.</span><span class="sxs-lookup"><span data-stu-id="f337d-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="f337d-132">Uno o più cluster o server host Hyper-V in ogni gruppo host.</span><span class="sxs-lookup"><span data-stu-id="f337d-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="f337d-133">Una o più macchine virtuali nel server Hyper-V di origine.</span><span class="sxs-lookup"><span data-stu-id="f337d-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="f337d-134">Prerequisiti di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f337d-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="f337d-135">I server Hyper-V host devono eseguire almeno **Windows Server 2012** con ruolo Hyper-V oppure **Microsoft Hyper-V Server 2012** e disporre degli ultimi aggiornamenti installati.</span><span class="sxs-lookup"><span data-stu-id="f337d-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="f337d-136">Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici.</span><span class="sxs-lookup"><span data-stu-id="f337d-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="f337d-137">Sarà necessario configurare manualmente il broker del cluster.</span><span class="sxs-lookup"><span data-stu-id="f337d-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="f337d-138">A tale scopo, in Gestione server > Gestione cluster di failover, connettersi al cluster, fare clic su **Configura ruolo** e selezionare **Gestore di replica Hyper-V** nella schermata **Seleziona ruolo** della procedura guidata Disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="f337d-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="f337d-139">Qualsiasi server o cluster Hyper-V per cui si vuole gestire la protezione deve essere incluso in un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="f337d-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="f337d-140">Prerequisiti di mapping di rete</span><span class="sxs-lookup"><span data-stu-id="f337d-140">Network mapping prerequisites</span></span>
<span data-ttu-id="f337d-141">Quando si proteggono le macchine virtuali in Azure il mapping di rete mappa tra le reti VM nel server VMM di origine e le reti di Azure in un server VMM di destinazione per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f337d-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="f337d-142">Tutte le macchine virtuali di cui viene eseguito il failover nella stessa rete possono connettersi tra loro, indipendentemente dal piano di ripristino di appartenenza.</span><span class="sxs-lookup"><span data-stu-id="f337d-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="f337d-143">Se nella rete di Azure di destinazione è configurato un gateway di rete, le macchine virtuali possono connettersi ad altre macchine virtuali locali.</span><span class="sxs-lookup"><span data-stu-id="f337d-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="f337d-144">Se non si configura il mapping delle reti, solo le macchine virtuali di cui viene eseguito il failover nello stesso piano di ripristino possono connettersi tra loro dopo il failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="f337d-145">Per distribuire il mapping di rete sarà necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f337d-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="f337d-146">Le macchine virtuali che si vuole proteggere nel server VMM di origine devono essere connesse a una rete VM.</span><span class="sxs-lookup"><span data-stu-id="f337d-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="f337d-147">È necessario che tale rete sia collegata a una rete logica associata al cloud.</span><span class="sxs-lookup"><span data-stu-id="f337d-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="f337d-148">Una rete di Azure a cui le macchine virtuali replicate possono connettersi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="f337d-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="f337d-149">Questa rete viene selezionata al momento del failover.</span><span class="sxs-lookup"><span data-stu-id="f337d-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="f337d-150">La rete deve trovarsi nella stessa area della sottoscrizione di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f337d-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="f337d-151">Prerequisiti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f337d-151">PowerShell prerequisites</span></span>
<span data-ttu-id="f337d-152">Assicurarsi che Azure PowerShell sia pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="f337d-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="f337d-153">Se già si utilizza PowerShell, è necessario eseguire l'aggiornamento alla versione 0.8.10 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f337d-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="f337d-154">Per informazioni sulla configurazione di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f337d-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f337d-155">Dopo avere impostato e configurato PowerShell, è possibile vedere tutti i cmdlet disponibili per il servizio [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f337d-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f337d-156">Per i suggerimenti che facilitano l’utilizzo dei cmdlet, ad esempio come i valori dei parametri, gli input e gli output vengono in genere gestiti in Azure PowerShell, vedere [Introduzione ai cmdlet di Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f337d-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="f337d-157">Passaggio 1: impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f337d-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="f337d-158">In PowerShell, eseguire questi cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f337d-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="f337d-159">Sostituire gli elementi all'interno dei segni di minore/maggiore ("< >") con le informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="f337d-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="f337d-160">Passaggio 2: creare un insieme di credenziali di Ripristino sito</span><span class="sxs-lookup"><span data-stu-id="f337d-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="f337d-161">In PowerShell, sostituire gli elementi all'interno dei segni di minore/maggiore ("< >") con le informazioni specifiche ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="f337d-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="f337d-162">Passaggio 3: generare una chiave di registrazione dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="f337d-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="f337d-163">Generare una chiave di registrazione nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f337d-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="f337d-164">Dopo aver scaricato il provider di Azure Site Recovery e averlo installato sul server VMM, si userà questa chiave per registrare il server VMM nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f337d-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="f337d-165">Ottenere il file di impostazione dell'insieme di ottenere e impostare il contesto:</span><span class="sxs-lookup"><span data-stu-id="f337d-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="f337d-166">Impostare il contesto dell’insieme di credenziali eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f337d-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="f337d-167">Passaggio 4: installare il provider di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f337d-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="f337d-168">Nel computer VMM, creare una directory eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="f337d-169">Estrarre i file utilizzando il provider scaricato eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="f337d-170">Installare il provider utilizzando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f337d-170">Install the provider using the following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="f337d-171">Attendere la fine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="f337d-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="f337d-172">Registrare il server nell'insieme di credenziali utilizzando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="f337d-173">Passaggio 5: creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f337d-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="f337d-174">Se non si dispone di un account di archiviazione di Azure, creare un account con la replica geografica abilitata eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="f337d-175">Si noti che l'account di archiviazione deve trovarsi nella stessa area geografica in cui si trova il servizio Azure Site Recovery e deve essere associato alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f337d-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="f337d-176">Passaggio 6: installare l'agente di Servizi di ripristino di Azure</span><span class="sxs-lookup"><span data-stu-id="f337d-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="f337d-177">Dal portale di Azure, installare l'agente di Servizi di ripristino di Azure in ogni server host Hyper-V presente nei cloud VMM da proteggere.</span><span class="sxs-lookup"><span data-stu-id="f337d-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="f337d-178">Eseguire il comando seguente in tutti gli host VMM:</span><span class="sxs-lookup"><span data-stu-id="f337d-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="f337d-179">Passaggio 7: configurare le impostazioni di protezione del cloud</span><span class="sxs-lookup"><span data-stu-id="f337d-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="f337d-180">Creare un profilo di protezione cloud in Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="f337d-181">Ottenere un contenitore di protezione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f337d-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="f337d-182">Avviare l'associazione del contenitore di protezione al cloud:</span><span class="sxs-lookup"><span data-stu-id="f337d-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="f337d-183">Al termine del processo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="f337d-184">Al termine del processo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-184">After the job has finished processing, run the following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="f337d-185">Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="f337d-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="f337d-186">Passaggio 8: configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="f337d-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="f337d-187">Prima di iniziare il mapping di rete, verificare che le macchine virtuali nel server VMM di origine siano connesse a una rete VM.</span><span class="sxs-lookup"><span data-stu-id="f337d-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="f337d-188">Inoltre, creare una o più rete virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="f337d-189">Si noti che è possibile mappare più reti VM a una singola rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="f337d-190">Si noti che, se la rete di destinazione ha più subnet e una di esse ha lo stesso nome di una subnet in cui si trova la macchina virtuale di origine, la macchina virtuale di replica sarà connessa a tale subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="f337d-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="f337d-191">Se non è presente una subnet di destinazione con un nome corrispondente, la macchina virtuale sarà connessa alla prima subnet della rete.</span><span class="sxs-lookup"><span data-stu-id="f337d-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="f337d-192">Il primo comando ottiene i server per l’insieme di credenziali corrente di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f337d-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="f337d-193">Il comando archivia i server di Microsoft Azure Site Recovery nella variabile di matrice $Servers.</span><span class="sxs-lookup"><span data-stu-id="f337d-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="f337d-194">Il secondo comando ottiene la rete di ripristino del sito per il primo server nella matrice $Servers.</span><span class="sxs-lookup"><span data-stu-id="f337d-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="f337d-195">Il comando archivia le reti nella variabile $Networks.</span><span class="sxs-lookup"><span data-stu-id="f337d-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="f337d-196">Il terzo comando ottiene le sottoscrizioni di Azure tramite il cmdlet Get-AzureSubscription e quindi archivia tale valore nella variabile $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f337d-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="f337d-197">Il quarto comando ottiene le reti virtuali di Azure tramite il cmdlet Get-AzureVNetSite e quindi archivia tale valore nella variabile $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="f337d-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="f337d-198">Il cmdlet finale crea un mapping tra la rete primaria e la rete delle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="f337d-199">Il cmdlet specifica la rete primaria come primo elemento di $Networks.</span><span class="sxs-lookup"><span data-stu-id="f337d-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="f337d-200">Il cmdlet specifica una rete di macchine virtuali come primo elemento di $AzureVmNetworks utilizzando il relativo ID.</span><span class="sxs-lookup"><span data-stu-id="f337d-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="f337d-201">Il comando include l'ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f337d-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="f337d-202">Passaggio 9: abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f337d-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="f337d-203">Dopo la configurazione corretta di server, cloud e reti, sarà possibile abilitare la protezione per le macchine virtuali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f337d-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="f337d-204">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f337d-204">Note the following:</span></span>

<span data-ttu-id="f337d-205">Le macchine virtuali devono soddisfare [i prerequisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="f337d-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="f337d-206">Per abilitare la protezione, è necessario che le proprietà del sistema operativo e del disco del sistema operativo siano impostate per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f337d-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="f337d-207">Quando si crea una macchina virtuale basata su un modello di macchina virtuale VMM è possibile impostare la proprietà.</span><span class="sxs-lookup"><span data-stu-id="f337d-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="f337d-208">È possibile impostare queste proprietà anche per le macchine virtuali esistenti nelle schede **Generale** e **Configurazione hardware** delle proprietà delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f337d-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="f337d-209">Se queste proprietà non vengono impostate in VMM, sarà possibile configurarle nel portale di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f337d-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="f337d-210">Per abilitare la protezione, eseguire il comando seguente per ottenere il contenitore di protezione:</span><span class="sxs-lookup"><span data-stu-id="f337d-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="f337d-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="f337d-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="f337d-212">Ottenere l'entità di protezione (VM) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="f337d-213">Abilitare il ripristino di emergenza per la macchina virtuale eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="f337d-214">Testare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f337d-214">Test your deployment</span></span>
<span data-ttu-id="f337d-215">Per testare la distribuzione è possibile eseguire un failover di test per una singola macchina virtuale oppure creare un piano di ripristino costituito da più macchine virtuali ed eseguire un failover di test per il piano.</span><span class="sxs-lookup"><span data-stu-id="f337d-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="f337d-216">Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.</span><span class="sxs-lookup"><span data-stu-id="f337d-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="f337d-217">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="f337d-217">Note that:</span></span>

* <span data-ttu-id="f337d-218">Per eseguire la connessione alla macchina virtuale in Azure tramite Desktop remoto dopo il failover, abilitare Connessione Desktop remoto sulla macchina virtuale prima di eseguire il failover di test.</span><span class="sxs-lookup"><span data-stu-id="f337d-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="f337d-219">Dopo il failover si userà un indirizzo IP pubblico per connettersi alla macchina virtuale in Azure tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f337d-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="f337d-220">Se si vuole procedere in questo senso, assicurarsi che non siano presenti criteri di dominio che impediscono la connessione a una macchina virtuale mediante un indirizzo pubblico.</span><span class="sxs-lookup"><span data-stu-id="f337d-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="f337d-221">Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="f337d-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="f337d-222">Creare un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="f337d-222">Create a recovery plan</span></span>
1. <span data-ttu-id="f337d-223">Creare un file XML come modello per il piano di ripristino utilizzando i dati seguenti e quindi salvarlo come "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="f337d-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="f337d-224">Cambiare l'ID nodo RecoveryPlan, il nome, il PrimaryServerId e il SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="f337d-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="f337d-225">Modificare il PrimaryProtectionEntityId del nodo ProtectionEntity (vmid da VMM).</span><span class="sxs-lookup"><span data-stu-id="f337d-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="f337d-226">È possibile aggiungere ulteriori macchine virtuali mediante l'aggiunta di più nodi ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="f337d-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="f337d-227">Inserire i dati nel modello:</span><span class="sxs-lookup"><span data-stu-id="f337d-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="f337d-228">Creare il RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="f337d-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="f337d-229">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="f337d-229">Run a test failover</span></span>
1. <span data-ttu-id="f337d-230">Ottenere l'oggetto RecoveryPlan eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="f337d-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="f337d-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="f337d-232">Avviare il failover di test eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f337d-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="f337d-233"><a name=monitor></a> Monitorare l'attività</span><span class="sxs-lookup"><span data-stu-id="f337d-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="f337d-234">Utilizzare i comandi seguenti per monitorare l'attività.</span><span class="sxs-lookup"><span data-stu-id="f337d-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="f337d-235">Si noti che è necessario attendere l'esecuzione dei processi per il completamento dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f337d-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="f337d-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f337d-236">Next steps</span></span>
<span data-ttu-id="f337d-237">[Altre informazioni](/powershell/azure/overview) sui cmdlet PowerShell per Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f337d-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="f337d-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="f337d-238"></a>.</span></span>
