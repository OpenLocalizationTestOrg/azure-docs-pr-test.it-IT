---
title: Archiviazione Premium di Azure con SQL Server aaaUse | Documenti Microsoft
description: In questo articolo usa le risorse create con il modello di distribuzione classica hello e vengono fornite istruzioni sull'uso di archiviazione Premium di Azure con SQL Server in esecuzione in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Utilizzare Archiviazione Premium di Azure con SQL Server in macchine virtuali
## <a name="overview"></a>Panoramica
[Archiviazione Premium di Azure](../../../storage/common/storage-premium-storage.md) è hello prossima generazione di archiviazione che fornisce bassa latenza e ad alta velocità effettiva dei / o. Funziona al meglio per i carichi di lavoro con numerose operazioni di I/O, ad esempio SQL Server in [macchine virtuali](https://azure.microsoft.com/services/virtual-machines/)IaaS.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In questo articolo fornisce la pianificazione e indicazioni per la migrazione di una macchina virtuale in esecuzione SQL Server toouse archiviazione Premium. Sono inclusi i passaggi relativi all'infrastruttura di Azure (rete, archiviazione) e alle macchine virtuali guest di Windows. esempio Hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) Mostra una migrazione tooend end completo completa di come toomove maggiore macchine virtuali tootake sfruttare un locale archiviazione sull'unità SSD con PowerShell.

Si tratta toounderstand importante hello end-to-end processo che utilizzano Premium di archiviazione di Azure con SQL Server in macchine virtuali IAAS. Sono inclusi:

* Identificazione dei prerequisiti di hello toouse archiviazione Premium.
* Esempi di distribuzione di SQL Server su IaaS tooPremium archiviazione per nuove distribuzioni.
* Esempi di migrazione delle distribuzioni esistenti, sia di server autonomi che distribuzioni tramite gruppi di disponibilità di SQL AlwaysOn.
* Approcci di migrazione possibili.
* Esempio completo end-to-end che mostra i passaggi di Azure, Windows e SQL Server per la migrazione di hello di un'implementazione di Always On esistente.

Per ottenere le informazioni più esaustive sull'uso di SQL Server in Macchine virtuali di Azure, vedere [SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Autore:** Daniel Sol **Revisori tecnici:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Prerequisiti per Archiviazione Premium
Esistono diversi prerequisiti per l'utilizzo di Archiviazione Premium.

### <a name="machine-size"></a>Dimensioni della macchina
Per l'utilizzo di archiviazione Premium è necessario serie DS toouse macchine virtuali (VM). Se si utilizzano macchine serie DS nel servizio cloud prima di, è necessario eliminare hello macchina virtuale esistente, mantenere i dischi collegato hello e quindi creare un nuovo servizio cloud prima di ricreare hello macchina virtuale come dimensioni del ruolo DS *. Per ulteriori informazioni sulle dimensioni della macchine virtuali, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Servizi cloud
È possibile utilizzare le macchine virtuali DS* con Archiviazione Premium solo quando vengono create in un nuovo servizio cloud. Se si utilizza SQL Server Always On in Azure, hello sempre sul Listener farà riferimento toohello indirizzo interno di Azure o indirizzo IP di bilanciamento del carico esterno che è associata a un servizio cloud. Questo articolo è incentrato sulla toomigrate, mantenendo la disponibilità in questo scenario.

> [!NOTE]
> Una serie DS * deve essere hello prima macchina virtuale che viene distribuito toohello nuovo servizio Cloud.
>
>

### <a name="regional-vnets"></a>Reti virtuali regionali
Per le macchine virtuali DS * è necessario configurare una rete virtuale (VNET) che ospita la macchine virtuali toobe internazionali hello. Questo hello "viene ampliato" rete virtuale è tooallow hello toobe macchine virtuali più grandi il provisioning in altri cluster e consentire la comunicazione tra di essi. Nella seguente schermata di hello, hello evidenziato percorso Mostra regione, mentre il primo risultato hello Mostra una rete virtuale "narrow".

![RegionalVNET][1]

È possibile generare un tooa di toomigrate ticket di supporto Microsoft rete virtuale di regione, Microsoft apportata una modifica, quindi toocomplete hello migrazione tooregional reti virtuali, modificare la proprietà hello AffinityGroup hello configurazione della rete. Prima di tutto esportare hello configurazione di rete in PowerShell e quindi sostituire hello **AffinityGroup** proprietà hello **VirtualNetworkSite** elemento con un **percorso** proprietà. Specificare `Location = XXXX` dove `XXXX` è un'area di Azure. Quindi importare nuova configurazione hello.

Ad esempio, considerare hello seguente configurazione di rete virtuale:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove questo tooa internazionali tra reti VIRTUALI in Europa occidentale, modificare hello toohello di configurazione seguente:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Account di archiviazione
Sarà necessario toocreate un nuovo account di archiviazione è configurato per l'archiviazione Premium. Si noti che utilizzo hello di archiviazione Premium è impostata in account di archiviazione di hello, non su singoli dischi rigidi virtuali, tuttavia quando si utilizza una macchina virtuale serie DS * è possibile collegare i file VHD dall'account di archiviazione Standard e Premium. Se non si desidera tooplace hello disco rigido virtuale del sistema operativo su toohello account di archiviazione Premium, è possibile considerare questo.

esempio Hello **New AzureStorageAccountPowerShell** comando con "Premium_LRS" hello **tipo** crea un Account di archiviazione Premium:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Impostazioni della cache di dischi rigidi virtuali
Hello differenza principale tra la creazione di dischi che fanno parte di un account di archiviazione Premium è impostazione della cache di hello disco. Per i dischi del volume di dati di SQL Server, è consigliabile usare "**Read Caching**". Per i volumi di log delle transazioni, impostazione della cache di hello disco deve essere impostato troppo '**Nessuno**'. Questa è diversa da quelle consigliate hello per gli account di archiviazione Standard.

Dopo aver allegati hello i dischi rigidi virtuali, non è possibile modificare l'impostazione della cache di hello. Si sarebbe necessario toodetach e si ricollega hello disco rigido virtuale con un'impostazione della cache aggiornata.

### <a name="windows-storage-spaces"></a>Spazi di archiviazione di Windows
È possibile utilizzare [spazi di archiviazione di Windows](https://technet.microsoft.com/library/hh831739.aspx) in modo analogo al precedente archiviazione Standard, in questo modo si toomigrate una macchina virtuale che è già utilizzano spazi di archiviazione. esempio Hello in [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (passaggio 9 in poi) illustra hello tooextract codice Powershell e importare una macchina virtuale con più dischi rigidi virtuali collegati.

Pool di archiviazione utilizzati con velocità effettiva tooenhance di account di archiviazione di Azure Standard e ridurre la latenza. Può essere utile testare i pool di archiviazione con Archiviazione Premium per le nuove distribuzioni, ma l’impostazione dell’archiviazione aggiunge ulteriore complessità.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Come toofind toostorage pool di mappare i dischi virtuali di Azure
Vi sono indicazioni di impostazione della cache diverse per i dischi rigidi virtuali collegati, è possibile decidere toocopy hello dischi rigidi virtuali tooa account di archiviazione Premium. Tuttavia, quando si ricollegarli toohello serie DS nuova macchina virtuale, potrebbe essere necessario tooalter le impostazioni della cache di hello. È più semplice hello tooapply che archiviazione Premium consigliata le impostazioni della cache quando si dispone di dischi rigidi virtuali separati per hello SQL dati file e log file (anziché un singolo disco rigido virtuale che contiene entrambi).

> [!NOTE]
> Se si dispone di file di dati e log di SQL Server su hello stesso volume, opzione che si sceglie di memorizzazione nella cache di hello dipende da modelli di accesso i/o hello per i carichi di lavoro del database. Solo i test possono dimostrare quale opzione di memorizzazione nella cache è più adatta a questo scenario.
>
>

Tuttavia, se si utilizza spazi di archiviazione di Windows che sono costituite da più dischi rigidi virtuali è necessario toolook nel tooidentify script originale cui collegata a dischi rigidi virtuali sono in quale pool specifico, pertanto, è quindi possibile impostare le impostazioni della cache di hello conseguenza per ogni disco.

Se non si dispone originale tooshow disponibili di script di cui eseguire il mapping di dischi rigidi virtuali toohello pool di archiviazione, è possibile utilizzare hello dopo il mapping del pool passaggi toodetermine hello/archiviazione su disco.

Per ogni disco, utilizzare hello alla procedura seguente:

1. Ottenere un elenco di dischi collegati tooVM con hello **Get-AzureVM** comando:

    Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. Si noti hello Diskname e al LUN.

    ![DisknameAndLUN][2]
3. Desktop remoto in hello macchina virtuale. Quindi andare troppo**Gestione Computer** | **Gestione dispositivi** | **unità disco**. Esaminare la proprietà hello di ogni hello 'Microsoft dischi virtuali'

    ![VirtualDiskProperties][3]
4. numero LUN Hello qui è un numero LUN toohello riferimento specificato durante il collegamento hello VHD toohello macchina virtuale.
5. Per "Disco virtuale di Microsoft" hello, visitare toohello **dettagli** scheda, quindi hello **proprietà** elenco, andare troppo**chiave Driver**. In hello **valore**, hello nota **Offset**, ovvero 0002 nella seguente schermata hello. Hello 0002 indica hello PhysicalDisk2 che hello riferimenti di pool di archiviazione.

    ![VirtualDiskPropertyDetails][4]
6. Per ogni pool di archiviazione, dump out hello associati dischi:

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

È ora possibile usare questo tooassociate informazioni collegati dischi rigidi virtuali tooPhysical dischi nel pool di archiviazione.

Dopo aver mappato i dischi rigidi virtuali tooPhysical dischi nel pool di archiviazione è quindi possibile scollegare e copiarli su tooa account di archiviazione Premium, quindi collegarli con cache di hello corretta impostazione. Vedere l'esempio hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), i passaggi da 8 a 12. Questi passaggi mostrano come tooextract un VHD associato alla macchina virtuale su disco tooa CSV file di configurazione copiare i dischi rigidi virtuali hello, modificare le impostazioni della cache di hello disco configurazione e infine ridistribuire hello macchina virtuale come macchina virtuale della serie DS con hello tutti i dischi collegati.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Larghezza di banda di archiviazione della VM e velocità effettiva di archiviazione del VHD
Hello le prestazioni di archiviazione dipende hello dimensioni DS * VM specificata e hello dimensioni disco rigido virtuale. macchine virtuali Hello hanno quote diverse per il numero di dischi rigidi virtuali che possono essere collegati e larghezza di banda massima (MB/s) supporteranno hello hello. Per i numeri di hello specifica larghezza di banda, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Input/output al secondo maggiori si ottengono con dimensioni del disco maggiori. Tenere conto di questa considerazione quando si decide il percorso di migrazione. Per informazioni dettagliate, [per IOPS e tipi di disco, vedere la tabella hello](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Infine, tenere presente che le macchine virtuali supporteranno larghezza di banda massime diverse per tutti i dischi collegati. Un carico elevato, è Impossibile saturare hello su disco massimo della larghezza di banda disponibile per la dimensione di ruolo macchina virtuale. Ad esempio un Standard_DS14 supporteranno backup too512MB/s. Pertanto, con tre dischi P30 è Impossibile saturare hello disco larghezza di banda di hello macchina virtuale. Ma in questo esempio, può essere superato il limite di velocità effettiva di hello a seconda della combinazione di hello di lettura e scrittura IOs.

## <a name="new-deployments"></a>Nuove distribuzioni
Hello nelle due sezioni successive viene illustrato come è possibile distribuire le macchine virtuali di SQL Server tooPremium archiviazione. Come accennato in precedenza, non è necessariamente necessario disco del sistema operativo di hello tooplace in archiviazione Premium. Si potrebbe scegliere toodo questa opzione se si sta prendendo in considerazione tooplace i carichi di lavoro con utilizzo intensivo dei / o su disco rigido virtuale del sistema operativo hello.

Hello primo esempio viene illustrato l'utilizzo di immagini della raccolta Azure esistente. Hello secondo esempio viene mostrato come una macchina virtuale personalizzata toouse immagine che si dispone di un account di archiviazione Standard esistente.

> [!NOTE]
> Questi esempi presuppongono che sia già stata creata una rete virtuale regionale.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Creare una nuova macchina virtuale con Archiviazione Premium con immagine della raccolta
esempio Hello riportato di seguito viene illustrato come tooplace hello disco rigido virtuale del sistema operativo in archiviazione premium e collegare i dischi rigidi virtuali di archiviazione Premium. Tuttavia, è possibile inoltre inserire disco del sistema operativo hello in un account di archiviazione Standard e quindi collegare i dischi rigidi virtuali che risiedono in un account di archiviazione Premium. Vengono illustrati entrambi gli scenari.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Passaggio 1: Creare un account di Archiviazione Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Passaggio 2: Creare un nuovo servizio cloud
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Passaggio 3: Riservare un VIP di servizio cloud (facoltativo)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Passaggio 4: Creare un contenitore di macchine virtuali
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Passaggio 5: Collocazione del disco rigido virtuale su Archiviazione Standard o Premium 
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Passaggio 6: Creare la macchina virtuale
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Creare un nuovo toouse VM archiviazione Premium con un'immagine personalizzata
Questo scenario mostra la posizione delle immagini personalizzate esistenti che risiedono in un account di Archiviazione Standard. Come accennato in se si desidera tooplace hello disco rigido virtuale del sistema operativo in archiviazione Premium, sarà necessario toocopy hello immagine che esiste in account di archiviazione Standard hello e li trasferisce tooa archiviazione Premium prima che possa essere utilizzato. Se dispone di un'immagine locale, è possibile inoltre utilizzare questo metodo toocopy che direttamente toohello account di archiviazione Premium.

#### <a name="step-1-create-storage-account"></a>Passaggio 1: Creare l’account di archiviazione
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Passaggio 2: Creare il servizio cloud
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Passaggio 3: Usare l'immagine esistente
È possibile utilizzare un'immagine esistente. In alternativa è possibile [acquisire un'immagine di una macchina esistente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Macchina hello nota che creare l'immagine non dispone di toobe DS * macchina. Dopo aver creato immagine hello, hello seguente procedura mostra come toocopy, account di archiviazione Premium con hello toohello **inizio AzureStorageBlobCopy** cmdlet PowerShell.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Passaggio 4: Copiare BLOB tra account di archiviazione
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Passaggio 5: Verificare regolarmente lo stato della copia:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Passaggio 6: Aggiungere immagini disco tooAzure disco Repository nella sottoscrizione
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> È possibile che anche se i rapporti di stato di hello come esito positivo, è comunque possibile ottenere un errore di lease del disco. In questo caso, attendere circa 10 minuti.
>
>

#### <a name="step-7--build-hello-vm"></a>Passaggio 7: Compilazione hello VM
Qui si sta compilando hello macchina virtuale da un'immagine e collegamento di due dischi rigidi virtuali archiviazione Premium:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Distribuzioni esistenti che non usano i gruppi di disponibilità AlwaysOn
> [!NOTE]
> Per le distribuzioni esistenti, vedere prima hello [prerequisiti](#prerequisites-for-premium-storage) sezione di questo argomento.
>
>

Esistono diverse considerazioni per le distribuzioni di SQL Server che non usano i gruppi di disponibilità AlwaysOn e per quelle che li usano. Se non si usa Always On e un Server SQL autonomo esistente, è possibile aggiornare tooPremium archiviazione utilizzando un nuovo account di servizio e l'archiviazione cloud. prendere in considerazione hello le opzioni seguenti:

* **Creare una nuova macchina virtuale di SQL Server**. È possibile creare una nuova macchina virtuale di SQL Server che utilizza un account di Archiviazione Premium, come documentato in Nuove distribuzioni. Eseguire quindi il backup e ripristino della configurazione di SQL Server e dei database utente. Hello applicazione sarà necessario aggiornare toobe tooreference hello nuovo SQL Server se si accede a internamente o esternamente. È necessario toocopy tutti gli oggetti 'fuori db' come se si verificasse una migrazione Side-by-Side (SxS) SQL Server. Sono inclusi oggetti come account di accesso, certificati e server collegati.
* **Eseguire la migrazione di una macchina virtuale di Server SQL esistente**. Sarà necessario portare offline hello macchina virtuale SQL Server, quindi trasferirli tooa nuovo servizio cloud, che include la copia di tutti i relativi toohello dischi rigidi virtuali collegato, account di archiviazione Premium. Quando si hello VM viene portata online, un'applicazione hello farà riferimento hello nome host del server come prima. Tenere presente che dimensioni hello del disco esistente hello influirà sulle prestazioni di hello. Ad esempio, un disco di 400 GB Ottiene arrotondato per eccesso tooa P20. Se si sa che non richiedono che le prestazioni del disco, quindi è possibile ricreare hello macchina virtuale come macchina virtuale serie DS e collegare i dischi rigidi virtuali archiviazione Premium della specifica di dimensione/prestazioni hello desiderate. È quindi possibile scollegare e ricollegare i file di database SQL di hello.

> [!NOTE]
> Quando la copia dei dischi VHD hello è necessario essere consapevoli delle dimensioni di hello, a seconda delle dimensioni di hello implica il tipo di disco di archiviazione Premium che rientrano in, determina specifica delle prestazioni del disco. Azure arrotonderà backup toohello più vicino al disco di dimensioni, se si dispone di un disco di 400 GB, questo verrà arrotondato tooa P20. A seconda dei requisiti dei / o esistenti di hello disco rigido virtuale del sistema operativo, potrebbe non essere necessario toomigrate questo tooa account di archiviazione Premium.
>
>

Se SQL Server è accessibile dall'esterno, hello VIP di servizio cloud verrà modificato. Sarà inoltre necessario tooupdate punti di fine, gli ACL e DNS impostazioni.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Distribuzioni esistenti che usano i gruppi di disponibilità AlwaysOn
> [!NOTE]
> Per le distribuzioni esistenti, vedere prima hello [prerequisiti](#prerequisites-for-premium-storage) sezione di questo argomento.
>
>

In questa sezione si osserverà prima di tutto in che modo AlwaysOn interagisce con una rete di Azure. Si verrà quindi scomporre le migrazioni in scenari tootwo: le migrazioni in cui è necessario ottenere tempi di inattività minimi e le migrazioni in cui è possibile tollerare i tempi di inattività.

I gruppi di disponibilità di SQL Server AlwaysOn locali usano un listener locale che registra un nome DNS virtuale con un indirizzo IP condiviso tra uno o più server SQL. Quando si connettono i client vengono indirizzate tramite hello listener IP toohello primaria di SQL Server. Questo è il server hello proprietario hello risorsa sempre su IP in quel momento.

![DeploymentsUseAlways On][6]

In Microsoft Azure è possibile avere un solo IP indirizzo assegnato tooa NIC nella macchina virtuale, hello in ordine tooachieve hello stesso livello di astrazione come locale, Azure Usa indirizzo IP hello assegnato bilanciamenti del carico interno/esterno di toohello (bilanciamento del carico interno/ELB). risorsa IP Hello condivisi tra i server hello impostata toohello stesso IP come hello/ELB di bilanciamento del carico interno. Questo viene pubblicato in DNS hello e il traffico dei client verrà passato tramite replica di SQL Server primario toohello ILB/ELB hello. bilanciamento del carico interno/ELB Hello sa che SQL Server è primario, poiché Usa risorse di probe tooprobe hello sempre su IP. Nell'esempio precedente hello, analizza ogni nodo che dispone di un endpoint a cui fa riferimento hello ELB/ILB, a seconda del valore di risposta è hello primaria di SQL Server.

> [!NOTE]
> Hello ILB ELB entrambi assegnati e tooa specifico servizio cloud Azure, pertanto, qualsiasi migrazione cloud in Azure verranno probabilmente che hello che IP di bilanciamento del carico verrà modificato.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migrazione delle distribuzioni di AlwaysOn che tollerano tempi di inattività
Sono disponibili due strategie toomigrate Always On le distribuzioni che consentono di tempi di inattività:

1. **Aggiungere ulteriori tooan repliche secondarie esistenti sempre in Cluster**
2. **Eseguire la migrazione tooa nuovo sempre in Cluster**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Aggiungere ulteriori repliche secondarie tooan sempre nel Cluster esistente
Una strategia è tooadd più database secondari toohello gruppo di disponibilità AlwaysOn. È necessario tooadd in un nuovo servizio cloud e aggiornare listener hello con hello nuovo indirizzo IP del servizio di bilanciamento di carico.

##### <a name="points-of-downtime"></a>Punti dei tempi di inattività:
* Convalida del cluster.
* Test di failover AlwaysOn per nuovi database secondari.

Se si utilizza il pool di archiviazione di Windows all'interno di hello macchina virtuale per una velocità effettiva dei / o, queste verranno portate offline durante una convalida completa di Cluster. test di convalida Hello è obbligatorio quando si aggiunge nodi toohello cluster. Hello tempo test hello toorun può variare, quindi è opportuno verificare questo nel tooget ambiente di test rappresentativo un tempo approssimativo di questo tempo richiesto.

È necessario eseguire il provisioning di tempo in cui è possibile eseguire il failover manuale e chaos test hello appena aggiunto le funzioni di disponibilità elevata Always On tooensure nodi come previsto.

![DeploymentUseAlways On2][7]

> [!NOTE]
> È necessario arrestare tutte le istanze di SQL Server in cui vengono utilizzati i pool di archiviazione hello prima hello la convalida viene eseguita.
>
> ##### <a name="high-level-steps"></a>Procedure generali
>

1. Creare due nuovi server SQL Server nel nuovo servizio cloud con Archiviazione Premium collegata.
2. Copiare i backup completi e ripristinare con **NORECOVERY**.
3. Copiare gli oggetti dipendenti esterni al database utente, ad esempio nomi di accesso e così via.
4. Crea un nuovo servizio di carico bilanciamento interno (ILB) oppure utilizzare un servizio di bilanciamento del carico esterno (ELB) e quindi impostare gli endpoint con bilanciamento del carico in entrambi i nodi nuovi.

   > [!NOTE]
   > Controllare che tutti i nodi dispongono di configurazione dell'Endpoint corretto hello prima di continuare
   >
   >
5. Arrestare l'accesso utente/applicazione toohello SQL Server (se si Usa pool di archiviazione).
6. Arrestare i servizi motore di SQL Server in tutti i nodi (se si utilizzano il pool di archiviazione).
7. Aggiungere nuovi nodi toocluster ed eseguire la convalida completa.
8. Quando la convalida ha esito positivo, avviare tutti i servizi di SQL Server.
9. Eseguire il backup dei log delle transazioni e ripristinare i database utente.
10. Aggiungere nuovi nodi nel gruppo di disponibilità AlwaysOn hello e inserire la replica in **sincrono**.
11. Aggiungi IP hello risorsa indirizzo di hello nuovo Cloud servizio di bilanciamento del carico interno/ELB tramite PowerShell per Always On in base a esempio multisito hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). Nel clustering di Windows, impostare hello **proprietari possibili** di hello **indirizzo IP** toohello nuovi nodi di risorsa precedenti. Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Failover tooone di nuovi nodi hello.
13. Assicurarsi di hello nuovi nodi partner di Failover automatico e i failover di test.
14. Rimuovere i nodi originali dal gruppo di disponibilità.

##### <a name="advantages"></a>Vantaggi
* Nuovo SQL Server possono essere testati (SQL Server e dell'applicazione) prima che vengano aggiunti tooAlways in.
* È possibile cambiare dimensioni della VM hello e personalizzare i requisiti di hello archiviazione tooyour esatto. Tuttavia, sarebbe utile tookeep tutti i percorsi di file SQL hello hello stesso.
* È possibile controllare quando vengono avviati i trasferimento hello di hello DB backup toohello repliche secondarie. Questo comportamento è diverso dall'utilizzo di Azure **inizio AzureStorageBlobCopy** toocopy cmdlet dischi rigidi virtuali, in quanto si tratta di una copia asincrona.

##### <a name="disadvantages"></a>Svantaggi:
* Quando si utilizza il pool di archiviazione di Windows, si è il tempo di inattività del Cluster durante hello convalida completa del Cluster per i nuovi nodi aggiuntivi di hello.
* A seconda della versione di SQL Server di hello e numero di repliche secondarie esistenti hello, potrebbe non essere in grado di tooadd più repliche secondarie senza rimuovere i database secondari esistenti.
* Possono essere molto tempo di trasferimento di dati SQL durante l'impostazione delle repliche secondarie hello.
* Esiste un costo aggiuntivo durante la migrazione mentre le nuove macchine vengono eseguite in parallelo.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Eseguire la migrazione tooa nuovo sempre in Cluster
Un'altra strategia consiste di un nuovo sempre in Cluster con nodi nuovi toocreate nel nuovo servizio cloud e quindi reindirizzamento hello client toouse è.

##### <a name="points-of-downtime"></a>Punti dei tempi di inattività
Quando si trasferisce utenti e applicazioni toohello nuovo Always On listener, è tempo di inattività. dipende dal tempo di inattività Hello:

* Hello scattato toodatabases di backup del log delle transazioni finale toorestore nei nuovi server.
* Hello scattato tooupdate applicazioni toouse nuovo Always On listener del client.

##### <a name="advantages"></a>Vantaggi
* È possibile testare l'ambiente di produzione reale hello, SQL Server, e sistema operativo compilazione (modifiche).
* È necessario hello opzione toocustomize hello archivio e toopotentially ridurre le dimensioni della macchina virtuale. Ciò potrebbe causare determinare una riduzione dei costi.
* Durante questo processo, è possibile aggiornare il build o la versione di SQL Server. È inoltre possibile aggiornare hello del sistema operativo.
* Hello che sempre nel Cluster precedente può fungere da destinazione di rollback a tinta unita.

##### <a name="disadvantages"></a>Svantaggi:
* Nome DNS di hello toochange del listener hello è necessario se si desidera che sia sempre in cluster che eseguono contemporaneamente. Amministrazione overhead durante la migrazione di hello verrà aggiunto come le stringhe dell'applicazione client devono riflettere hello nuovo nome del Listener.
* È necessario implementare un meccanismo di sincronizzazione tra hello due ambienti tookeep come chiudere toominimize possibili i requisiti di sincronizzazione finale hello prima della migrazione.
* Esiste aggiunta costo durante la migrazione mentre il nuovo ambiente hello in esecuzione.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migrazione delle distribuzioni AlwaysOn per un tempo di inattività minimo
Sono disponibili due strategie per la migrazione delle distribuzioni di AlwaysOn per un tempo di inattività minimo:

1. **Utilizzare una replica secondaria esistente: singolo sito**
2. **Utilizzare repliche secondarie esistenti: multisito**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Usare una replica secondaria esistente: sito singolo
Una strategia per tempo di inattività minimo è un cloud esistente secondario tootake e rimuoverlo dal servizio cloud corrente hello. Copiare quindi hello toohello di dischi rigidi virtuali nuovo account di archiviazione Premium e hello macchina virtuale nel nuovo servizio cloud di hello. Aggiornare quindi il listener hello in clustering e il failover.

##### <a name="points-of-downtime"></a>Punti dei tempi di inattività
* Quando si aggiorna il nodo finale di hello con endpoint con carico bilanciato hello è tempo di inattività.
* La riconnessione del client potrebbe essere rimandata a seconda della configurazione client/DNS.
* Se si sceglie tootake hello sempre il Cluster nel gruppo non in linea tooswap gli indirizzi IP hello è tempo di inattività aggiuntiva. È possibile evitare questo problema utilizzando una dipendenza OR e proprietari possibili per hello aggiunto la risorsa indirizzo IP. Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Quando si desidera hello toopartake nodo aggiunto in come un sempre nel Partner di Failover, è necessario tooadd un Endpoint di Azure con carico bilanciato impostato un toohello di riferimento. Quando si esegue hello **Add-AzureEndpoint** comando toodo, tooremain connessioni corrente aperto, ma nuovo listener toohello di connessioni non saranno in grado di toobe stabilita solo servizio di bilanciamento del carico hello è aggiornato. Nei test questo era 90-120seconds toolast rilevato, questa deve essere testata.
>
>

##### <a name="advantages"></a>Vantaggi
* Nessun costo aggiuntivo durante la migrazione.
* Una migrazione uno a uno.
* Minore complessità.
* Consente un maggiore IOPS dalle SKU di Archiviazione Premium. Quando parti un 3rd hello dischi vengono scollegata dalla macchina virtuale hello e copiati toohello del nuovo servizio cloud, può essere tooincrease utilizzate dimensioni di disco rigido virtuale hello, che offre una maggiore produttività. Per aumentare le dimensioni del disco rigido virtuale, vedere questo [forum di discussione](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Svantaggi:
* Perdita temporanea di disponibilità elevata e ripristino di emergenza durante la migrazione.
* Poiché si tratta di una migrazione 1:1, sarà necessario toouse una dimensione minima di macchina virtuale in grado di supportare il numero di dischi rigidi virtuali, pertanto potrebbe non essere in grado di toodownsize le macchine virtuali.
* Questo scenario utilizza hello Azure **inizio AzureStorageBlobCopy** cmdlet, che è asincrono. Non esiste alcun contratto di servizio al completamento della copia. tempo di Hello di copie di hello varia, mentre questo dipende dal tempo di attesa in coda che variano inoltre quantità hello di tootransfer di dati. tempo di copia Hello aumenta se il trasferimento di hello verrà tooanother data center di Azure che supporta l'archiviazione Premium in un'altra area. Se si dispone solo di 2 nodi, prendere in considerazione una mitigazione possibili in caso di copia hello richiede più tempo durante i test. Ad esempio hello seguenti idee.
  * Aggiungere un nodo di SQL Server 3 temporaneo per la disponibilità elevata prima della migrazione hello concordata tempi di inattività.
  * Eseguire la migrazione di hello di fuori di manutenzione pianificata di Azure.
  * Assicurarsi di che avere configurato correttamente il quorum del cluster.  

##### <a name="high-level-steps"></a>Procedure generali
Questo documento viene illustrato un esempio di tooend end completa, tuttavia hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fornisce informazioni dettagliate che possono essere sfruttate tooperform questo.

![MinimalDowntime][8]

* Configurazione del disco sequenziale e Rimuovi nodo hello (non eliminare i dischi rigidi virtuali collegati).
* Creare un account di archiviazione Premium e copiare i dischi rigidi virtuali da hello account di archiviazione Standard
* Crea nuovo servizio cloud e ridistribuire hello VM SQL2 nel servizio cloud. Creare VM hello utilizzando hello copiati i file VHD originale del sistema operativo e collegamento hello dischi rigidi virtuali.
* Configurare ILB/ELB e aggiungere gli endpoint.
* Aggiornare il listener in uno dei modi seguenti:
  * Tenendo hello gruppo Always On non in linea e l'aggiornamento hello sempre sul Listener con bilanciamento del carico interno nuovo / indirizzo IP ELB.
  * O l'aggiunta di hello la risorsa indirizzo IP del nuovo Cloud servizio di bilanciamento del carico interno/ELB tramite PowerShell in Windows clustering. Quindi set hello possibili proprietari del toohello risorsa indirizzo IP di hello eseguita la migrazione di nodo, SQL2 e impostare la dipendenza OR hello nome di rete. Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Controllare i client toohello configurazione/propagazione DNS.
* Eseguire la migrazione della macchina virtuale SQL1 ed effettuare i passaggi da 2 a 4.
* Se si utilizza 5ii passaggi, quindi aggiungere SQL1 come possibile proprietario di hello aggiunto la risorsa indirizzo IP
* Testare i failover.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Usare una o più repliche secondarie esistenti: multisito
Se si dispongono di nodi in più Data Center Azure (DC) o se si dispone di un ambiente ibrido, è possibile utilizzare una configurazione di Always On in questo periodo di inattività toominimize ambiente.

approccio Hello è toochange hello Always On sincronizzazione tooSynchronous per hello in locale o controller di dominio secondario di Azure e il failover su toothat SQL Server. Quindi copiare i dischi rigidi virtuali di hello tooa account di archiviazione Premium, quindi ridistribuire macchina hello in un nuovo servizio cloud. Aggiornare listener hello e quindi eseguire il failback.

##### <a name="points-of-downtime"></a>Punti dei tempi di inattività
tempo di inattività Hello è costituito da toofailover toohello alternativa controller di dominio di hello tempo e viceversa. Dipende anche dalla configurazione del client/DNS e potrebbe determinare un ritardo della riconnessione del client.
Prendere in considerazione hello seguente esempio di una configurazione ibrida Always On:

![MultiSite1][9]

##### <a name="advantages"></a>Vantaggi
* È possibile utilizzare l'infrastruttura esistente.
* È necessario innanzitutto hello toopre-aggiornamento di hello opzione di archiviazione di Azure nel controller di dominio di ripristino di emergenza Azure hello.
* è possibile riconfigurare Hello archiviazione di ripristino di emergenza Azure controller di dominio.
* Esiste un minimo di due failover durante la migrazione, esclusi i failover di test.
* Non è necessario toomove dati di SQL Server con backup e ripristino.

##### <a name="disadvantages"></a>Svantaggi:
* A seconda di tooSQL di accesso client Server, potrebbe esserci un aumento della latenza durante l'esecuzione di SQL Server in un'applicazione di toohello controller di dominio alternativa.
* Hello copia di dischi rigidi virtuali tooPremium archiviazione potrebbe richiedere tempo. Ciò potrebbe influenzare la decisione su se tookeep hello nodo hello gruppo di disponibilità. Considerare questo aspetto quando durante la migrazione di hello eseguono carichi di lavoro a elevato utilizzo log è obbligatorio, poiché il nodo primario hello avrà tookeep hello transazioni non replicate nel log delle transazioni. aumentando così in modo significativo.
* Questo scenario utilizza hello Azure **inizio AzureStorageBlobCopy** cmdlet, che è asincrono. Non esiste alcun contratto di servizio al completamento. Hello orario di copie di hello cambia, anche se ciò dipende dal tempo di attesa in coda, verrà inoltre dipendono quantità hello di tootransfer di dati. Pertanto, è sufficiente un nodo nel centro dati 2, eseguire passaggi di attenuazione nel caso in cui la copia hello richiede più tempo durante i test. Ad esempio hello seguenti idee.
  * Aggiungere un nodo SQL 2nd temporaneo per la disponibilità elevata prima della migrazione hello concordata tempi di inattività.
  * Eseguire la migrazione di hello di fuori di manutenzione pianificata di Azure.
  * Assicurarsi di che avere configurato correttamente il quorum del cluster.

Questo scenario si presuppone di aver documentato l'installazione e conoscere la modalità di mapping di archiviazione hello modifiche toomake ordine per le impostazioni della cache del disco ottimali.

##### <a name="high-level-steps"></a>Procedure generali
![MultiSite2][10]

* Rendere hello locale / alternativo hello Azure controller di dominio primario di SQL Server e renderlo hello altri Partner di Failover automatico (AFP).
* Raccogliere informazioni di configurazione disco SQL2 e Rimuovi nodo hello (non eliminare i dischi rigidi virtuali collegati).
* Creare un account di archiviazione Premium e copiare i dischi rigidi virtuali da hello account di archiviazione Standard.
* Creare un nuovo servizio cloud e creare hello SQL2 VM con i dischi di archiviazione premi associati.
* Configurare ILB/ELB e aggiungere gli endpoint.
* Hello aggiornamento sempre sul Listener con nuovo bilanciamento del carico interno / ELB IP indirizzo e il failover.
* Controllare la configurazione DNS hello.
* Modificare hello AFP tooSQL2, eseguire la migrazione di SQL1 ed eseguire i passaggi 2-5.
* Testare i failover.
* Passare tooSQL1 indietro hello AFP e SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Appendice: La migrazione di un tooPremium sempre sul Cluster multisito archiviazione
resto Hello di questo argomento fornisce un esempio dettagliato di conversione di un archivio per multisito AlwaysOn cluster tooPremium. Converte inoltre hello Listener dall'utilizzo di bilanciamento del carico interno un carico esterno (ELB) del servizio di bilanciamento tooan (ILB).

### <a name="environment"></a>Environment
* Windows 2K12 /SQL 2K12
* 1 File DB su SP
* 2 pool di archiviazione per ogni nodo

![Appendix1][11]

### <a name="vm"></a>VM:
In questo esempio verrà toodemonstrate lo spostamento da un tooILB ELB. Viene illustrato come toothis tooswitch durante hello migrazione ELB era disponibile prima di bilanciamento del carico interno.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>I passaggi precedenti: Connettersi tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Passaggio 1: Creare un nuovo account di archiviazione e servizio cloud
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Passaggio 2: Hello aumento consentito errori sulle risorse<Optional>
In alcune risorse appartenenti al gruppo di disponibilità AlwaysOn tooyour esistono limiti il numero di errori che può verificarsi in un periodo, in cui il servizio cluster hello tenterà gruppo di risorse toorestart hello. È consigliabile che aumentare questo al contempo scorrere tramite questa procedura, poiché in caso contrario manualmente failover failover e trigger arrestando macchine si può ottenere il limite di toothis Chiudi.

Potrebbe essere consentito di errore hello prudente toodouble, toodo in Gestione Cluster di Failover, vedere toohello proprietà hello sempre nel gruppo di risorse:

![Appendix3][13]

Modificare hello too6 numero massimo di errori.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Passaggio 3: Aggiungere la risorsa indirizzo IP per il gruppo di cluster <Optional>
Se si dispone di un solo indirizzo IP per il gruppo di Cluster hello e la subnet cloud toohello allineato, tenere presente, se si accidentalmente portare offline tutti i nodi del cluster nel cloud hello che rete quindi risorsa indirizzo IP del Cluster hello e nome di rete Cluster non saranno in grado di toocome in linea. In hello evento di questo che eviterà Aggiorna tooother risorse del cluster.

#### <a name="step-4-dns-configuration"></a>Passaggio 4: Eseguire la configurazione di DNS
tooimplement una transizione uniforme dipende dalla modalità DNS viene usato e aggiornato.
Quando viene installato Always On, viene creato un gruppo di risorse Cluster di Windows, se si apre Gestione Cluster di Failover, si noterà che almeno avrà tre risorse, hello due che hello documento fa riferimento tooare:

* Nome di rete virtuale (VNN) – si tratta hello DNS nome client connettersi toowhen che desiderano tooconnect tooSQL server tramite Always On.
* Risorsa indirizzo IP: si tratta di indirizzi IP associato alla hello VNN hello, è possibile avere più e sarà necessario un indirizzo IP per ogni sito e subnet in una configurazione multisito.

Quando si recupera i record DNS hello associato listener hello, provare tooconnect tooeach tooSQL connessione Server, il driver di SQL Server Client hello Always On associato l'indirizzo IP, seguito prende in esame alcuni fattori che possono influenzare questo.

Hello numero di record DNS simultanee associati con il nome del listener hello dipende non solo il numero di hello di indirizzi IP associati, ma hello ' RegisterAllIpProviders'setting nel Clustering di Failover per la risorsa nome di rete virtuale ON sempre hello.

Quando si distribuisce Always On in Azure sono disponibili diversi passaggi toocreate hello Listener e gli indirizzi IP, si dispone di toomanually configurare too1 'RegisterAllIpProviders' hello, si tratta di diversi tooan distribuzione sempre in locale in cui è già impostato too1.

Se 'RegisterAllIpProviders' è 0, viene visualizzata solo un record DNS nel DNS associato hello Listener:

![Appendix4][14]

Se 'RegisterAllIpProviders' è 1:

![Appendix5][15]

codice Hello riportato di seguito verrà eseguire il dump di hello le impostazioni di nome di rete virtuale e impostarlo per l'utente, si noti che per hello tootake effetto occorrerà tootake hello VNN offline e attivare di nuovo online, questa acquisire hello offline che causa interruzioni di connettività client Listener.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

In un passaggio successivo di migrazione sarà necessario tooupdate hello Always On listener con un indirizzo IP aggiornato che fa riferimento un servizio di bilanciamento del carico, questo comporta un rimozione della risorsa indirizzo IP e l'aggiunta. Dopo l'aggiornamento IP hello, è necessario tooensure hello nuovo indirizzo IP è stato aggiornato nella zona DNS e che i client hello Aggiorna cache DNS locale.

Se i client si trovano in un segmento di rete diversa e fanno riferimento a un altro server DNS, è necessario tooconsider conseguenze sui trasferimenti di zona DNS durante la migrazione di hello, hello applicazione si riconnettono ora sarà vincolato dal hello almeno il tempo di trasferimento zona di eventuali nuovi indirizzi IP per il listener hello. Se si è nel vincolo di tempo in questo caso, è consigliabile discutere e testare l'utilizzo forzato di un trasferimento di zona incrementale con i team di Windows, e anche inserire hello DNS tooa record host tooLive TTL (Time), ridurre in modo da aggiornano i client hello. Per ulteriori informazioni, vedere [Trasferimenti di zona incrementali](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Impostazione hello predefinito durata (TTL) per i Record DNS associato hello Listener Always On in Azure è 1200 secondi. È possibile tooreduce in questo caso nel vincolo di tempo durante l'aggiornamento client di migrazione tooensure hello relativi nomi con IP hello aggiornato l'indirizzo per il listener hello. È possibile visualizzare e modificare la configurazione di hello eseguendo il dump out configurazione hello di hello VNN:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Si noti, hello inferiore hello 'HostRecordTTL', si verificherà una maggiore quantità di traffico DNS.

##### <a name="client-application-settings"></a>Impostazioni applicazione client
Se supportate dall'applicazione client SQL hello .net 4.5 SQLClient, sarà possibile usare ' MULTISUBNETFAILOVER = TRUE' (parola chiave), questa opzione è consigliata toobe applicato, che consente di tooSQL connessione più veloce gruppo di disponibilità AlwaysOn durante il failover. Enumera tutti gli indirizzi IP associati hello Always On listener in parallelo ed esegue una velocità di tentativi di connessione TCP più aggressiva durante un failover.

Per ulteriori informazioni sulla hello impostazioni indicate sopra, vedere [parola chiave MultiSubnetFailover e funzionalità associate](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Vedere anche [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Passaggio 5: Impostare il quorum del cluster
Come si intende toobe richiede almeno un server SQL verso il basso alla volta, è necessario modificare impostazione del quorum del cluster hello, con 2 nodi di controllo di condivisione File (FSW), è necessario impostare maggioranza dei nodi di hello quorum tooallow e utilizzare il voto dinamico, se si tratta di tooallow per condizione tooremain un singolo nodo.

    Set-ClusterQuorum -NodeMajority  

Per ulteriori informazioni sulla gestione e la configurazione quorum del cluster hello, vedere [configurare e gestire il Quorum in un Cluster di Failover di Windows Server 2012 di hello](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Passaggio 6: Estrarre endpoint e ACL esistenti
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Salvare questi file di testo tooa.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Passaggio 7: Modificare i partner di failover e le modalità di replica
Se si dispone di più di 2 istanze di SQL Server, è necessario impostare failover hello di un'altra replica secondaria in un altro controller di dominio o 'too'Synchronous on-premise e renderlo un Partner di Failover automatico (AFP), in modo da mantenere a disponibilità elevata, mentre si apportano modifiche. A tale scopo, è possibile utilizzare TSQL o SSMS:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Passaggio 8: Rimuovere la VM secondaria dal servizio cloud
Si consiglia di pianificare toomigrate un nodo secondario del cloud in primo luogo, se si tratta attualmente primario, si deve avviare un failover manuale.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Passaggio 9: Modificare le impostazioni di caching del disco nel file CSV e salvare
Per i volumi di dati questi deve essere impostati tooREADONLY.

Per i volumi TLOG questi deve essere impostati tooNONE.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Passaggio 10: Copiare i dischi rigidi virtuali
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



È possibile controllare lo stato di copia hello di hello dischi rigidi virtuali toohello account di archiviazione Premium:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Attendere che tutto venga registrato come esito positivo.

Per informazioni per i singoli BLOB:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Passaggio 11: Registrare un disco del sistema operativo
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Passaggio 12: Importare la replica secondaria nel nuovo servizio cloud
codice Hello seguito anche aggiunto di hello utilizza opzione qui è possibile importare la macchina hello e utilizzare hello retainable VIP.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Passaggio 13: Creare il servizio ILB sul nuovo Svc cloud, aggiungere endpoint a carico bilanciato e ACL
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Passaggio 14: Aggiornare AlwaysOn
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Rimuovere il servizio di cloud precedente hello indirizzo IP.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Passaggio 15: Eseguire il controllo dell'aggiornamento DNS
È ora necessario controllare i server DNS di una rete di client di SQL Server e assicurarsi che il servizio cluster sia aggiunto hello record host aggiuntivi per hello aggiunta indirizzo IP. Se i server DNS non sono aggiornate, è possibile forzare un trasferimento di zona DNS e verificare che i client nella subnet sono hello sono in grado di tooresolve tooboth sempre su indirizzi IP, in tal caso non è necessario toowait per la replica automatica DNS.

#### <a name="step-16-reconfigure-always-on"></a>Passaggio 16: Riconfigurare Always On
A questo punto è attendere hello secondario tale nodo che è stato migrato toofully risincronizzare con nodo locale hello e passa il nodo di replica toosynchronous e renderlo AFP hello.  

#### <a name="step-17-migrate-second-node"></a>Passaggio 17: Eseguire la migrazione del secondo nodo
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Passaggio 18: Modificare le impostazioni di caching del disco nel file CSV e salvare
Per i volumi di dati questi deve essere impostati tooREADONLY.

Per i volumi TLOG questi deve essere impostati tooNONE.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Passaggio 19: Creare nuovi account di archiviazione indipendente per il nodo secondario
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Passaggio 20: Copiare i dischi rigidi virtuali
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


È possibile controllare lo stato di copia di hello disco rigido virtuale per tutti i dischi rigidi virtuali: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. EtichettaDisco $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Attendere che tutto venga registrato come esito positivo.

Per informazioni per i singoli BLOB:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Passaggio 21: Registrare il disco del sistema operativo
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Passaggio 22: Aggiungere endpoint con carico bilanciato e ACL
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Passaggio 23: Eseguire il failover di test
A questo punto, è consigliabile consentire nodo migrati hello sincronizzare con hello on-premise sempre nel nodo, posizionare il report in modalità di replica toosynchronous e attendere fino a quando viene sincronizzata. Quindi il failover da locale toohello primo nodo migrato, ovvero AFP hello. Una volta che ha funzionato, hello modifica ultima migrazione AFP toohello nodo.

È consigliabile i failover tra tutti i nodi di test ed eseguire se test chaos failover tooensure funziona come previsto e in un tempo indicato.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Passaggio 24: Ripristinare le impostazioni quorum del cluster / TTL DNS / Failover Pntrs / impostazioni di sincronizzazione
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Aggiunta della risorsa indirizzo IP nella stessa Subnet
Se si dispone solo 2 istanze di SQL Server e che si desidera toomigrate li tooa nuovo servizio cloud, ma si desidera tookeep su hello stessa subnet, è possibile evitare di creare listener hello originale di hello toodelete offline sempre l'indirizzo IP e aggiungere hello nuovo indirizzo IP. Se si esegue la migrazione di subnet di tooanother hello macchine virtuali non è necessario toodo questo come sarà presente una rete di cluster aggiuntivo che farà riferimento a subnet.

Dopo aver spostato hello eseguita la migrazione di database secondario e aggiunto nella nuova risorsa indirizzo IP hello per nuovo servizio cloud di hello prima failover hello primario esistente, è necessario eseguire la procedura all'interno di hello gestione Cluster di Failover:

tooadd nell'indirizzo IP, vedere hello [appendice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), passaggio 14.

1. Per la risorsa indirizzo IP corrente di hello, modificare hello possibile proprietario too'Existing Server SQL primario ', nell'esempio riportato di seguito, 'dansqlams4' hello:

    ![Appendix13][23]
2. Per la nuova risorsa indirizzo IP di hello, modificare hello possibile proprietario too'Migrated secondaria SQL Server ", nell'esempio riportato di seguito, 'dansqlams5' hello:

    ![Appendix14][24]
3. Dopo aver impostato questo è possibile eseguire il failover, e quando viene eseguita la migrazione dell'ultimo nodo hello hello possibili proprietari possono essere modificati in modo tale nodo viene aggiunto come possibile proprietario:

    ![Appendix15][25]

## <a name="additional-resources"></a>Risorse aggiuntive
* [Archiviazione Premium di Azure](../../../storage/common/storage-premium-storage.md)
* [Macchine virtuali](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
