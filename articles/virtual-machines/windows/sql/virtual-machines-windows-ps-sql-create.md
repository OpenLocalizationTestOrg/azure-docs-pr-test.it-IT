---
title: Creare una macchina virtuale SQL Server in Azure PowerShell (Resource Manager) | Microsoft Docs
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
ms.openlocfilehash: aa90a1d017af5f477407ab33f0580904472f412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="a4253-103">Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="a4253-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4253-104">Portale</span><span class="sxs-lookup"><span data-stu-id="a4253-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="a4253-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4253-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="a4253-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4253-106">Overview</span></span>
<span data-ttu-id="a4253-107">Questa esercitazione illustra come creare una singola macchina virtuale di Azure usando il modello di distribuzione **Azure Resource Manager** con i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4253-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="a4253-108">In questa esercitazione verrà creata una singola macchina virtuale con una singola unità disco da un'immagine di SQL Gallery.</span><span class="sxs-lookup"><span data-stu-id="a4253-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="a4253-109">Verranno creati nuovi provider per le risorse di archiviazione, rete e calcolo che verranno usate dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="a4253-110">Se esistono già provider per queste risorse, è possibile usarli.</span><span class="sxs-lookup"><span data-stu-id="a4253-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="a4253-111">Se è necessaria la versione classica di questo argomento, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (classico)](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="a4253-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4253-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4253-112">Prerequisites</span></span>
<span data-ttu-id="a4253-113">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="a4253-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="a4253-114">Un account e una sottoscrizione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="a4253-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="a4253-115">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4253-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a4253-116">[Azure PowerShell](/powershell/azure/overview), versione 1.4.0 o successiva. Questa esercitazione usa la versione 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="a4253-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="a4253-117">Per recuperare la versione, digitare **Get-Module Azure -ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="a4253-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="a4253-118">Configurare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a4253-118">Configure your subscription</span></span>
<span data-ttu-id="a4253-119">Aprire Windows PowerShell e accedere all'account Azure eseguendo il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="a4253-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="a4253-120">Verrà visualizzata una schermata di accesso per immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="a4253-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="a4253-121">Utilizzare lo stesso indirizzo email e password utilizzati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4253-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="a4253-122">Dopo aver effettuato l'accesso, sullo schermo verranno visualizzate informazioni tra cui il valore SubscriptionId usato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a4253-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="a4253-123">Si tratta della sottoscrizione in cui verranno create le risorse per questa esercitazione, a meno che non si specifichi una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="a4253-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="a4253-124">Se sono presenti più valori SubscriptionId, eseguire il cmdlet seguente per restituire un elenco di tutti i valori SubscriptionId:</span><span class="sxs-lookup"><span data-stu-id="a4253-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="a4253-125">Per passare a un altro SubscriptionId, eseguire il cmdlet seguente con il valore SubscriptionId desiderato.</span><span class="sxs-lookup"><span data-stu-id="a4253-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="a4253-126">Definire le variabili di immagine</span><span class="sxs-lookup"><span data-stu-id="a4253-126">Define image variables</span></span>
<span data-ttu-id="a4253-127">Per facilitare l'uso e la comprensione dello script completo di questa esercitazione, verranno prima di tutto definite alcune variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="a4253-128">Cambiare i valori dei parametri in base alla necessità, ma quando si modificano i valori forniti occorre prestare attenzione alle restrizioni di denominazione correlate alle lunghezze dei nomi e ai caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="a4253-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="a4253-129">Posizione e gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a4253-129">Location and Resource Group</span></span>
<span data-ttu-id="a4253-130">Usare due variabili per definire l'area dei dati e il gruppo di risorse in cui verranno create le altre risorse per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="a4253-131">Modificare in base alle esigenze specifiche e quindi eseguire i cmdlet seguenti per inizializzare le variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="a4253-132">Proprietà della risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a4253-132">Storage properties</span></span>
<span data-ttu-id="a4253-133">Usare le variabili seguenti per definire l'account di archiviazione e il tipo di risorsa di archiviazione che devono essere usati dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="a4253-134">Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="a4253-135">Si noti che in questo esempio viene usata l' [Archiviazione Premium](../../../storage/common/storage-premium-storage.md), consigliata per carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="a4253-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="a4253-136">Per informazioni dettagliate su questa e su altre indicazioni, vedere [Procedure consigliate per le prestazioni per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a4253-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="a4253-137">Proprietà di rete</span><span class="sxs-lookup"><span data-stu-id="a4253-137">Network properties</span></span>
<span data-ttu-id="a4253-138">Usare le variabili seguenti per definire l'interfaccia di rete, il metodo di allocazione TCP/IP, il nome della rete virtuale, il nome della subnet virtuale, l'intervallo di indirizzi IP per la rete virtuale, l'intervallo di indirizzi IP per la subnet e l'etichetta del nome del dominio pubblico che devono essere usati dalla rete nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="a4253-139">Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="a4253-140">Proprietà della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-140">Virtual machine properties</span></span>
<span data-ttu-id="a4253-141">Usare le variabili seguenti per definire il nome della macchina virtuale, il nome del computer, le dimensioni della macchina virtuale e il nome del disco del sistema operativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="a4253-142">Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="a4253-143">Proprietà dell'immagine</span><span class="sxs-lookup"><span data-stu-id="a4253-143">Image properties</span></span>
<span data-ttu-id="a4253-144">Usare le variabili seguenti per definire l'immagine da usare per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="a4253-145">In questo esempio viene usata l'immagine di SQL Server 2016 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a4253-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="a4253-146">Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.</span><span class="sxs-lookup"><span data-stu-id="a4253-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="a4253-147">Si noti che è possibile ottenere un elenco completo di immagini di SQL Server disponibili con il comando Get-AzureRmVMImageOffer:</span><span class="sxs-lookup"><span data-stu-id="a4253-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="a4253-148">È anche possibile visualizzare gli SKU disponibili per un'offerta con il comando Get-AzureRmVMImageSku.</span><span class="sxs-lookup"><span data-stu-id="a4253-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="a4253-149">Il comando seguente mostra tutti gli SKU disponibili per l'offerta **SQL2014SP1-WS2012R2** .</span><span class="sxs-lookup"><span data-stu-id="a4253-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="a4253-150">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a4253-150">Create a resource group</span></span>
<span data-ttu-id="a4253-151">Il primo oggetto creato con il modello di distribuzione Resource Manager è il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4253-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="a4253-152">Verrà usato il cmdlet [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) per creare un gruppo di risorse di Azure e le rispettive risorse, con nome e posizione del gruppo di risorse definiti dalle variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-152">We will use the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="a4253-153">Eseguire il cmdlet seguente per creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4253-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="a4253-154">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a4253-154">Create a storage account</span></span>
<span data-ttu-id="a4253-155">La macchina virtuale richiede risorse di archiviazione per il disco del sistema operativo e per i file di dati e di log di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4253-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="a4253-156">Per semplificare, verrà creato un singolo disco per entrambi.</span><span class="sxs-lookup"><span data-stu-id="a4253-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="a4253-157">Successivamente è possibile collegare dischi aggiuntivi usando il cmdlet [Add-Azure Disk](/powershell/module/azure/add-azuredisk) per posizionare i file di dati e di log di SQL Server in dischi dedicati.</span><span class="sxs-lookup"><span data-stu-id="a4253-157">You can attach additional disks later using the [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="a4253-158">Verrà usato il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) per creare un account di archiviazione standard nel nuovo gruppo di risorse, con il nome dell'account di archiviazione, il nome dello SKU di storage e la posizione definiti usando le variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-158">We will use the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="a4253-159">Eseguire il cmdlet seguente per creare il nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a4253-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="a4253-160">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="a4253-160">Create network resources</span></span>
<span data-ttu-id="a4253-161">La macchina virtuale richiede alcune risorse di rete per la connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="a4253-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="a4253-162">Ogni macchina virtuale richiede una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="a4253-163">In una rete virtuale deve essere definita almeno una subnet.</span><span class="sxs-lookup"><span data-stu-id="a4253-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="a4253-164">È necessario che sia definita un'interfaccia di rete con un indirizzo IP pubblico o privato.</span><span class="sxs-lookup"><span data-stu-id="a4253-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="a4253-165">Creare una configurazione di subnet di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="a4253-166">Creare prima di tutto una configurazione di subnet per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="a4253-167">Per l'esercitazione verrà creata una subnet predefinita mediante il cmdlet [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) .</span><span class="sxs-lookup"><span data-stu-id="a4253-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="a4253-168">La configurazione di subnet di rete virtuale verrà creata con il nome di subnet e il prefisso di indirizzo definiti usando le variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="a4253-169">È possibile definire altre proprietà della configurazione della subnet della rete virtuale usando questo cmdlet, ma questa operazione non rientra nell'ambito dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4253-169">You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="a4253-170">Eseguire il cmdlet seguente per creare la configurazione di subnet virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="a4253-171">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-171">Create a virtual network</span></span>
<span data-ttu-id="a4253-172">Verrà quindi creata la rete virtuale mediante il cmdlet [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) .</span><span class="sxs-lookup"><span data-stu-id="a4253-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="a4253-173">La rete virtuale verrà creata nel nuovo gruppo di risorse, con nome, posizione e prefisso di indirizzo definiti usando le variabili inizializzate in precedenza e con la configurazione di subnet definita nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="a4253-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="a4253-174">Eseguire il cmdlet seguente per creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="a4253-175">Creare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="a4253-175">Create the public IP address</span></span>
<span data-ttu-id="a4253-176">Dopo avere definito la rete virtuale, è necessario configurare un indirizzo IP per la connettività alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="a4253-177">Per questa esercitazione verrà creato un indirizzo IP pubblico mediante indirizzi IP dinamici per supportare la connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="a4253-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="a4253-178">Verrà usato il cmdlet [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) per creare l'indirizzo IP pubblico nel gruppo di risorse creato in precedenza e con nome, posizione, metodo di allocazione ed etichetta del nome di dominio DNS definiti usando le variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-178">We will use the [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="a4253-179">È possibile definire altre proprietà dell'indirizzo IP pubblico usando questo cmdlet, ma questa operazione non rientra nell'ambito dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4253-179">You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial.</span></span> <span data-ttu-id="a4253-180">È anche possibile creare un indirizzo privato o un indirizzo di tipo statico, ma anche questa procedura non rientra nell'ambito dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4253-180">You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="a4253-181">Eseguire il cmdlet seguente per creare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a4253-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="a4253-182">Creare l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="a4253-182">Create the network interface</span></span>
<span data-ttu-id="a4253-183">È ora possibile creare l'interfaccia di rete che verrà usata dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="a4253-184">Verrà usato il cmdlet [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per creare l'interfaccia di rete nel gruppo di risorse creato in precedenza e con nome, posizione, subnet e indirizzo IP pubblico definiti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-184">We will use the [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="a4253-185">Eseguire il cmdlet seguente per creare l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a4253-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="a4253-186">Configurare un oggetto VM</span><span class="sxs-lookup"><span data-stu-id="a4253-186">Configure a VM object</span></span>
<span data-ttu-id="a4253-187">Dopo avere definito le risorse di archiviazione e di rete, è possibile definire le risorse di calcolo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="a4253-188">Per questa esercitazione verranno specificate le dimensioni della macchina virtuale e alcune proprietà del sistema operativo, verrà specificata l'interfaccia di rete creata in precedenza, verrà definito l'archivio BLOB e verrà quindi specificato il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a4253-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="a4253-189">Creare l'oggetto macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-189">Create the VM object</span></span>
<span data-ttu-id="a4253-190">Specificare prima di tutto le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="a4253-191">Per questa esercitazione verrà specificata l'opzione DS13.</span><span class="sxs-lookup"><span data-stu-id="a4253-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="a4253-192">Verrà usato il cmdlet [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) per creare un oggetto macchina virtuale configurabile con nome e dimensioni definiti usando le variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-192">We will use the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="a4253-193">Eseguire il cmdlet seguente per creare l'oggetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="a4253-194">Creare un oggetto credenziali per includere il nome e la password per le credenziali di amministratore locale</span><span class="sxs-lookup"><span data-stu-id="a4253-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="a4253-195">Prima di configurare le proprietà del sistema operativo per la macchina virtuale, è necessario specificare le credenziali per l'account di amministratore locale sotto forma di stringa sicura.</span><span class="sxs-lookup"><span data-stu-id="a4253-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="a4253-196">Per ottenere questo risultato, usare il cmdlet [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a4253-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="a4253-197">Eseguire il cmdlet seguente e nella finestra della richiesta di credenziali di Windows PowerShell immettere il nome e la password da usare per l'account di amministratore locale nella macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="a4253-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="a4253-198">Configurare le proprietà del sistema operativo per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="a4253-199">È ora possibile configurare le proprietà del sistema operativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="a4253-200">Verrà usato il cmdlet [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) per configurare il tipo di sistema operativo come Windows, richiedere l'installazione dell'[agente di macchine virtuali](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), specificare che il cmdlet abilita l'aggiornamento automatico e configurare il nome della macchina virtuale, il nome del computer e le credenziali usando le variabili inizializzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-200">We will use the [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="a4253-201">Eseguire il cmdlet seguente per configurare le proprietà del sistema operativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="a4253-202">Aggiungere l'interfaccia di rete alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="a4253-203">Verrà quindi aggiunta alla macchina virtuale l'interfaccia di rete creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="a4253-204">Verrà usato il cmdlet [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) per aggiungere l'interfaccia di rete utilizzando la variabile di interfaccia di rete definita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-204">We will use the [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="a4253-205">Eseguire il cmdlet seguente per configurare l'interfaccia di rete per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="a4253-206">Impostare la posizione dell'archivio BLOB per il disco da usare per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="a4253-207">Verrà quindi impostata la posizione dell'archivio BLOB per il disco che verrà usato dalla macchina virtuale usando le variabili definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="a4253-208">Eseguire il cmdlet seguente per impostare la posizione dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="a4253-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="a4253-209">Configurare le proprietà del disco del sistema operativo per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="a4253-210">Verranno quindi configurate le proprietà del disco del sistema operativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="a4253-211">Verrà usato il cmdlet [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) per specificare che il sistema operativo per la macchina virtuale deriverà da un'immagine, per configurare la memorizzazione nella cache su sola lettura, perché SQL Server viene installato nello stesso disco e per definire il nome della macchina virtuale e il disco del sistema operativo specificati usando le variabili definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-211">We will use the [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="a4253-212">Eseguire il cmdlet seguente per configurare le proprietà del disco del sistema operativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="a4253-213">Specificare l'immagine di piattaforma per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4253-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="a4253-214">L'ultimo passaggio della configurazione consiste nello specificare l'immagine di piattaforma per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="a4253-215">Per l'esercitazione viene usata l'immagine più recente per SQL Server 2016 CTP.</span><span class="sxs-lookup"><span data-stu-id="a4253-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="a4253-216">Verrà usato il cmdlet [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) per utilizzare questa immagine in base a quanto definito dalle variabili definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4253-216">We will use the [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="a4253-217">Eseguire il cmdlet seguente per specificare l'immagine di piattaforma per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="a4253-218">Creare la macchina virtuale SQL</span><span class="sxs-lookup"><span data-stu-id="a4253-218">Create the SQL VM</span></span>
<span data-ttu-id="a4253-219">Al termine della procedura di configurazione, è possibile creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="a4253-220">Verrà usato il cmdlet [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) per creare la macchina virtuale utilizzando le variabili definite.</span><span class="sxs-lookup"><span data-stu-id="a4253-220">We will use the [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="a4253-221">Eseguire il cmdlet seguente per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4253-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="a4253-222">La macchina virtuale viene creata.</span><span class="sxs-lookup"><span data-stu-id="a4253-222">The virtual machine is created.</span></span> <span data-ttu-id="a4253-223">Si noti che viene creato un account di archiviazione standard per la diagnostica dell'avvio, perché l'account di archiviazione specificato per il disco della macchina virtuale è un account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="a4253-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="a4253-224">È ora possibile visualizzare la macchina virtuale nel portale di Azure, per verificarne [l'indirizzo IP pubblico e il nome di dominio completo](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a4253-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="a4253-225">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a4253-225">Example script</span></span>
<span data-ttu-id="a4253-226">Lo script seguente contiene lo script PowerShell completo per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4253-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="a4253-227">Si presuppone che sia stata già impostata la sottoscrizione di Azure da usare con i comandi **Add-AzureRmAccount** e **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="a4253-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="a4253-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4253-228">Next steps</span></span>
<span data-ttu-id="a4253-229">Dopo la creazione della macchina virtuale, è possibile connettersi alla macchina virtuale mediante RDP e configurare la connettività.</span><span class="sxs-lookup"><span data-stu-id="a4253-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="a4253-230">Per altre informazioni, vedere [Connettersi a una macchina virtuale di SQL Server in Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a4253-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

