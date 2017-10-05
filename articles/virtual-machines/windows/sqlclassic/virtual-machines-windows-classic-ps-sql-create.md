---
title: Creare una macchina virtuale SQL Server in Azure PowerShell (distribuzione classica) | Microsoft Docs
description: "Fornisce procedure e script di PowerShell per la creazione di una macchina virtuale di Azure con le immagini della galleria di macchine virtuali SQL Server. In questo argomento viene usata la modalità di distribuzione classica."
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
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="6be2c-104">Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="6be2c-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="6be2c-105">In questo articolo viene descritta la procedura per creare una macchina virtuale SQL Server in Azure usando i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6be2c-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6be2c-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6be2c-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6be2c-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="6be2c-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6be2c-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="6be2c-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="6be2c-109">Per la versione di Resource Manager di questo argomento, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (Resource Manager)](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="6be2c-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="6be2c-110">Installare e configurare PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6be2c-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="6be2c-111">Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6be2c-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="6be2c-112">[Scaricare e installare i comandi di Azure PowerShell più recenti](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6be2c-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="6be2c-113">Avviare Windows PowerShell e connetterlo alla sottoscrizione di Azure mediante il comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="6be2c-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="6be2c-114">Determinare l'area di destinazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6be2c-114">Determine your target Azure region</span></span>

<span data-ttu-id="6be2c-115">La macchina virtuale di SQL Server verrà ospitata in un servizio cloud che si trova un'area di Azure specifica.</span><span class="sxs-lookup"><span data-stu-id="6be2c-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="6be2c-116">I passaggi seguenti consentono di determinare l'area, l'account di archiviazione e il servizio cloud che verranno usati nel resto dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6be2c-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="6be2c-117">Determinare il data center che si desidera usare per ospitare la macchina virtuale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be2c-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="6be2c-118">Il comando PowerShell seguente visualizza un elenco di nomi di aree disponibili.</span><span class="sxs-lookup"><span data-stu-id="6be2c-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="6be2c-119">Dopo che è stata identificata la località preferita, impostare una variabile denominata **$dcLocation** su quell'area.</span><span class="sxs-lookup"><span data-stu-id="6be2c-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="6be2c-120">Il comando seguente, ad esempio, imposta l'area su "Stati Uniti orientali":</span><span class="sxs-lookup"><span data-stu-id="6be2c-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="6be2c-121">Impostare l'account di archiviazione e la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6be2c-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="6be2c-122">Determinare la sottoscrizione di Azure da usare per la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6be2c-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="6be2c-123">Assegnare la sottoscrizione di Azure di destinazione alla variabile **$subscr** .</span><span class="sxs-lookup"><span data-stu-id="6be2c-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="6be2c-124">Quindi, impostarla come la sottoscrizione di Azure corrente.</span><span class="sxs-lookup"><span data-stu-id="6be2c-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="6be2c-125">Verificare la presenza di account di archiviazione esistenti.</span><span class="sxs-lookup"><span data-stu-id="6be2c-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="6be2c-126">Lo script seguente consente di visualizzare tutti gli account di archiviazione presenti nell'area selezionata:</span><span class="sxs-lookup"><span data-stu-id="6be2c-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="6be2c-127">Se è necessario un nuovo account di archiviazione, creare prima un nome account di archiviazione tutto in minuscolo con il comando New-AzureStorageAccount come nell'esempio seguente: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="6be2c-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="6be2c-128">Assegnare il nome dell'account di archiviazione di destinazione a **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="6be2c-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="6be2c-129">Usare quindi **Set-AzureSubscription** per impostare la sottoscrizione e l'account di archiviazione corrente.</span><span class="sxs-lookup"><span data-stu-id="6be2c-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="6be2c-130">Selezionare un'immagine di macchina virtuale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="6be2c-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="6be2c-131">Trovare l'elenco delle immagini delle macchine virtuali di SQL Server disponibili nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="6be2c-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="6be2c-132">Queste immagini hanno la proprietà **ImageFamily** che inizia con "SQL".</span><span class="sxs-lookup"><span data-stu-id="6be2c-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="6be2c-133">La query seguente consente di visualizzare la famiglia di immagini disponibile che include SQL Server preinstallato.</span><span class="sxs-lookup"><span data-stu-id="6be2c-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="6be2c-134">Nella famiglia di immagini di macchina virtuale trovata potrebbero esserci più immagini pubblicate.</span><span class="sxs-lookup"><span data-stu-id="6be2c-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="6be2c-135">Usare lo script seguente per trovare il nome dell'immagine di macchina virtuale pubblicata più recente per la famiglia di immagini selezionata (ad esempio **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="6be2c-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="6be2c-136">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6be2c-136">Create the virtual machine</span></span>

<span data-ttu-id="6be2c-137">Infine, creare la macchina virtuale con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6be2c-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="6be2c-138">Creare un servizio cloud per ospitare la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6be2c-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="6be2c-139">Si noti che è anche possibile usare un servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="6be2c-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="6be2c-140">Creare una nuova variabile **$svcname** con il nome breve del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6be2c-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="6be2c-141">Specificare il nome della macchina virtuale e le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6be2c-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="6be2c-142">Per altre informazioni sulle dimensioni della macchina virtuale, vedere [Dimensioni delle macchine virtuali in Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6be2c-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="6be2c-143">Specificare l'account amministratore locale e la password.</span><span class="sxs-lookup"><span data-stu-id="6be2c-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="6be2c-144">Eseguire lo script seguente per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6be2c-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="6be2c-145">Per le opzioni di configurazione e le spiegazioni aggiuntive, vedere la sezione **Compilare il set di comandi** in [Uso di Azure PowerShell per creare e preconfigurare macchine virtuali basate su Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6be2c-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="6be2c-146">Script di PowerShell di esempio</span><span class="sxs-lookup"><span data-stu-id="6be2c-146">Example PowerShell script</span></span>

<span data-ttu-id="6be2c-147">Lo script seguente costituisce un esempio di uno script completo che crea una macchina virtuale **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="6be2c-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="6be2c-148">Se si usa questo script, è necessario personalizzare le variabili iniziali sulla base dei passaggi precedenti di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="6be2c-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="6be2c-149">Connettersi a Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="6be2c-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="6be2c-150">Creare i file con estensione rdp nella cartella documenti dell'utente corrente per avviare queste macchine virtuali e completare l'installazione:</span><span class="sxs-lookup"><span data-stu-id="6be2c-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="6be2c-151">Nella directory dei documenti avviare il file con estensione rdp.</span><span class="sxs-lookup"><span data-stu-id="6be2c-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="6be2c-152">Connettersi con il nome utente e la password dell'amministratore specificati in precedenza (ad esempio, se è stato specificato il nome utente VMAdmin, specificare "\VMAdmin" come utente e fornire la password).</span><span class="sxs-lookup"><span data-stu-id="6be2c-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="6be2c-153">Completare la configurazione del computer SQL Server per l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="6be2c-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="6be2c-154">Dopo aver eseguito l'accesso al computer con desktop remoto, configurare SQL Server in base alle istruzioni presenti in [Procedura per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="6be2c-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6be2c-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6be2c-155">Next steps</span></span>

<span data-ttu-id="6be2c-156">Per istruzioni aggiuntive sul provisioning delle macchine virtuali con PowerShell, vedere la [documentazione delle macchine virtuali](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6be2c-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="6be2c-157">In molti casi, il passaggio successivo consiste nella migrazione dei database in questa nuova macchina virtuale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be2c-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="6be2c-158">Per linee guida sulla migrazione dei database, vedere [Migrazione di un database a SQL Server in una VM di Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6be2c-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="6be2c-159">Se si è interessati anche all'uso del portale di Azure per creare macchine virtuali di SQL Server, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server nel portale di Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6be2c-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="6be2c-160">Si noti che l'esercitazione che illustra il portale descrive la creazione di macchine virtuali mediante il modello consigliato di Gestione risorse anziché il modello classico impiegato in questo argomento di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6be2c-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="6be2c-161">Oltre a queste risorse, è consigliabile esaminare [altri argomenti relativi all'esecuzione di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6be2c-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
