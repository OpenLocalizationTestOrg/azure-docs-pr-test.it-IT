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
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portale](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Panoramica
Questa esercitazione illustra come creare una singola macchina virtuale di Azure usando il modello di distribuzione **Azure Resource Manager** con i cmdlet di Azure PowerShell. In questa esercitazione verrà creata una singola macchina virtuale con una singola unità disco da un'immagine di SQL Gallery. Verranno creati nuovi provider per le risorse di archiviazione, rete e calcolo che verranno usate dalla macchina virtuale. Se esistono già provider per queste risorse, è possibile usarli.

Se è necessaria la versione classica di questo argomento, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (classico)](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Prerequisiti
Per questa esercitazione occorrono:

* Un account e una sottoscrizione di Azure prima di iniziare. Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview), versione 1.4.0 o successiva. Questa esercitazione usa la versione 1.5.0.
  * Per recuperare la versione, digitare **Get-Module Azure -ListAvailable**.

## <a name="configure-your-subscription"></a>Configurare la sottoscrizione
Aprire Windows PowerShell e accedere all'account Azure eseguendo il cmdlet seguente. Verrà visualizzata una schermata di accesso per immettere le credenziali. Utilizzare lo stesso indirizzo email e password utilizzati per accedere al portale di Azure.

    Add-AzureRmAccount

Dopo aver effettuato l'accesso, sullo schermo verranno visualizzate informazioni tra cui il valore SubscriptionId usato per l'accesso. Si tratta della sottoscrizione in cui verranno create le risorse per questa esercitazione, a meno che non si specifichi una sottoscrizione diversa. Se sono presenti più valori SubscriptionId, eseguire il cmdlet seguente per restituire un elenco di tutti i valori SubscriptionId:

    Get-AzureRmSubscription

Per passare a un altro SubscriptionId, eseguire il cmdlet seguente con il valore SubscriptionId desiderato.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definire le variabili di immagine
Per facilitare l'uso e la comprensione dello script completo di questa esercitazione, verranno prima di tutto definite alcune variabili. Cambiare i valori dei parametri in base alla necessità, ma quando si modificano i valori forniti occorre prestare attenzione alle restrizioni di denominazione correlate alle lunghezze dei nomi e ai caratteri speciali.

### <a name="location-and-resource-group"></a>Posizione e gruppo di risorse
Usare due variabili per definire l'area dei dati e il gruppo di risorse in cui verranno create le altre risorse per la macchina virtuale.

Modificare in base alle esigenze specifiche e quindi eseguire i cmdlet seguenti per inizializzare le variabili.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Proprietà della risorsa di archiviazione
Usare le variabili seguenti per definire l'account di archiviazione e il tipo di risorsa di archiviazione che devono essere usati dalla macchina virtuale.

Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili. Si noti che in questo esempio viene usata l' [Archiviazione Premium](../../../storage/common/storage-premium-storage.md), consigliata per carichi di lavoro di produzione. Per informazioni dettagliate su questa e su altre indicazioni, vedere [Procedure consigliate per le prestazioni per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Proprietà di rete
Usare le variabili seguenti per definire l'interfaccia di rete, il metodo di allocazione TCP/IP, il nome della rete virtuale, il nome della subnet virtuale, l'intervallo di indirizzi IP per la rete virtuale, l'intervallo di indirizzi IP per la subnet e l'etichetta del nome del dominio pubblico che devono essere usati dalla rete nella macchina virtuale.

Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Proprietà della macchina virtuale
Usare le variabili seguenti per definire il nome della macchina virtuale, il nome del computer, le dimensioni della macchina virtuale e il nome del disco del sistema operativo per la macchina virtuale.

Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Proprietà dell'immagine
Usare le variabili seguenti per definire l'immagine da usare per la macchina virtuale. In questo esempio viene usata l'immagine di SQL Server 2016 Enterprise.

Modificare in base alle esigenze specifiche e quindi eseguire il cmdlet seguente per inizializzare le variabili.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Si noti che è possibile ottenere un elenco completo di immagini di SQL Server disponibili con il comando Get-AzureRmVMImageOffer:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

È anche possibile visualizzare gli SKU disponibili per un'offerta con il comando Get-AzureRmVMImageSku. Il comando seguente mostra tutti gli SKU disponibili per l'offerta **SQL2014SP1-WS2012R2** .

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Il primo oggetto creato con il modello di distribuzione Resource Manager è il gruppo di risorse. Verrà usato il cmdlet [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) per creare un gruppo di risorse di Azure e le rispettive risorse, con nome e posizione del gruppo di risorse definiti dalle variabili inizializzate in precedenza.

