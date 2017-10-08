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
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portale](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come una singola macchina virtuale di Azure utilizzando toocreate hello **Azure Resource Manager** modello di distribuzione utilizzando i cmdlet PowerShell di Azure. In questa esercitazione si creerà una singola macchina virtuale utilizzando una singola unità disco da un'immagine in hello raccolta SQL. Si creerà nuovi provider per l'archiviazione di hello, rete e risorse di calcolo che verranno utilizzate dalla macchina virtuale hello. Se esistono già provider per queste risorse, è possibile usarli.

Se è necessario hello versione classica di questo argomento, vedere [il provisioning di una macchina virtuale di SQL Server utilizzando PowerShell di Azure classico](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Prerequisiti
Per questa esercitazione occorrono:

* Un account e una sottoscrizione di Azure prima di iniziare. Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview), versione 1.4.0 o successiva. Questa esercitazione usa la versione 1.5.0.
  * tooretrieve la versione, il tipo **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configurare la sottoscrizione
Aprire Windows PowerShell e stabilire tooyour accesso account Azure eseguendo i seguenti cmdlet hello. Verrà visualizzata con un segno di schermata tooenter le credenziali. Utilizzare hello stesso messaggio di posta elettronica e la password usati toosign in toohello portale di Azure.

    Add-AzureRmAccount

Dopo l'accesso correttamente verranno visualizzate alcune informazioni sullo schermo che include l'ID sottoscrizione hello con cui hai effettuato l'accesso. Si tratta di sottoscrizione hello in cui le risorse di hello per questa esercitazione verranno create a meno che non si modifica una sottoscrizione diversa tooa. Se si dispone di più ID sottoscrizione, eseguire un elenco di tutti l'ID sottoscrizione hello tooreturn cmdlet seguenti:

    Get-AzureRmSubscription

tooanother toochange ID sottoscrizione, eseguire hello seguente cmdlet con l'ID di sottoscrizione desiderata.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definire le variabili di immagine
toosimplify usabilità e nella conoscenza dello script hello completata da questa esercitazione, si inizierà definendo una serie di variabili. Modificare i valori di parametro hello quando si ritengono appropriato, ma fare attenzione alle lunghezze di tooname correlati restrizioni dei nomi e i caratteri speciali quando si modificano i valori hello forniti.

### <a name="location-and-resource-group"></a>Posizione e gruppo di risorse
Utilizzare due variabili toodefine hello dati hello e area del gruppo di risorse in cui si creerà hello altre risorse per la macchina virtuale hello.

Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Proprietà della risorsa di archiviazione
Utilizzare hello seguenti variabili toodefine hello storage account e hello il tipo di archiviazione toobe usata dalla macchina virtuale hello.

Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili. Si noti che in questo esempio viene usata l' [Archiviazione Premium](../../../storage/common/storage-premium-storage.md), consigliata per carichi di lavoro di produzione. Per informazioni dettagliate su questa e su altre indicazioni, vedere [Procedure consigliate per le prestazioni per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Proprietà di rete
Utilizzare hello seguendo l'interfaccia di rete variabili toodefine hello, metodo di allocazione hello TCP/IP, nome di rete virtuale hello, il nome di subnet virtuale hello, hello intervallo di indirizzi IP per rete virtuale hello, hello intervallo di indirizzi IP per subnet hello e hello utilizzata dalla rete hello nella macchina virtuale hello toobe etichetta nome di dominio pubblico.

Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Proprietà della macchina virtuale
Utilizzare hello seguente nome della macchina virtuale hello toodefine variabili, nome del computer hello, dimensioni della macchina virtuale hello e nome hello del disco del sistema operativo per la macchina virtuale hello.

Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Proprietà dell'immagine
Utilizzare hello seguenti variabili toodefine hello immagine toouse per la macchina virtuale hello. In questo esempio viene utilizzata l'immagine di SQL Server 2016 Enterprise Edition di hello.

Modificare come desiderato e quindi eseguire hello seguente cmdlet tooinitialize queste variabili.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Si noti che è possibile ottenere un elenco completo delle offerte di immagine di SQL Server con il comando Get-AzureRmVMImageOffer hello:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

Ed è possibile visualizzare hello SKU disponibile per un'offerta con il comando Get-AzureRmVMImageSku hello. comando che segue Hello Mostra tutti gli SKU disponibili per hello **SQL2014SP1 WS2012R2** offrono.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Con modello di distribuzione di gestione risorse hello, hello prima che l'oggetto creato è il gruppo di risorse hello. Si utilizzerà hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate cmdlet un gruppo di risorse di Azure e le risorse con risorse hello del gruppo di nome e il percorso definito dalle variabili hello che è stato inizializzato in precedenza.

Eseguire hello cmdlet toocreate dopo il nuovo gruppo di risorse.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
macchina virtuale Hello richiede risorse di archiviazione per disco del sistema operativo hello e hello dati di SQL Server e i file di log. Per semplificare, verrà creato un singolo disco per entrambi. È possibile collegare dischi aggiuntivi in un secondo momento utilizzando hello [Azure-Aggiungi disco](/powershell/module/azure/add-azuredisk) cmdlet in ordine tooplace i dati di SQL Server e i file di registro in dischi dedicati. Si utilizzerà hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate cmdlet un'archiviazione standard account nel nuovo gruppo di risorse e con nome di account di archiviazione hello, nome Sku di archiviazione e posizione definita utilizzo di variabili hello in precedenza è stato inizializzato.

Eseguire hello cmdlet toocreate dopo il nuovo account di archiviazione.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Creare risorse di rete
macchina virtuale Hello richiede un numero di risorse di rete per la connettività di rete.

* Ogni macchina virtuale richiede una rete virtuale.
* In una rete virtuale deve essere definita almeno una subnet.
* È necessario che sia definita un'interfaccia di rete con un indirizzo IP pubblico o privato.

### <a name="create-a-virtual-network-subnet-configuration"></a>Creare una configurazione di subnet di rete virtuale
Creare prima di tutto una configurazione di subnet per la rete virtuale. Per questa esercitazione si creerà una subnet predefinita utilizzando hello [New AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. La configurazione di subnet della rete virtuale verrà creata con hello nome e indirizzo prefisso di subnet definito utilizzando le variabili hello è inizializzata in precedenza.

> [!NOTE]
> È possibile definire proprietà aggiuntive di configurazione della subnet di rete virtuale hello utilizzando questo cmdlet, ma che non rientra hello ambito di questa esercitazione.
>
>

Eseguire hello cmdlet toocreate dopo la configurazione di subnet virtuale.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Crea rete virtuale
Successivamente, si creerà la rete virtuale utilizzando hello [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. Verrà creata la rete virtuale nel nuovo gruppo di risorse, con prefisso di indirizzo definito utilizzando variabili di hello che è stato inizializzato in precedenza e utilizzando la configurazione di subnet hello è definito nel passaggio precedente hello, percorso e nome hello.

Eseguire hello seguente cmdlet toocreate la rete virtuale.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Creare l'indirizzo IP pubblico hello
Ora che è disponibile la rete virtuale definita, è necessario tooconfigure un indirizzo IP per la macchina virtuale toohello di connettività. Per questa esercitazione si creerà un indirizzo IP pubblico utilizzando l'indirizzo IP dinamico addressing toosupport connettività Internet. Si utilizzerà hello [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello indirizzo IP pubblico in hello risorsa gruppo creato prevously e con nome hello, percorso, il metodo di allocazione ed etichetta del nome di dominio DNS definito tramite hello variabili che è stato inizializzato in precedenza.

> [!NOTE]
> È possibile definire proprietà aggiuntive dell'indirizzo IP pubblico hello utilizzando questo cmdlet, ma che non rientra hello ambito di questa esercitazione iniziale. È inoltre possibile creare un indirizzo privato o un indirizzo con un indirizzo statico, ma è anche esula hello in questa esercitazione.
>
>

Eseguire hello seguente cmdlet toocreate l'indirizzo IP pubblico.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Creare l'interfaccia di rete hello
Si sono ora pronti toocreate interfaccia di rete hello che utilizzerà la macchina virtuale. Si utilizzerà hello [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate cmdlet l'interfaccia di rete nel gruppo di risorse hello creato in precedenza e con nome hello, percorso, subnet e indirizzi IP pubblici definiti in precedenza.

Eseguire hello seguente cmdlet toocreate l'interfaccia di rete.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configurare un oggetto VM
Ora che si dispone di risorse di archiviazione e di rete definite, ci sono risorse di calcolo toodefine pronto per la macchina virtuale hello. Per questa esercitazione, si verrà specificare varie proprietà del sistema operativo e dimensioni della macchina virtuale hello, specificare hello interfaccia di rete che è stati creati in precedenza, definire nell'archiviazione blob e quindi specificare disco del sistema operativo hello.

### <a name="create-hello-vm-object"></a>Creare l'oggetto macchina virtuale hello
Si inizierà specificando la dimensione di macchina virtuale hello. Per questa esercitazione verrà specificata l'opzione DS13. Si utilizzerà hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate cmdlet un oggetto macchina virtuale può essere configurato con nome hello e dimensioni definiti utilizzando le variabili hello è inizializzata in precedenza.

Eseguire hello seguente oggetto macchina virtuale di cmdlet toocreate hello.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Creare un nome delle credenziali oggetto toohold hello e una password per le credenziali di amministratore locale hello
Prima che è possibile impostare proprietà del sistema operativo per la macchina virtuale hello hello, dobbiamo credenziali hello toosupply per account di amministratore locale hello come stringa sicura. tooaccomplish, si utilizzerà hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Eseguire hello seguente cmdlet e, nella finestra di richiesta delle credenziali di Windows PowerShell hello, digitare hello toouse di nome e una password per account di amministratore locale hello nella macchina virtuale di Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Impostare le proprietà del sistema operativo hello per la macchina virtuale hello
Ora siamo proprietà del sistema operativo della macchina virtuale hello di tooset pronto. Si utilizzerà hello [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) tipo hello tooset di cmdlet del sistema operativo di Windows, richiedono hello [agente della macchina virtuale](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installato, specificare tale cmdlet hello consente auto aggiornare e impostare il nome di macchina virtuale hello, nome del computer hello e le credenziali di hello utilizzare variabili hello che è stato inizializzato in precedenza.

Eseguire hello cmdlet tooset hello del sistema operativo le proprietà seguenti per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Aggiungere la macchina virtuale hello rete interfaccia toohello
A questo punto si aggiungerà l'interfaccia di rete hello creata in precedenza macchina virtuale toohello. Si utilizzerà hello [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet interfaccia di rete hello tooadd utilizzando una variabile dell'interfaccia di rete hello definita in precedenza.

Eseguire hello seguente interfaccia di rete hello tooset cmdlet per la macchina virtuale.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Imposta percorso di archiviazione blob di hello per hello disco toobe usata dalla macchina virtuale hello
Successivamente, si imposterà percorso di archiviazione blob di hello per hello disco toobe usata dalla macchina virtuale hello utilizzando variabili di hello è definito in precedenza.

Eseguire hello seguente percorso di archiviazione blob di cmdlet tooset hello.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Set di proprietà del disco per la macchina virtuale hello hello del sistema operativo
Successivamente, verranno impostate hello del sistema operativo su disco per la macchina virtuale hello. Si utilizzerà hello [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet che il sistema operativo per la macchina virtuale hello hello in provengono da un'immagine, la memorizzazione nella cache solo tooread tooset (perché SQL Server viene installato sul hello stesso disco) e definire nome della macchina virtuale Hello e disco del sistema operativo hello definita utilizzando le variabili di hello definita in precedenza.

Eseguire hello cmdlet tooset hello del sistema operativo disco le proprietà seguenti per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Specificare l'immagine della piattaforma per la macchina virtuale hello hello
L'ultimo passaggio di configurazione è l'immagine della piattaforma hello toospecify per la macchina virtuale. Immagine di SQL Server 2016 CTP più recente di hello viene usato per questa esercitazione. Si utilizzerà hello [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse cmdlet questa immagine come definito dalle variabili hello definita in precedenza.

Eseguire hello seguente immagine della piattaforma hello toospecify cmdlet per la macchina virtuale.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Creare VM SQL hello
Dopo aver completato i passaggi di configurazione hello, si è macchina virtuale di hello toocreate pronto. Si utilizzerà hello [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello macchina virtuale utilizzando variabili di hello che sono state definite.

Eseguire hello seguente cmdlet toocreate la macchina virtuale.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

macchina virtuale Hello viene creato. Si noti che viene creato un account di archiviazione standard per la diagnostica di avvio perché hello specificato l'account di archiviazione per il disco della macchina virtuale hello è un account di archiviazione premium.

È ora possibile visualizzare la macchina in hello Azure Portal toosee [l'indirizzo IP pubblico e il relativo nome di dominio completo](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Script di esempio
Hello lo script seguente contiene script di PowerShell hello completo per questa esercitazione. Si presuppone che si disponga già di installazione hello sottoscrizione di Azure toouse con hello **Aggiungi AzureRmAccount** e **selezionare AzureRmSubscription** comandi.

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

## <a name="next-steps"></a>Passaggi successivi
Dopo la creazione di macchine virtuali hello, si è pronti tooconnect macchina virtuale di toohello tramite connettività RDP e il programma di installazione. Per ulteriori informazioni, vedere [connessione macchina virtuale di SQL Server in Azure (gestione delle risorse) tooa](virtual-machines-windows-sql-connect.md).

