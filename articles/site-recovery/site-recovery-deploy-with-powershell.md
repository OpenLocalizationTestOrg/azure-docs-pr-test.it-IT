---
title: aaaReplicate tooAzure di macchine virtuali Hyper-V nel portale classico di hello con PowerShell | Documenti Microsoft
description: Automatizzare la replica delle macchine virtuali Hyper-V nei cloud VMM tramite il ripristino del sito e PowerShell nel portale classico hello hello
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
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="f90d5-103">Replicare tooAzure macchine virtuali Hyper-V con PowerShell nel portale classico hello</span><span class="sxs-lookup"><span data-stu-id="f90d5-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f90d5-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f90d5-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="f90d5-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="f90d5-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="f90d5-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="f90d5-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="f90d5-107">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="f90d5-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="f90d5-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f90d5-108">Overview</span></span>
<span data-ttu-id="f90d5-109">Azure Site Recovery favorisce strategia ripristino emergenza e continuità tooyour aziendale gestendo la replica, il failover e ripristino delle macchine virtuali in un numero di scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f90d5-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="f90d5-110">Per un elenco completo di distribuzione di scenari di vedere hello [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f90d5-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="f90d5-111">Questo articolo illustra come attività comuni di toouse PowerShell tooautomate occorre tooperform per la configurazione di macchine virtuali di Azure Site Recovery tooreplicate Hyper-V nel servizio di archiviazione tooAzure cloud System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="f90d5-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="f90d5-112">articolo Hello sono inclusi i prerequisiti per lo scenario di hello e Mostra è come tooset di un insieme di credenziali di Site Recovery, installa hello Provider di Azure Site Recovery nel server VMM di origine hello, registrare hello server nell'insieme di credenziali hello, aggiungere un account di archiviazione di Azure, installare hello Azure Agente di servizi di ripristino in server host Hyper-V, configurare le impostazioni di protezione per i cloud VMM che verranno applicati tooall protetto le macchine virtuali e quindi abilitare la protezione per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f90d5-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="f90d5-113">Completare test toomake failover hello che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="f90d5-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="f90d5-114">Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f90d5-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="f90d5-115">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f90d5-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f90d5-116">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="f90d5-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f90d5-117">Before you start</span></span>
<span data-ttu-id="f90d5-118">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f90d5-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="f90d5-119">Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="f90d5-119">Azure prerequisites</span></span>
* <span data-ttu-id="f90d5-120">È necessario un account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="f90d5-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="f90d5-121">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f90d5-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f90d5-122">È necessario un toostore replicati dati dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90d5-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="f90d5-123">account di Hello deve replica geografica abilitata.</span><span class="sxs-lookup"><span data-stu-id="f90d5-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="f90d5-124">Dovrebbe essere nella stessa area dell'insieme di credenziali di Azure Site Recovery hello hello e associato hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f90d5-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="f90d5-125">[Altre informazioni sull'Archiviazione di Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f90d5-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="f90d5-126">È necessario assicurarsi che le macchine virtuali da tooprotect rispettino toomake [macchina virtuale di Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="f90d5-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="f90d5-127">Prerequisiti di VMM</span><span class="sxs-lookup"><span data-stu-id="f90d5-127">VMM prerequisites</span></span>
* <span data-ttu-id="f90d5-128">È necessario un server VMM in esecuzione su System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f90d5-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="f90d5-129">È necessario almeno un cloud nel server VMM si desidera tooprotect hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="f90d5-130">cloud Hello deve contenere:</span><span class="sxs-lookup"><span data-stu-id="f90d5-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="f90d5-131">Uno o più gruppi host VMM.</span><span class="sxs-lookup"><span data-stu-id="f90d5-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="f90d5-132">Uno o più cluster o server host Hyper-V in ogni gruppo host.</span><span class="sxs-lookup"><span data-stu-id="f90d5-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="f90d5-133">Uno o più macchine virtuali nel server Hyper-V di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="f90d5-134">Prerequisiti di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f90d5-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="f90d5-135">Hello Server host Hyper-V deve essere in esecuzione almeno **Windows Server 2012** con ruolo Hyper-V o **Microsoft Hyper-V Server 2012** e avere hello installati aggiornamenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="f90d5-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="f90d5-136">Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici.</span><span class="sxs-lookup"><span data-stu-id="f90d5-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="f90d5-137">È necessario un gestore cluster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="f90d5-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="f90d5-138">toodo questa operazione, in Server Manager > Gestione Cluster di Failover, connettersi toohello cluster, fare clic su **Configura ruolo** e selezionare **gestore Replica Hyper-V** in hello **selezionare il ruolo**schermata della procedura guidata disponibilità elevata hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="f90d5-139">Qualsiasi server host Hyper-V o cluster di cui si desidera toomanage protezione deve essere incluso in un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="f90d5-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="f90d5-140">Prerequisiti di mapping di rete</span><span class="sxs-lookup"><span data-stu-id="f90d5-140">Network mapping prerequisites</span></span>
<span data-ttu-id="f90d5-141">Quando si proteggono macchine virtuali nella rete di Azure viene eseguito il mapping tra le reti VM nel server VMM di origine hello e seguente hello tooenable di reti di Azure di destinazione:</span><span class="sxs-lookup"><span data-stu-id="f90d5-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="f90d5-142">Tutti i computer in cui eseguire il failover su hello stesso può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in rete.</span><span class="sxs-lookup"><span data-stu-id="f90d5-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="f90d5-143">Se un gateway di rete è configurato nella rete Azure di destinazione hello, macchine virtuali possono connettersi le macchine virtuali tooother locale.</span><span class="sxs-lookup"><span data-stu-id="f90d5-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="f90d5-144">Se non si configura rete mapping solo le macchine virtuali che il failover hello stesso piano di ripristino saranno in grado di tooconnect tooeach altri dopo tooAzure di failover.</span><span class="sxs-lookup"><span data-stu-id="f90d5-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="f90d5-145">Se si desidera che il mapping di rete toodeploy, occorre seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f90d5-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="f90d5-146">Hello le macchine virtuali da tooprotect nel server VMM di origine hello deve essere una rete VM tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="f90d5-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="f90d5-147">La rete deve essere collegato tooa la rete logica associata al cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="f90d5-148">Le macchine virtuali toowhich replicata una rete di Azure possono connettersi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="f90d5-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="f90d5-149">Selezionare la rete in fase di hello di failover.</span><span class="sxs-lookup"><span data-stu-id="f90d5-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="f90d5-150">rete Hello devono trovarsi in hello stessa area la sottoscrizione di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f90d5-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="f90d5-151">Prerequisiti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f90d5-151">PowerShell prerequisites</span></span>
<span data-ttu-id="f90d5-152">Assicurarsi di disporre di Azure PowerShell pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="f90d5-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="f90d5-153">Se si sta già usando PowerShell, è necessario tooupgrade tooversion 0.8.10 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f90d5-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="f90d5-154">Per informazioni sull'impostazione di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f90d5-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f90d5-155">Dopo aver impostato e configurato PowerShell, è possibile visualizzare tutti i cmdlet disponibili di hello per servizio hello [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f90d5-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f90d5-156">toolearn sui suggerimenti che consentono di utilizzare i cmdlet di hello, ad esempio come i valori dei parametri, input e output vengono in genere gestiti in Azure PowerShell, vedere [Introduzione ai cmdlet di Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f90d5-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="f90d5-157">Passaggio 1: Impostare una sottoscrizione di hello</span><span class="sxs-lookup"><span data-stu-id="f90d5-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="f90d5-158">In PowerShell, eseguire questi cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f90d5-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="f90d5-159">Sostituire gli elementi di hello all'interno di hello "< >" con le informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="f90d5-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="f90d5-160">Passaggio 2: creare un insieme di credenziali di Ripristino sito</span><span class="sxs-lookup"><span data-stu-id="f90d5-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="f90d5-161">In PowerShell, sostituire gli elementi di hello all'interno di hello "< >" con le informazioni specifiche ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="f90d5-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="f90d5-162">Passaggio 3: generare una chiave di registrazione dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="f90d5-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="f90d5-163">Generare una chiave di registrazione nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="f90d5-164">Dopo aver scaricato hello Provider di Azure Site Recovery e installarlo nel server VMM hello, si utilizzerà il server VMM di hello tooregister chiave nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="f90d5-165">Ottenere file di impostazioni dell'insieme di credenziali hello e impostare il contesto di hello:</span><span class="sxs-lookup"><span data-stu-id="f90d5-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="f90d5-166">Imposta il contesto di insieme di credenziali di hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f90d5-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="f90d5-167">Passaggio 4: Installare il Provider di Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="f90d5-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="f90d5-168">Nel computer VMM hello, creare una directory eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="f90d5-169">Estrarre il file hello utilizzando provider hello scaricato eseguendo hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="f90d5-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="f90d5-170">Installare il provider di hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f90d5-170">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="f90d5-171">Attendere toofinish installazione hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="f90d5-172">Registrare server hello in hello insieme di credenziali hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="f90d5-173">Passaggio 5: creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f90d5-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="f90d5-174">Se non si dispone di un account di archiviazione di Azure, è possibile creare un account di replica geografica abilitata eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="f90d5-175">Si noti che l'account di archiviazione hello deve essere nella stessa area geografica del servizio Azure Site Recovery hello hello e associato hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f90d5-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="f90d5-176">Passaggio 6: Installare hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="f90d5-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="f90d5-177">Da hello portale di Azure, installare l'agente servizi di ripristino di Azure hello in ogni server host Hyper-V presenti nei cloud VMM hello desiderate tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f90d5-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="f90d5-178">Eseguire hello comando seguente in tutti gli host VMM:</span><span class="sxs-lookup"><span data-stu-id="f90d5-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="f90d5-179">Passaggio 7: configurare le impostazioni di protezione del cloud</span><span class="sxs-lookup"><span data-stu-id="f90d5-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="f90d5-180">Creare un tooAzure profilo di protezione cloud eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="f90d5-181">Ottenere un contenitore di protezione eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f90d5-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="f90d5-182">Avviare associazione hello del contenitore di protezione hello cloud hello:</span><span class="sxs-lookup"><span data-stu-id="f90d5-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="f90d5-183">Al termine, il processo di hello eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="f90d5-184">Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-184">After hello job has finished processing, run hello following command:</span></span>

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



<span data-ttu-id="f90d5-185">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="f90d5-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="f90d5-186">Passaggio 8: configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="f90d5-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="f90d5-187">Prima di iniziare il mapping di rete verificare che le macchine virtuali nel server VMM di origine hello rete VM tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="f90d5-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="f90d5-188">Inoltre, creare una o più rete virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90d5-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="f90d5-189">Si noti che più reti VM possono essere mappate tooa singola rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90d5-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="f90d5-190">Si noti che se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="f90d5-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="f90d5-191">Se non è presente una subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="f90d5-192">Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f90d5-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="f90d5-193">comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="f90d5-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="f90d5-194">Hello secondo comando Recupera hello sito ripristino rete per il primo server di hello nella matrice hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="f90d5-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="f90d5-195">comando Hello archivia reti hello nella variabile di hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="f90d5-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="f90d5-196">Hello terzo comando recupera le sottoscrizioni di Azure tramite il cmdlet Get-AzureSubscription hello e il valore viene archiviato nella variabile hello $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f90d5-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="f90d5-197">Hello quarto comando recupera le reti virtuali di Azure tramite il cmdlet Get-AzureVNetSite hello e tale valore nella variabile hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="f90d5-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="f90d5-198">Hello finale cmdlet crea un mapping tra la rete primaria hello e di rete di macchina virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="f90d5-199">cmdlet di Hello specifica rete primaria hello come primo elemento di hello di $Networks.</span><span class="sxs-lookup"><span data-stu-id="f90d5-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="f90d5-200">cmdlet di Hello specifica una rete di macchina virtuale al primo elemento hello di $AzureVmNetworks utilizzando il relativo ID.</span><span class="sxs-lookup"><span data-stu-id="f90d5-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="f90d5-201">comando Hello include l'ID sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="f90d5-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="f90d5-202">Passaggio 9: abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f90d5-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="f90d5-203">Dopo aver configurate correttamente i server, cloud e reti, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="f90d5-204">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="f90d5-204">Note hello following:</span></span>

<span data-ttu-id="f90d5-205">Le macchine virtuali devono soddisfare [i prerequisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="f90d5-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="f90d5-206">per la macchina virtuale hello, è necessario impostare del sistema operativo di tooenable protezione hello e proprietà del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f90d5-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="f90d5-207">Quando si crea una macchina virtuale in VMM utilizzando un modello di macchina virtuale è possibile impostare proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="f90d5-208">È inoltre possibile impostare queste proprietà per le macchine virtuali esistenti in hello **generale** e **configurazione Hardware** schede delle proprietà di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f90d5-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="f90d5-209">Se le proprietà non impostate in VMM sarà in grado di tooconfigure nel portale di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="f90d5-210">protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="f90d5-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="f90d5-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="f90d5-212">Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="f90d5-213">Abilitare hello ripristino di emergenza per hello VM eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="f90d5-214">Testare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f90d5-214">Test your deployment</span></span>
<span data-ttu-id="f90d5-215">pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest.</span><span class="sxs-lookup"><span data-stu-id="f90d5-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="f90d5-216">Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.</span><span class="sxs-lookup"><span data-stu-id="f90d5-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="f90d5-217">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="f90d5-217">Note that:</span></span>

* <span data-ttu-id="f90d5-218">Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello.</span><span class="sxs-lookup"><span data-stu-id="f90d5-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="f90d5-219">Dopo il failover, si utilizzerà una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f90d5-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="f90d5-220">Se si desidera toodo, assicurarsi che tutti i criteri che impediscono la connessione tooa virtual machine tramite un indirizzo pubblico dominio non è.</span><span class="sxs-lookup"><span data-stu-id="f90d5-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="f90d5-221">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="f90d5-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="f90d5-222">Creare un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="f90d5-222">Create a recovery plan</span></span>
1. <span data-ttu-id="f90d5-223">Creare un file XML come modello per il piano di ripristino utilizzando i seguenti dati hello e quindi salvarlo come "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="f90d5-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="f90d5-224">Modificare il nodo di RecoveryPlan hello Id, nome, PrimaryServerId e SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="f90d5-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="f90d5-225">Modificare il nodo di ProtectionEntity hello PrimaryProtectionEntityId (vmid da VMM).</span><span class="sxs-lookup"><span data-stu-id="f90d5-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="f90d5-226">È possibile aggiungere ulteriori macchine virtuali mediante l'aggiunta di più nodi ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="f90d5-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="f90d5-227">Inserire dati hello nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="f90d5-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="f90d5-228">Creare hello RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="f90d5-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="f90d5-229">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="f90d5-229">Run a test failover</span></span>
1. <span data-ttu-id="f90d5-230">Ottenere l'oggetto RecoveryPlan hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="f90d5-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="f90d5-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="f90d5-232">Avviare il failover di test hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90d5-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="f90d5-233"><a name=monitor></a> Monitorare l'attività</span><span class="sxs-lookup"><span data-stu-id="f90d5-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="f90d5-234">Utilizzare hello attività hello toomonitor di comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f90d5-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="f90d5-235">Si noti la presenza di toowait tra i processi per hello toofinish di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f90d5-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="f90d5-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f90d5-236">Next steps</span></span>
<span data-ttu-id="f90d5-237">[Altre informazioni](/powershell/azure/overview) sui cmdlet PowerShell per Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f90d5-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="f90d5-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="f90d5-238"></a>.</span></span>
