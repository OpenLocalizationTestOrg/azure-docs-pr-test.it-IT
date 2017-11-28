---
title: aaaCreate una macchina virtuale di SQL Server in Azure PowerShell (versione classica) | Documenti Microsoft
description: "Fornisce procedure e script di PowerShell per la creazione di una macchina virtuale di Azure con le immagini della galleria di macchine virtuali SQL Server. In questo argomento Usa la modalità di distribuzione classica hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="6a637-104">Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="6a637-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="6a637-105">In questo articolo viene descritta la procedura per la modalità toocreate una macchina virtuale di SQL Server in Azure utilizzando hello i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a637-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6a637-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6a637-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6a637-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6a637-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="6a637-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="6a637-109">Per la versione di hello Gestione risorse di questo argomento, vedere [il provisioning di una macchina virtuale di SQL Server tramite Gestione risorse di Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="6a637-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="6a637-110">Installare e configurare PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a637-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="6a637-111">Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a637-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="6a637-112">[Scaricare e installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6a637-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="6a637-113">Avviare Windows PowerShell e connetterla tooyour sottoscrizione di Azure con hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="6a637-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="6a637-114">Determinare l'area di destinazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6a637-114">Determine your target Azure region</span></span>

<span data-ttu-id="6a637-115">La macchina virtuale di SQL Server verrà ospitata in un servizio cloud che si trova un'area di Azure specifica.</span><span class="sxs-lookup"><span data-stu-id="6a637-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="6a637-116">Hello seguente procedura consente di toodetermine è l'area geografica, un account di archiviazione e un servizio cloud che verrà utilizzato per il resto di hello di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="6a637-117">Determinare i data center di hello che si desidera toouse toohost la macchina virtuale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a637-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="6a637-118">il comando PowerShell seguente viene visualizzato un elenco di nomi delle aree disponibili.</span><span class="sxs-lookup"><span data-stu-id="6a637-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="6a637-119">Dopo aver identificato il percorso desiderato, impostare una variabile denominata **$dcLocation** toothat area.</span><span class="sxs-lookup"><span data-stu-id="6a637-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="6a637-120">Ad esempio, hello comando set hello area troppo seguente "Stati Uniti orientali":</span><span class="sxs-lookup"><span data-stu-id="6a637-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="6a637-121">Impostare l'account di archiviazione e la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6a637-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="6a637-122">Determinare hello sottoscrizione Azure, si utilizzerà per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6a637-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="6a637-123">Assegnare il toohello di sottoscrizione di Azure di destinazione **$subscr** variabile.</span><span class="sxs-lookup"><span data-stu-id="6a637-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="6a637-124">Quindi, impostarla come la sottoscrizione di Azure corrente.</span><span class="sxs-lookup"><span data-stu-id="6a637-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="6a637-125">Verificare la presenza di account di archiviazione esistenti.</span><span class="sxs-lookup"><span data-stu-id="6a637-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="6a637-126">Hello lo script seguente consente di visualizzare tutti gli account di archiviazione presenti nel proprio paese scelto:</span><span class="sxs-lookup"><span data-stu-id="6a637-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="6a637-127">Se è necessario un nuovo account di archiviazione, creare innanzitutto un nome di account di archiviazione tutto minuscolo con il comando New-AzureStorageAccount hello come hello di esempio seguente:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="6a637-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="6a637-128">Assegnare hello destinazione storage account name toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="6a637-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="6a637-129">Utilizzare quindi **Set-AzureSubscription** tooset hello sottoscrizione e l'account di archiviazione corrente.</span><span class="sxs-lookup"><span data-stu-id="6a637-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="6a637-130">Selezionare un'immagine di macchina virtuale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="6a637-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="6a637-131">Individuare l'elenco di hello di immagini di macchine virtuali di SQL Server disponibili dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="6a637-132">Queste immagini hanno la proprietà **ImageFamily** che inizia con "SQL".</span><span class="sxs-lookup"><span data-stu-id="6a637-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="6a637-133">esempio Hello query consente di visualizzare hello immagine famiglia disponibili tooyou che SQL Server è preinstallato.</span><span class="sxs-lookup"><span data-stu-id="6a637-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="6a637-134">Quando si individua una famiglia di immagine di macchina virtuale hello, in questo gruppo possono essere più immagini pubblicate.</span><span class="sxs-lookup"><span data-stu-id="6a637-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="6a637-135">Lo script seguente hello utilizzare viene toofind hello più recente pubblicata immagine nome della macchina virtuale per l'intera famiglia di immagine selezionata (ad esempio **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="6a637-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="6a637-136">Creare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="6a637-136">Create hello virtual machine</span></span>

<span data-ttu-id="6a637-137">Infine, creare macchine virtuali hello con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a637-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="6a637-138">Creare un cloud servizio toohost hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6a637-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="6a637-139">Si noti che è anche possibile toouse un servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="6a637-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="6a637-140">Creare una nuova variabile **$svcname** nome breve di hello del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="6a637-141">Specificare il nome di macchina virtuale hello e una dimensione.</span><span class="sxs-lookup"><span data-stu-id="6a637-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="6a637-142">Per altre informazioni sulle dimensioni della macchina virtuale, vedere [Dimensioni delle macchine virtuali in Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a637-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="6a637-143">Specificare la password e account di amministratore locale hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="6a637-144">Eseguire hello seguente macchina virtuale di script toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="6a637-145">Per informazioni aggiuntive e le opzioni di configurazione, vedere hello **compilare il set di comandi** sezione [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a637-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="6a637-146">Script di PowerShell di esempio</span><span class="sxs-lookup"><span data-stu-id="6a637-146">Example PowerShell script</span></span>

<span data-ttu-id="6a637-147">Hello script riportato di seguito viene fornito un esempio di uno script completo che consente di creare un **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2** macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6a637-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="6a637-148">Se si usa questo script, è necessario personalizzare le variabili di hello iniziale in base ai passaggi precedenti di hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="6a637-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="6a637-149">Connettersi a Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="6a637-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="6a637-150">Creare i file RDP hello toolaunch di cartella documenti dell'utente corrente hello il programma di installazione toocomplete queste macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="6a637-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="6a637-151">Nella directory documenti hello, avviare il file RDP hello.</span><span class="sxs-lookup"><span data-stu-id="6a637-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="6a637-152">La connessione con nome utente dell'amministratore hello e la password specificati in precedenza (ad esempio, se il nome utente è stato VMAdmin, specificare "\VMAdmin" come utente hello e fornire la password di hello).</span><span class="sxs-lookup"><span data-stu-id="6a637-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="6a637-153">Configurazione di hello completo di hello macchina di SQL Server per l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="6a637-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="6a637-154">Dopo l'accesso toohello computer con desktop remoto, configurare SQL Server in base alle istruzioni hello [passaggi per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="6a637-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a637-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a637-155">Next steps</span></span>

<span data-ttu-id="6a637-156">È possibile trovare istruzioni aggiuntive per il provisioning di macchine virtuali con PowerShell in hello [macchine virtuali-documentazione](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a637-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="6a637-157">In molti casi, la fase successiva hello è toomigrate toothis il database nuova VM SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a637-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="6a637-158">Per istruzioni sulla migrazione di database, vedere [la migrazione di un Server in una macchina virtuale Azure di tooSQL Database](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a637-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="6a637-159">Se inoltre si è interessati all'uso hello toocreate portale Azure macchine virtuali di SQL, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6a637-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="6a637-160">Si noti che esercitazione hello che tramite il portale di hello crea le macchine virtuali utilizzando percorsi hello modello consigliato di gestione risorse, anziché modello classico di hello utilizzato in questo argomento di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a637-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="6a637-161">Inoltre le risorse toothese, che è consigliabile consultare [su altri argomenti relativi a SQL Server in macchine virtuali di Azure toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a637-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
