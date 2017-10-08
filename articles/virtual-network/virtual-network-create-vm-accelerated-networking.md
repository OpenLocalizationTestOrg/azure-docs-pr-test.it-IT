---
title: una macchina virtuale di Azure con accelerazione di rete aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una macchina virtuale con accelerazione di rete.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Creare una macchina virtuale con rete accelerata

In questa esercitazione, è illustrato come toocreate una macchina virtuale di Azure (VM) con accelerazione di rete. La funzionalità di rete accelerata è disponibile a livello generale per Windows e in anteprima pubblica per distribuzioni Linux specifiche. Rete accelerata consente single root i/o virtualization (SR-IOV) tooa VM, migliorando le prestazioni di rete. Questo percorso ad alte prestazioni Ignora host hello dal relativo al percorso dati hello riducendo la latenza e instabilità utilizzo della CPU, per l'utilizzo con hello più esigenti rete carichi di lavoro supportati tipi di macchine Virtuali. Hello seguente immagine Mostra comunicazione tra due macchine virtuali (VM) con e senza la configurazione di rete:

![Confronto](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Senza la configurazione di rete, tutto il traffico di rete da e verso hello VM deve attraversare host hello e commutatore virtuale hello. commutatore virtuale Hello fornisce tutti i criteri, ad esempio come gruppi di sicurezza di rete accedere gli elenchi di controllo, l'isolamento e altro traffico di rete virtualizzata servizi toonetwork. informazioni sui commutatori virtuali, leggere hello toolearn [virtualizzazione rete Hyper-V e il commutatore virtuale](https://technet.microsoft.com/library/jj945275.aspx) articolo.

Con la rete con accelerata, traffico di rete arriva all'interfaccia di rete della macchina virtuale di hello (NIC) e verrà quindi inoltrato toohello macchina virtuale. Tutti i criteri di rete che hello commutatore virtuale applicata senza rete accelerata vengono scaricate e applicate nell'hardware. L'applicazione dei criteri in hardware Abilita hello NIC tooforward traffico di rete direttamente toohello macchina virtuale, ignorando host hello e lo switch virtuale hello, mantenendo tutti i criteri di hello in host hello è applicata.

Hello vantaggi delle reti con accelerazione si applicano solo toohello è abilitato nella macchina virtuale. Per ottenere risultati ottimali hello è ideale tooenable questa funzionalità in almeno due macchine virtuali connesse toohello stessa rete virtuale di Azure (VNet). Durante la comunicazione tra reti virtuali o la connessione locale, questa funzionalità presenta una latenza toooverall un impatto minimo.

> [!WARNING]
> Questo Linux anteprima pubblica potrebbe non disporre hello dello stesso livello di disponibilità e affidabilità come le funzioni che sono in genere versione disponibilità. Hello funzionalità non è supportato, può avere vincolato funzionalità e potrebbero non essere disponibili in tutte le posizioni di Azure. Per più le notifiche di hello su disponibilità e lo stato di questa funzionalità, controllo pagina degli aggiornamenti di hello rete virtuale di Azure.

## <a name="benefits"></a>Vantaggi
* **Latenza più bassa / superiore pacchetti al secondo (pps):** rimozione hello il commutatore virtuale dal relativo al percorso dati hello rimuove hello tempo pacchetti nell'host di hello per l'elaborazione di criteri e aumenta hello numero di pacchetti che possono essere elaborati all'interno di hello macchina virtuale.
* **Ridotto instabilità:** commutatore virtuale elaborazione dipende dalla quantità hello di criteri che deve toobe applicato e hello del carico di lavoro di hello CPU che esegue l'elaborazione di hello. Offload hardware toohello imposizione dei criteri di hello rimuove tale variabilità offrendo pacchetti direttamente attiva toohello VM, rimuovendo la comunicazione tra tooVM di hello host e tutti i software interrupt e contesto.
* **Ridurre l'utilizzo della CPU:** esclusione hello il commutatore virtuale nell'host di hello comporta l'utilizzo della CPU tooless per elaborare il traffico di rete.

## <a name="Limitations"></a>Limitazioni
Hello limitazioni seguenti esiste quando si utilizza questa funzionalità:

* **Creazione di un'interfaccia di rete**: la funzionalità rete accelerata può essere abilitata solo per una nuova scheda di interfaccia di rete. Non può essere abilitata per una scheda di interfaccia di rete esistente.
* **Creazione della macchina virtuale:** una scheda NIC con la rete accelerata abilitata possono solo essere collegato tooa VM quando hello viene creata la VM. Hello NIC non può essere collegato tooan macchina virtuale esistente.
* **Aree**: le VM Windows con rete accelerata sono disponibili nella maggior parte delle aree di Azure. Le VM Linux con rete accelerata sono disponibili in più aree. Questa funzionalità è disponibile nelle aree di Hello all'espansione. Vedere blog di Azure Aggiorna rete virtuale hello sotto per informazioni più recenti di hello.   
* **Sistemi operativi supportati**: Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016. Linux: Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superiore, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (pubblicato da "Rogue Wave Software").
* **Dimensione della VM**: dimensioni di istanza per scopo generico e con ottimizzazione per il calcolo con otto o più memorie centrali. Per ulteriori informazioni, vedere hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale. set di dimensioni di istanza di macchina virtuale supportate Hello verranno espanse in hello future.
* **Solo distribuzione tramite Azure Resource Manager (ARM):** la rete accelerata non è disponibile per la distribuzione tramite ASM/RDFE.

Limitazioni di toothese le modifiche vengono annunciate tramite hello [le funzionalità di rete virtuale di Azure Aggiorna](https://azure.microsoft.com/updates/accelerated-networking-in-preview) pagina.

## <a name="create-a-windows-vm"></a>Creare un'app Windows
È possibile utilizzare hello portale di Azure o Azure [PowerShell](#windows-powershell) toocreate hello macchina virtuale.

### <a name="windows-portal"></a>Portale

1. Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Nel portale di hello, fare clic su **+ nuovo** > **calcolo** > **Data Center di Windows Server 2016**. 
3. In hello **Data Center di Windows Server 2016** pannello viene visualizzato, lasciare *Gestione risorse* selezionato in **selezionare un modello di distribuzione**, fare clic su **crea** .
4. In hello **nozioni di base** blade che viene visualizzata, immettere i seguenti valori hello, lasciare hello rimanenti opzioni predefinite o selezionare o immettere valori personalizzati, quindi scegliere hello **OK** pulsante:

    |Impostazione|Valore|
    |---|---|
    |Nome|MyVm|
    |Gruppo di risorse|Lasciare selezionata l'opzione **Crea nuovo** e immettere *MyResourceGroup*|
    |Località|Stati Uniti occidentali 2|

    Se si tooAzure nuovo, altre informazioni, vedere [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [percorsi](https://azure.microsoft.com/regions) (che sono anche definiti tooas aree).
5. In hello **scegliere una dimensione** blade che viene visualizzata, immettere *8* in hello **numero minimo di core** casella, quindi fare clic su **visualizzare tutti**.
6. Fare clic su **DS4_V2 Standard**, o qualsiasi macchina virtuale è supportato, quindi fare clic su hello **selezionare** pulsante.
7. In hello **impostazioni** pannello visualizzato, lasciare tutte le impostazioni come-è, ad eccezione di fare clic su **abilitato** in **Accelerated rete**, quindi fare clic su hello **OK** pulsante. **Nota:** se, nei passaggi precedenti, si selezionano i valori per dimensioni, il sistema operativo o percorso macchina virtuale che non sono elencati in hello [limitazioni](#Limitations) sezione di questo articolo, **Accelerated rete**non è visibile.
8. In hello **riepilogo** pannello visualizzato, fare clic su hello **OK** pulsante. Azure avvia hello VM di creazione. La creazione della VM richiede alcuni minuti.
9. hello tooinstall accelerated driver di rete per Windows, hello completato i passaggi in hello [configurare Windows](#configure-windows) sezione di questo articolo.

### <a name="windows-powershell"></a>PowerShell
1. Installare hello la versione più recente di Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, leggere hello [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.
2. Avviare una sessione di PowerShell facendo clic sul pulsante Start di Windows hello, digitando **powershell**, quindi fare clic su **PowerShell** dai risultati della ricerca hello.
3. Nella finestra di PowerShell, immettere hello `login-azurermaccount` toosign comando con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Nel browser, copiare lo script seguente hello:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. Nella finestra di PowerShell, fare doppio clic su script hello toopaste e avviare l'esecuzione. Vengono richiesti un nome utente e una password. Utilizzare queste toolog credenziali in toohello VM quando ci si connette tooit nel passaggio successivo hello. Se si verifica un errore di script hello e modificate nello script hello valori prima dell'esecuzione, verificare i valori hello è utilizzato per le dimensioni di macchina virtuale, il sistema operativo, e posizione sono elencate nella hello [limitazioni](#Limitations) sezione di questo articolo.
6. hello tooinstall accelerated driver di rete per Windows, hello completato i passaggi in hello [configurare Windows](#configure-windows) sezione di questo articolo.

### <a name="configure-windows"></a>Configurare Windows
Dopo aver creato hello VM in Azure, è necessario installare i driver di rete con accelerazione hello per Windows. Prima di completare hello alla procedura seguente, è necessario avere creato una macchina virtuale Windows con la rete accelerata utilizzando entrambi hello [portale](#windows-portal) o [PowerShell](#windows-powershell) i passaggi in questo articolo. 

1. Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *MyVm*. Quando **MyVm** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **MyVm** pannello visualizzato, fare clic su hello **Connetti** pulsante hello alto a sinistra del pannello hello. **Nota:** se **creazione** è visibile in hello **Connetti** pulsante, Azure non è ancora terminata hello VM di creazione. Fare clic su **Connetti** solo dopo che non si visualizzano più **creazione** in hello **Connetti** pulsante.
4. Consenti il hello toodownload browser **MyVm.rdp** file.  Una volta scaricato, fare clic su tooopen file hello è. 
5. Fare clic su hello **Connetti** pulsante hello **connessione Desktop remoto** visualizzata, viene indicato che hello non è possibile identificare l'autore della connessione remota hello.
6. In hello **la sicurezza di Windows** casella viene visualizzata, fare clic su **altre scelte**, quindi fare clic su **utilizzare un account diverso**. Immettere nome utente hello e la password immessa nel passaggio 4, quindi fare clic su hello **OK** pulsante.
7. Fare clic su hello **Sì** pulsante nella finestra di connessione Desktop remoto hello visualizzata, viene indicato che è Impossibile verificare l'identità di hello del computer remoto hello.
8. Fare doppio clic su pulsante Start di Windows hello e fare clic su **Gestione dispositivi**. Espandere hello **schede di rete** nodo. Verificare che hello **scheda Ethernet di funzione virtuale Mellanox ConnectX-3** viene visualizzato, come illustrato nella seguente immagine hello:
   
    ![Gestione dispositivi](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. La funzionalità di rete accelerata è ora abilitata per la VM.

## <a name="create-a-linux-vm"></a>Creare una macchina virtuale Linux
È possibile utilizzare hello portale di Azure o Azure [PowerShell](#linux-powershell) toocreate un Ubuntu o SLES VM. Per le VM RHEL e CentOS, il flusso di lavoro è diverso.  Vedere le istruzioni di hello seguenti.

### <a name="linux-portal"></a>Portale
1. Registrazione per l'accelerazione di rete per l'anteprima di Linux, completare i passaggi da 1 a 5 di hello hello [creare una VM Linux - PowerShell](#linux-powershell) sezione di questo articolo.  È possibile registrare per l'anteprima di hello nel portale di hello.
2. Completare i passaggi 1-8 in hello [creare una macchina virtuale Windows - portale](#windows-portal) sezione di questo articolo. Nel passaggio 2 fare clic su **Ubuntu Server 16.04 LTS** anziché su **Windows Server 2016 Datacenter**. Per questa esercitazione, scegliere toouse una password, anziché una chiave SSH, anche se per le distribuzioni di produzione, è possibile utilizzare. Se **Accelerated rete** non viene visualizzato al termine di passaggio 7 di hello [creare una macchina virtuale Windows - portale](#windows-portal) sezione di questo articolo, è probabile che per uno dei seguenti motivi hello:
    - Per l'anteprima di hello non ancora registrato. Verificare che lo stato di registrazione sia **registrati**, come illustrato nel passaggio 4 di hello [creare una VM Linux - Powershell](#linux-powershell) sezione di questo articolo. **Nota:** se si è partecipato alla hello Accelerated di rete per l'anteprima di macchine virtuali di Windows (il non toouse tooregister necessario più tempo accelerazione di rete per le macchine virtuali di Windows), non vengono registrate automaticamente per hello Accelerated rete per Visualizzare in anteprima le macchine virtuali Linux. È necessario registrare hello Accelerated di rete per le macchine virtuali Linux anteprima tooparticipate in essa contenuti.
    - Non è stata selezionata una dimensione, del sistema operativo o percorso indicato nella hello VM [limitazioni](#limitations) sezione di questo articolo.
3. hello tooinstall accelerated driver di rete per Linux, hello completato i passaggi in hello [configurare Linux](#configure-linux) sezione di questo articolo.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Se si creare macchine virtuali Linux con la rete in una sottoscrizione e quindi tenta una macchina virtuale Windows con la rete accelerata in hello toocreate stessa sottoscrizione, creazione della macchina virtuale di Windows hello potrebbe non riuscire. Durante questa anteprima è consigliabile testare le VM Windows e Linux con rete accelerata in sottoscrizioni distinte.
>

1. Installare hello la versione più recente di Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, leggere hello [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.
2. Avviare una sessione di PowerShell facendo clic sul pulsante Start di Windows hello, digitando **powershell**, quindi fare clic su **PowerShell** dai risultati della ricerca hello.
3. Nella finestra di PowerShell, immettere hello `login-azurermaccount` toosign comando con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Registrazione per l'accelerazione di rete per Azure hello anteprima completando hello alla procedura seguente:
    - Inviare un messaggio di posta elettronica troppo[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con l'ID sottoscrizione di Azure e l'utilizzo previsto. Attendere la conferma tramite posta elettronica dell'abilitazione della sottoscrizione da parte di Microsoft.
    - Immettere hello tooconfirm comando che sono registrati per l'anteprima di hello seguenti:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Non proseguire con il passaggio 5 fino a **registrati** viene visualizzato nell'output dopo l'immissione hello precedente comando hello. L'output deve essere simile seguente hello output prima di continuare:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Se si è partecipato alla hello Accelerated di rete per l'anteprima di macchine virtuali di Windows (il non toouse tooregister necessario più tempo accelerazione di rete per le macchine virtuali di Windows), non vengono registrate automaticamente per hello Accelerated di rete per l'anteprima di macchine virtuali Linux. È necessario registrare hello Accelerated di rete per le macchine virtuali Linux anteprima tooparticipate in essa contenuti.
      >
5. Nel browser, copiare lo script sostituendo Ubuntu o SLES desiderato seguente hello.  Anche in questo caso, Redhat e CentOS prevedono un flusso di lavoro diverso, illustrato di seguito.

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. Nella finestra di PowerShell, fare doppio clic su script hello toopaste e avviare l'esecuzione. Vengono richiesti un nome utente e una password. Utilizzare queste toolog credenziali in toohello VM quando ci si connette tooit nel passaggio successivo hello. Se hello script non riesce, verificare quanto segue:
    - Sono registrati per l'anteprima di hello, come illustrato nel passaggio 4
    - Se si modificati dimensioni, tipo di sistema operativo o i valori di posizione nello script hello VM prima dell'esecuzione, sono elencati i valori hello in hello [limitazioni](#Limitations) sezione di questo articolo.
7. hello tooinstall accelerated driver di rete per Linux, hello completato i passaggi in hello [configurare Linux](#configure-linux) sezione di questo articolo.

### <a name="configure-linux"></a>Configurare Linux

Dopo aver creato hello VM in Azure, è necessario installare i driver di rete con accelerazione hello per Linux. Prima di completare hello alla procedura seguente, è necessario avere creato una VM Linux con la rete accelerata utilizzando entrambi hello [portale](#linux-portal) o [PowerShell](#linux-powershell) i passaggi in questo articolo. 

1. Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Nella parte superiore di hello del diritto toohello portale, di hello di hello *individuare risorse* barra, fare clic su hello **> _** toostart icona una shell di cloud Bash (anteprima). Hello Bash cloud shell riquadro viene visualizzato nella parte inferiore di hello del portale hello e dopo alcuni secondi, presenta un  **username@Azure:~ $** prompt dei comandi. Se è possibile SSH toohello macchina virtuale del computer, piuttosto che shell cloud hello, istruzioni di hello in questa esercitazione si presuppone che shell cloud hello in uso.
3. Nella parte superiore di hello del portale hello, nella casella hello contenente testo hello *individuare risorse*, tipo *MyVm*. Quando **MyVm** viene visualizzato nei risultati della ricerca hello, selezionarlo.
4. In hello **MyVm** pannello visualizzato, fare clic su hello **Connetti** pulsante hello alto a sinistra del pannello hello. **Nota:** se **creazione** è visibile in hello **Connetti** pulsante, Azure non è ancora terminata hello VM di creazione. Fare clic su **Connetti** solo dopo che non si visualizzano più **creazione** in hello **Connetti** pulsante.
5. Azure consente di aprire una finestra informa hello tooenter `ssh adminuser@<ipaddress>`. Immettere questo comando hello cloud shell (o copia dalla casella hello che venivano visualizzate nel passaggio 4 e incollarlo nella shell di cloud toohello), quindi premere INVIO.
6. Invio **Sì** toohello desiderano se si desidera che la connessione toocontinue, quindi premere INVIO.
7. Immettere la password di hello che immessi durante la creazione di hello macchina virtuale. Dopo aver connesso toohello macchina virtuale, viene visualizzato un adminuser@MyVm:~ prompt$. Si è connessi a questo punto toohello VM tramite una sessione della shell hello cloud. **Nota**: le sessioni cloud shell vanno in timeout dopo 10 minuti di inattività.

A questo punto, le istruzioni di hello variano in base distribuzione hello in uso. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Al prompt dei comandi hello, immettere `uname -r` e verificare la versione di hello per:

    * Per Ubuntu, "4.4.0-77-generic" o versione superiore
    * Per SLES, "4.4.59-92.20-default" o versione superiore

2. Creare un legame tra vNIC di rete standard hello e vNIC rete hello accelerata dall'esecuzione di comandi hello che seguono. Il traffico di rete utilizza hello migliori prestazioni con accelerata rete scheda di rete virtuale, mentre obbligazione hello assicura che il traffico di rete non venga interrotta tra alcune modifiche di configurazione.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Dopo l'esecuzione dello script, hello hello VM verrà riavviato dopo un secondo 60 sospendere.
4. Una volta hello VM viene riavviata, riconnettersi tooit completando i passaggi da 5 a 7 nuovamente.
5. Eseguire hello `ifconfig` comando e verificare che è risultata bond0 interfaccia hello è visualizzato come backup. 
 
 >[!NOTE]
      >Le applicazioni con una rete con accelerata devono comunicare su hello *bond0* interfaccia, non *eth0*.  può modificare il nome di interfaccia Hello prima accelerata rete raggiunge disponibilità generale.

#### <a name="rhelcentos"></a>RHEL/CentOS

Creazione di una macchina virtuale 7.3 CentOS Red Hat Enterprise Linux richiede alcuni ulteriori passaggi tooload hello più recente i driver necessari per SR-IOV e hello driver VF (Virtual Function) della scheda di rete hello. Hello prima fase di istruzioni hello prepara un'immagine che può essere utilizzato toomake uno o più macchine virtuali che includono driver hello precaricati.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Fase 1: Preparare un'immagine di base Red Hat Enterprise Linux o CentOS 7.3 

1.  Effettuare il provisioning di una VM CentOS 7.3 non SR-IOV in Azure

2.  Installare LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Scaricare i file di configurazione
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Effettuare il deprovisioning della VM

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Dal portale di Azure, arrestare la macchina virtuale; e passare i "dischi del tooVM", URI VHD dell'hello OSDisk acquisizione. Questo URI contiene hello base nome dell'immagine disco rigido virtuale e il relativo account di archiviazione. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Fase 2: Effettuare il provisioning delle nuove VM in Azure

1.  Eseguire il provisioning di nuove macchine virtuali in base con New-AzureRMVMConfig utilizzando hello base immagine VHD acquisito in fase di uno, con AcceleratedNetworking abilitata nella scheda di rete virtuale hello:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Dopo l'avviano di macchine virtuali, controllare il dispositivo di VF hello da "lspci" e verificare voce Mellanox hello. Ad esempio, questo elemento di output di hello lspci dovremmo vedere:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Eseguire script partnership hello da:

    ```bash
    sudo bondvf.sh
    ```

4.  Riavviare il computer hello nuove macchine virtuali:

    ```bash
    sudo reboot
    ```

Hello VM deve iniziare con bond0 configurato e hello percorso Accelerated rete abilitato.  Eseguire `ifconfig` tooconfirm.
