---
title: aaaCreate una macchina virtuale di SQL Server in Azure PowerShell, Gestione risorse () | Documenti Microsoft
description: Fornisce procedure e script di PowerShell per la creazione di una macchina virtuale di Azure con le immagini della galleria di macchine virtuali SQL Server.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="730fc-103">Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="730fc-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="730fc-104">Portale</span><span class="sxs-lookup"><span data-stu-id="730fc-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="730fc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="730fc-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="730fc-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="730fc-106">Overview</span></span>
<span data-ttu-id="730fc-107">Questa esercitazione viene illustrato come una singola macchina virtuale di Azure utilizzando toocreate hello **Azure Resource Manager** modello di distribuzione utilizzando i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="730fc-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="730fc-108">In questa esercitazione si creerà una singola macchina virtuale utilizzando una singola unità disco da un'immagine in hello raccolta SQL.</span><span class="sxs-lookup"><span data-stu-id="730fc-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="730fc-109">Si creerà nuovi provider per l'archiviazione di hello, rete e risorse di calcolo che verranno utilizzate dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="730fc-110">Se esistono già provider per queste risorse, è possibile usarli.</span><span class="sxs-lookup"><span data-stu-id="730fc-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="730fc-111">Se è necessario hello versione classica di questo argomento, vedere [il provisioning di una macchina virtuale di SQL Server utilizzando PowerShell di Azure classico](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="730fc-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="730fc-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="730fc-112">Prerequisites</span></span>
<span data-ttu-id="730fc-113">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="730fc-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="730fc-114">Un account e una sottoscrizione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="730fc-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="730fc-115">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="730fc-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="730fc-116">[Azure PowerShell](/powershell/azure/overview), versione 1.4.0 o successiva. Questa esercitazione usa la versione 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="730fc-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="730fc-117">tooretrieve la versione, il tipo **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="730fc-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="730fc-118">Configurare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="730fc-118">Configure your subscription</span></span>
<span data-ttu-id="730fc-119">Aprire Windows PowerShell e stabilire tooyour accesso account Azure eseguendo i seguenti cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="730fc-120">Verrà visualizzata con un segno di schermata tooenter le credenziali.</span><span class="sxs-lookup"><span data-stu-id="730fc-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="730fc-121">Utilizzare hello stesso messaggio di posta elettronica e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="730fc-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="730fc-122">Dopo l'accesso correttamente verranno visualizzate alcune informazioni sullo schermo che include l'ID sottoscrizione hello con cui hai effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="730fc-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="730fc-123">Si tratta di sottoscrizione hello in cui le risorse di hello per questa esercitazione verranno create a meno che non si modifica una sottoscrizione diversa tooa.</span><span class="sxs-lookup"><span data-stu-id="730fc-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="730fc-124">Se si dispone di più ID sottoscrizione, eseguire un elenco di tutti l'ID sottoscrizione hello tooreturn cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="730fc-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="730fc-125">tooanother toochange ID sottoscrizione, eseguire hello seguente cmdlet con l'ID di sottoscrizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="730fc-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="730fc-126">Definire le variabili di immagine</span><span class="sxs-lookup"><span data-stu-id="730fc-126">Define image variables</span></span>
<span data-ttu-id="730fc-127">toosimplify usabilità e nella conoscenza dello script hello completata da questa esercitazione, si inizierà definendo una serie di variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="730fc-128">Modificare i valori di parametro hello quando si ritengono appropriato, ma fare attenzione alle lunghezze di tooname correlati restrizioni dei nomi e i caratteri speciali quando si modificano i valori hello forniti.</span><span class="sxs-lookup"><span data-stu-id="730fc-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="730fc-129">Posizione e gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="730fc-129">Location and Resource Group</span></span>
<span data-ttu-id="730fc-130">Utilizzare due variabili toodefine hello dati hello e area del gruppo di risorse in cui si creerà hello altre risorse per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="730fc-131">Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="730fc-132">Proprietà della risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="730fc-132">Storage properties</span></span>
<span data-ttu-id="730fc-133">Utilizzare hello seguenti variabili toodefine hello storage account e hello il tipo di archiviazione toobe usata dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="730fc-134">Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="730fc-135">Si noti che in questo esempio viene usata l' [Archiviazione Premium](../../../storage/common/storage-premium-storage.md), consigliata per carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="730fc-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="730fc-136">Per informazioni dettagliate su questa e su altre indicazioni, vedere [Procedure consigliate per le prestazioni per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="730fc-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="730fc-137">Proprietà di rete</span><span class="sxs-lookup"><span data-stu-id="730fc-137">Network properties</span></span>
<span data-ttu-id="730fc-138">Utilizzare hello seguendo l'interfaccia di rete variabili toodefine hello, metodo di allocazione hello TCP/IP, nome di rete virtuale hello, il nome di subnet virtuale hello, hello intervallo di indirizzi IP per rete virtuale hello, hello intervallo di indirizzi IP per subnet hello e hello utilizzata dalla rete hello nella macchina virtuale hello toobe etichetta nome di dominio pubblico.</span><span class="sxs-lookup"><span data-stu-id="730fc-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="730fc-139">Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="730fc-140">Proprietà della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="730fc-140">Virtual machine properties</span></span>
<span data-ttu-id="730fc-141">Utilizzare hello seguente nome della macchina virtuale hello toodefine variabili, nome del computer hello, dimensioni della macchina virtuale hello e nome hello del disco del sistema operativo per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="730fc-142">Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="730fc-143">Proprietà dell'immagine</span><span class="sxs-lookup"><span data-stu-id="730fc-143">Image properties</span></span>
<span data-ttu-id="730fc-144">Utilizzare hello seguenti variabili toodefine hello immagine toouse per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="730fc-145">In questo esempio viene utilizzata l'immagine di SQL Server 2016 Enterprise Edition di hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="730fc-146">Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.</span><span class="sxs-lookup"><span data-stu-id="730fc-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="730fc-147">Si noti che è possibile ottenere un elenco completo delle offerte di immagine di SQL Server con il comando Get-AzureRmVMImageOffer hello:</span><span class="sxs-lookup"><span data-stu-id="730fc-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="730fc-148">Ed è possibile visualizzare hello SKU disponibile per un'offerta con il comando Get-AzureRmVMImageSku hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="730fc-149">comando che segue Hello Mostra tutti gli SKU disponibili per hello **SQL2014SP1 WS2012R2** offrono.</span><span class="sxs-lookup"><span data-stu-id="730fc-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="730fc-150">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="730fc-150">Create a resource group</span></span>
<span data-ttu-id="730fc-151">Con modello di distribuzione di gestione risorse hello, hello prima che l'oggetto creato è il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="730fc-152">Si utilizzerà hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate cmdlet un gruppo di risorse di Azure e le risorse con risorse hello del gruppo di nome e il percorso definito dalle variabili hello che è stato inizializzato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="730fc-153">Eseguire hello cmdlet toocreate dopo il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="730fc-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="730fc-154">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="730fc-154">Create a storage account</span></span>
<span data-ttu-id="730fc-155">macchina virtuale Hello richiede risorse di archiviazione per disco del sistema operativo hello e hello dati di SQL Server e i file di log.</span><span class="sxs-lookup"><span data-stu-id="730fc-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="730fc-156">Per semplificare, verrà creato un singolo disco per entrambi.</span><span class="sxs-lookup"><span data-stu-id="730fc-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="730fc-157">È possibile collegare dischi aggiuntivi in un secondo momento utilizzando hello [Azure-Aggiungi disco](/powershell/module/azure/add-azuredisk) cmdlet in ordine tooplace i dati di SQL Server e i file di registro in dischi dedicati.</span><span class="sxs-lookup"><span data-stu-id="730fc-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="730fc-158">Si utilizzerà hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate cmdlet un'archiviazione standard account nel nuovo gruppo di risorse e con nome di account di archiviazione hello, nome Sku di archiviazione e posizione definita utilizzo di variabili hello in precedenza è stato inizializzato.</span><span class="sxs-lookup"><span data-stu-id="730fc-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="730fc-159">Eseguire hello cmdlet toocreate dopo il nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="730fc-160">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="730fc-160">Create network resources</span></span>
<span data-ttu-id="730fc-161">macchina virtuale Hello richiede un numero di risorse di rete per la connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="730fc-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="730fc-162">Ogni macchina virtuale richiede una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="730fc-163">In una rete virtuale deve essere definita almeno una subnet.</span><span class="sxs-lookup"><span data-stu-id="730fc-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="730fc-164">È necessario che sia definita un'interfaccia di rete con un indirizzo IP pubblico o privato.</span><span class="sxs-lookup"><span data-stu-id="730fc-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="730fc-165">Creare una configurazione di subnet di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="730fc-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="730fc-166">Creare prima di tutto una configurazione di subnet per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="730fc-167">Per questa esercitazione si creerà una subnet predefinita utilizzando hello [New AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="730fc-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="730fc-168">La configurazione di subnet della rete virtuale verrà creata con hello nome e indirizzo prefisso di subnet definito utilizzando le variabili hello è inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="730fc-169">È possibile definire proprietà aggiuntive di configurazione della subnet di rete virtuale hello utilizzando questo cmdlet, ma che non rientra hello ambito di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="730fc-170">Eseguire hello cmdlet toocreate dopo la configurazione di subnet virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="730fc-171">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="730fc-171">Create a virtual network</span></span>
<span data-ttu-id="730fc-172">Successivamente, si creerà la rete virtuale utilizzando hello [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="730fc-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="730fc-173">Verrà creata la rete virtuale nel nuovo gruppo di risorse, con prefisso di indirizzo definito utilizzando variabili di hello che è stato inizializzato in precedenza e utilizzando la configurazione di subnet hello è definito nel passaggio precedente hello, percorso e nome hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="730fc-174">Eseguire hello seguente cmdlet toocreate la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="730fc-175">Creare l'indirizzo IP pubblico hello</span><span class="sxs-lookup"><span data-stu-id="730fc-175">Create hello public IP address</span></span>
<span data-ttu-id="730fc-176">Ora che è disponibile la rete virtuale definita, è necessario tooconfigure un indirizzo IP per la macchina virtuale toohello di connettività.</span><span class="sxs-lookup"><span data-stu-id="730fc-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="730fc-177">Per questa esercitazione si creerà un indirizzo IP pubblico utilizzando l'indirizzo IP dinamico addressing toosupport connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="730fc-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="730fc-178">Si utilizzerà hello [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello indirizzo IP pubblico in hello risorsa gruppo creato prevously e con nome hello, percorso, il metodo di allocazione ed etichetta del nome di dominio DNS definito tramite hello variabili che è stato inizializzato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="730fc-179">È possibile definire proprietà aggiuntive dell'indirizzo IP pubblico hello utilizzando questo cmdlet, ma che non rientra hello ambito di questa esercitazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="730fc-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="730fc-180">È inoltre possibile creare un indirizzo privato o un indirizzo con un indirizzo statico, ma è anche esula hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="730fc-181">Eseguire hello seguente cmdlet toocreate l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="730fc-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="730fc-182">Creare l'interfaccia di rete hello</span><span class="sxs-lookup"><span data-stu-id="730fc-182">Create hello network interface</span></span>
<span data-ttu-id="730fc-183">Si sono ora pronti toocreate interfaccia di rete hello che utilizzerà la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="730fc-184">Si utilizzerà hello [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate cmdlet l'interfaccia di rete nel gruppo di risorse hello creato in precedenza e con nome hello, percorso, subnet e indirizzi IP pubblici definiti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="730fc-185">Eseguire hello seguente cmdlet toocreate l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="730fc-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="730fc-186">Configurare un oggetto VM</span><span class="sxs-lookup"><span data-stu-id="730fc-186">Configure a VM object</span></span>
<span data-ttu-id="730fc-187">Ora che si dispone di risorse di archiviazione e di rete definite, ci sono risorse di calcolo toodefine pronto per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="730fc-188">Per questa esercitazione, si verrà specificare varie proprietà del sistema operativo e dimensioni della macchina virtuale hello, specificare hello interfaccia di rete che è stati creati in precedenza, definire nell'archiviazione blob e quindi specificare disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="730fc-189">Creare l'oggetto macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="730fc-189">Create hello VM object</span></span>
<span data-ttu-id="730fc-190">Si inizierà specificando la dimensione di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="730fc-191">Per questa esercitazione verrà specificata l'opzione DS13.</span><span class="sxs-lookup"><span data-stu-id="730fc-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="730fc-192">Si utilizzerà hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate cmdlet un oggetto macchina virtuale può essere configurato con nome hello e dimensioni definiti utilizzando le variabili hello è inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="730fc-193">Eseguire hello seguente oggetto macchina virtuale di cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="730fc-194">Creare un nome delle credenziali oggetto toohold hello e una password per le credenziali di amministratore locale hello</span><span class="sxs-lookup"><span data-stu-id="730fc-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="730fc-195">Prima che è possibile impostare proprietà del sistema operativo per la macchina virtuale hello hello, dobbiamo credenziali hello toosupply per account di amministratore locale hello come stringa sicura.</span><span class="sxs-lookup"><span data-stu-id="730fc-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="730fc-196">tooaccomplish, si utilizzerà hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="730fc-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="730fc-197">Eseguire hello seguente cmdlet e, nella finestra di richiesta delle credenziali di Windows PowerShell hello, digitare hello toouse di nome e una password per account di amministratore locale hello nella macchina virtuale di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="730fc-198">Impostare le proprietà del sistema operativo hello per la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="730fc-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="730fc-199">Ora siamo proprietà del sistema operativo della macchina virtuale hello di tooset pronto.</span><span class="sxs-lookup"><span data-stu-id="730fc-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="730fc-200">Si utilizzerà hello [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) tipo hello tooset di cmdlet del sistema operativo di Windows, richiedono hello [agente della macchina virtuale](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installato, specificare tale cmdlet hello consente auto aggiornare e impostare il nome di macchina virtuale hello, nome del computer hello e le credenziali di hello utilizzare variabili hello che è stato inizializzato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="730fc-201">Eseguire hello cmdlet tooset hello del sistema operativo le proprietà seguenti per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="730fc-202">Aggiungere la macchina virtuale hello rete interfaccia toohello</span><span class="sxs-lookup"><span data-stu-id="730fc-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="730fc-203">A questo punto si aggiungerà l'interfaccia di rete hello creata in precedenza macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="730fc-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="730fc-204">Si utilizzerà hello [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet interfaccia di rete hello tooadd utilizzando una variabile dell'interfaccia di rete hello definita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="730fc-205">Eseguire hello seguente interfaccia di rete hello tooset cmdlet per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="730fc-206">Imposta percorso di archiviazione blob di hello per hello disco toobe usata dalla macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="730fc-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="730fc-207">Successivamente, si imposterà percorso di archiviazione blob di hello per hello disco toobe usata dalla macchina virtuale hello utilizzando variabili di hello è definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="730fc-208">Eseguire hello seguente percorso di archiviazione blob di cmdlet tooset hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="730fc-209">Set di proprietà del disco per la macchina virtuale hello hello del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="730fc-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="730fc-210">Successivamente, verranno impostate hello del sistema operativo su disco per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="730fc-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="730fc-211">Si utilizzerà hello [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet che il sistema operativo per la macchina virtuale hello hello in provengono da un'immagine, la memorizzazione nella cache solo tooread tooset (perché SQL Server viene installato sul hello stesso disco) e definire nome della macchina virtuale Hello e disco del sistema operativo hello definita utilizzando le variabili di hello definita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="730fc-212">Eseguire hello cmdlet tooset hello del sistema operativo disco le proprietà seguenti per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="730fc-213">Specificare l'immagine della piattaforma per la macchina virtuale hello hello</span><span class="sxs-lookup"><span data-stu-id="730fc-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="730fc-214">L'ultimo passaggio di configurazione è l'immagine della piattaforma hello toospecify per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="730fc-215">Immagine di SQL Server 2016 CTP più recente di hello viene usato per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="730fc-216">Si utilizzerà hello [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse cmdlet questa immagine come definito dalle variabili hello definita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="730fc-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="730fc-217">Eseguire hello seguente immagine della piattaforma hello toospecify cmdlet per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="730fc-218">Creare VM SQL hello</span><span class="sxs-lookup"><span data-stu-id="730fc-218">Create hello SQL VM</span></span>
<span data-ttu-id="730fc-219">Dopo aver completato i passaggi di configurazione hello, si è macchina virtuale di hello toocreate pronto.</span><span class="sxs-lookup"><span data-stu-id="730fc-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="730fc-220">Si utilizzerà hello [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello macchina virtuale utilizzando variabili di hello che sono state definite.</span><span class="sxs-lookup"><span data-stu-id="730fc-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="730fc-221">Eseguire hello seguente cmdlet toocreate la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="730fc-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="730fc-222">macchina virtuale Hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="730fc-222">hello virtual machine is created.</span></span> <span data-ttu-id="730fc-223">Si noti che viene creato un account di archiviazione standard per la diagnostica di avvio perché hello specificato l'account di archiviazione per il disco della macchina virtuale hello è un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="730fc-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="730fc-224">È ora possibile visualizzare la macchina in hello Azure Portal toosee [l'indirizzo IP pubblico e il relativo nome di dominio completo](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="730fc-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="730fc-225">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="730fc-225">Example script</span></span>
<span data-ttu-id="730fc-226">Hello lo script seguente contiene script di PowerShell hello completo per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="730fc-227">Si presuppone che si disponga già di installazione hello sottoscrizione di Azure toouse con hello **Aggiungi AzureRmAccount** e **selezionare AzureRmSubscription** comandi.</span><span class="sxs-lookup"><span data-stu-id="730fc-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="730fc-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="730fc-228">Next steps</span></span>
<span data-ttu-id="730fc-229">Dopo la creazione di macchine virtuali hello, si è pronti tooconnect macchina virtuale di toohello tramite connettività RDP e il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="730fc-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="730fc-230">Per ulteriori informazioni, vedere [connessione macchina virtuale di SQL Server in Azure (gestione delle risorse) tooa](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="730fc-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