Eseguire il cmdlet seguente per creare un nuovo gruppo di risorse.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
La macchina virtuale richiede risorse di archiviazione per il disco del sistema operativo e per i file di dati e di log di SQL Server. Per semplificare, verrà creato un singolo disco per entrambi. Successivamente è possibile collegare dischi aggiuntivi usando il cmdlet [Add-Azure Disk](/powershell/module/azure/add-azuredisk) per posizionare i file di dati e di log di SQL Server in dischi dedicati. Verrà usato il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) per creare un account di archiviazione standard nel nuovo gruppo di risorse, con il nome dell'account di archiviazione, il nome dello SKU di storage e la posizione definiti usando le variabili inizializzate in precedenza.

Eseguire il cmdlet seguente per creare il nuovo account di archiviazione.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Creare risorse di rete
La macchina virtuale richiede alcune risorse di rete per la connettività di rete.

* Ogni macchina virtuale richiede una rete virtuale.
* In una rete virtuale deve essere definita almeno una subnet.
* È necessario che sia definita un'interfaccia di rete con un indirizzo IP pubblico o privato.

### <a name="create-a-virtual-network-subnet-configuration"></a>Creare una configurazione di subnet di rete virtuale
Creare prima di tutto una configurazione di subnet per la rete virtuale. Per l'esercitazione verrà creata una subnet predefinita mediante il cmdlet [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) . La configurazione di subnet di rete virtuale verrà creata con il nome di subnet e il prefisso di indirizzo definiti usando le variabili inizializzate in precedenza.

> [!NOTE]
> È possibile definire altre proprietà della configurazione della subnet della rete virtuale usando questo cmdlet, ma questa operazione non rientra nell'ambito dell'esercitazione.
>
>

Eseguire il cmdlet seguente per creare la configurazione di subnet virtuale.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Crea rete virtuale
Verrà quindi creata la rete virtuale mediante il cmdlet [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) . La rete virtuale verrà creata nel nuovo gruppo di risorse, con nome, posizione e prefisso di indirizzo definiti usando le variabili inizializzate in precedenza e con la configurazione di subnet definita nel passaggio precedente.

Eseguire il cmdlet seguente per creare la rete virtuale.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a>Creare l'indirizzo IP pubblico
Dopo avere definito la rete virtuale, è necessario configurare un indirizzo IP per la connettività alla macchina virtuale. Per questa esercitazione verrà creato un indirizzo IP pubblico mediante indirizzi IP dinamici per supportare la connettività Internet. Verrà usato il cmdlet [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) per creare l'indirizzo IP pubblico nel gruppo di risorse creato in precedenza e con nome, posizione, metodo di allocazione ed etichetta del nome di dominio DNS definiti usando le variabili inizializzate in precedenza.

> [!NOTE]
> È possibile definire altre proprietà dell'indirizzo IP pubblico usando questo cmdlet, ma questa operazione non rientra nell'ambito dell'esercitazione. È anche possibile creare un indirizzo privato o un indirizzo di tipo statico, ma anche questa procedura non rientra nell'ambito dell'esercitazione.
>
>

Eseguire il cmdlet seguente per creare l'indirizzo IP pubblico.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a>Creare l'interfaccia di rete
È ora possibile creare l'interfaccia di rete che verrà usata dalla macchina virtuale. Verrà usato il cmdlet [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per creare l'interfaccia di rete nel gruppo di risorse creato in precedenza e con nome, posizione, subnet e indirizzo IP pubblico definiti in precedenza.

Eseguire il cmdlet seguente per creare l'interfaccia di rete.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configurare un oggetto VM
Dopo avere definito le risorse di archiviazione e di rete, è possibile definire le risorse di calcolo per la macchina virtuale. Per questa esercitazione verranno specificate le dimensioni della macchina virtuale e alcune proprietà del sistema operativo, verrà specificata l'interfaccia di rete creata in precedenza, verrà definito l'archivio BLOB e verrà quindi specificato il disco del sistema operativo.

### <a name="create-the-vm-object"></a>Creare l'oggetto macchina virtuale
Specificare prima di tutto le dimensioni della macchina virtuale. Per questa esercitazione verrà specificata l'opzione DS13. Verrà usato il cmdlet [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) per creare un oggetto macchina virtuale configurabile con nome e dimensioni definiti usando le variabili inizializzate in precedenza.

Eseguire il cmdlet seguente per creare l'oggetto macchina virtuale.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a>Creare un oggetto credenziali per includere il nome e la password per le credenziali di amministratore locale
Prima di configurare le proprietà del sistema operativo per la macchina virtuale, è necessario specificare le credenziali per l'account di amministratore locale sotto forma di stringa sicura. Per ottenere questo risultato, usare il cmdlet [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .

Eseguire il cmdlet seguente e nella finestra della richiesta di credenziali di Windows PowerShell immettere il nome e la password da usare per l'account di amministratore locale nella macchina virtuale Windows.

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a>Configurare le proprietà del sistema operativo per la macchina virtuale
È ora possibile configurare le proprietà del sistema operativo per la macchina virtuale. Verrà usato il cmdlet [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) per configurare il tipo di sistema operativo come Windows, richiedere l'installazione dell'[agente di macchine virtuali](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), specificare che il cmdlet abilita l'aggiornamento automatico e configurare il nome della macchina virtuale, il nome del computer e le credenziali usando le variabili inizializzate in precedenza.

Eseguire il cmdlet seguente per configurare le proprietà del sistema operativo per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a>Aggiungere l'interfaccia di rete alla macchina virtuale
Verrà quindi aggiunta alla macchina virtuale l'interfaccia di rete creata in precedenza. Verrà usato il cmdlet [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) per aggiungere l'interfaccia di rete utilizzando la variabile di interfaccia di rete definita in precedenza.

Eseguire il cmdlet seguente per configurare l'interfaccia di rete per la macchina virtuale.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a>Impostare la posizione dell'archivio BLOB per il disco da usare per la macchina virtuale
Verrà quindi impostata la posizione dell'archivio BLOB per il disco che verrà usato dalla macchina virtuale usando le variabili definite in precedenza.

Eseguire il cmdlet seguente per impostare la posizione dell'archivio BLOB.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a>Configurare le proprietà del disco del sistema operativo per la macchina virtuale
Verranno quindi configurate le proprietà del disco del sistema operativo per la macchina virtuale. Verrà usato il cmdlet [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) per specificare che il sistema operativo per la macchina virtuale deriverà da un'immagine, per configurare la memorizzazione nella cache su sola lettura, perché SQL Server viene installato nello stesso disco e per definire il nome della macchina virtuale e il disco del sistema operativo specificati usando le variabili definite in precedenza.

Eseguire il cmdlet seguente per configurare le proprietà del disco del sistema operativo per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a>Specificare l'immagine di piattaforma per la macchina virtuale
L'ultimo passaggio della configurazione consiste nello specificare l'immagine di piattaforma per la macchina virtuale. Per l'esercitazione viene usata l'immagine più recente per SQL Server 2016 CTP. Verrà usato il cmdlet [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) per utilizzare questa immagine in base a quanto definito dalle variabili definite in precedenza.

Eseguire il cmdlet seguente per specificare l'immagine di piattaforma per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a>Creare la macchina virtuale SQL
Al termine della procedura di configurazione, è possibile creare la macchina virtuale. Verrà usato il cmdlet [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) per creare la macchina virtuale utilizzando le variabili definite.

Eseguire il cmdlet seguente per creare la macchina virtuale.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

La macchina virtuale viene creata. Si noti che viene creato un account di archiviazione standard per la diagnostica dell'avvio, perché l'account di archiviazione specificato per il disco della macchina virtuale è un account di archiviazione Premium.

È ora possibile visualizzare la macchina virtuale nel portale di Azure, per verificarne [l'indirizzo IP pubblico e il nome di dominio completo](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Script di esempio
Lo script seguente contiene lo script PowerShell completo per l'esercitazione. Si presuppone che sia stata già impostata la sottoscrizione di Azure da usare con i comandi **Add-AzureRmAccount** e **Select-AzureRmSubscription**.

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

## <a name="next-steps"></a>Passaggi successivi
Dopo la creazione della macchina virtuale, è possibile connettersi alla macchina virtuale mediante RDP e configurare la connettività. Per altre informazioni, vedere [Connettersi a una macchina virtuale di SQL Server in Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).

