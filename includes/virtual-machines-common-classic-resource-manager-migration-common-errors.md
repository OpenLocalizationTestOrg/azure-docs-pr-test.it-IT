# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Errori comuni durante la classica tooAzure migrazione di gestione risorse
I cataloghi di questo articolo hello errori e le misure di attenuazione più comuni durante la migrazione di hello delle risorse IaaS dallo stack Azure Resource Manager toohello modello di distribuzione classico di Azure.

## <a name="list-of-errors"></a>Elenco degli errori
| Stringa di errore | Mitigazione |
| --- | --- |
| Errore interno del server |In alcuni casi, si tratta di un errore temporaneo che si risolve con un nuovo tentativo. Se continua, toopersist [contattare il supporto tecnico di Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) poiché necessita di analisi dei log di piattaforma. <br><br> **Nota:** dopo l'evento imprevisto di hello verrà rilevato dal team di supporto hello, non tentare qualsiasi mitigazione automatica come ciò potrebbe avere conseguenze impreviste nell'ambiente. |
| La migrazione non è supportata per la distribuzione {nome-distribuzione} in HostedService {nome-servizio-ospitato} perché si tratta di una distribuzione PaaS (Web/di lavoro). |Ciò si verifica quando una distribuzione contiene un ruolo Web o di lavoro. Poiché la migrazione è supportata solo per le macchine virtuali, rimuovere ruoli web/di lavoro hello dalla distribuzione hello e ripetere la migrazione. |
| Distribuzione del modello {nome modello} non riuscita. CorrelationId={guid} |In hello back-end del servizio di migrazione, si usa risorse di Azure Resource Manager modelli toocreate nello stack di hello Azure Resource Manager. In genere perché i modelli sono idempotente, è possibile ritentare in modo sicuro hello migrazione operazione tooget dopo questo errore. Se questo errore si ripresenta toopersist, [contattare il supporto tecnico di Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) e fornire loro hello CorrelationId. <br><br> **Nota:** dopo l'evento imprevisto di hello verrà rilevato dal team di supporto hello, non tentare qualsiasi mitigazione automatica come ciò potrebbe avere conseguenze impreviste nell'ambiente. |
| rete virtuale Hello {virtual-network-name} non esiste. |Questa situazione può verificarsi se è stato creato hello rete virtuale nel nuovo portale di Azure hello. nome di rete virtuale effettivo Hello segue il modello di hello "gruppo * <VNET name>" |
| La VM {nome-vm} in HostedService {nome-servizio-ospitato} contiene l'estensione {nome-estensione} non supportata in Azure Resource Manager. È consigliabile toouninstall dalla hello VM prima di continuare con la migrazione. |Le estensioni XML, ad esempio BGInfo 1.*, non sono supportate in Azure Resource Manager. Queste estensioni non possono essere migrate. Se queste estensioni sono macchina virtuale hello installato su a sinistra, vengono disinstallate automaticamente prima del completamento della migrazione hello. |
| La macchina virtuale {nome-vm} nel servizio ospitato {nome-servizio-ospitato} contiene l'estensione VMSnapshot/VMSnapshotLinux che non è attualmente supportata per la migrazione. Disinstallarla dalla macchina virtuale hello e riaggiungerlo tramite Gestione risorse di Azure al termine della migrazione hello |Si tratta di uno scenario di hello in macchina virtuale hello è configurato per il Backup di Azure. Poiché questo scenario non è attualmente non supportato, attenersi alla soluzione hello in https://aka.ms/vmbackupmigration |
| VM {vm-name} nel servizio ospitato {ospitato-service-name} contiene estensione {estensione-name} con stato non viene segnalato da hello macchina virtuale. Di conseguenza, non è possibile eseguire la migrazione di questa VM. Verificare che lo stato dell'estensione di hello viene segnalato o disinstallare l'estensione hello da hello macchina virtuale e ripetere la migrazione. <br><br> La VM {nome-vm} in HostedService {nome-servizio-ospitato} contiene l'estensione {nome-estensione} con Stato Handler: {stato-handler}. Di conseguenza, non può essere migrato hello macchina virtuale. Verificare che lo stato del gestore dell'estensione hello da segnalare è {gestore-status} o disinstallarla dalla macchina virtuale hello e ripetere la migrazione. <br><br> Segnala l'agente di macchine Virtuali per la macchina virtuale {vm-name} nel servizio ospitato {ospitato-service-name} hello stato generale dell'agente non risulta pronta. Di conseguenza, hello macchina virtuale potrebbe non essere migrato, se possibile estensione. Verificare che tale agente VM hello segnala stato agente generale come pronto. Fare riferimento toohttps://aka.ms/classiciaasmigrationfaqs. |Agente guest di Azure e le estensioni di macchina virtuale in uscita internet access toohello VM storage account toopopulate necessario relativo stato. Le cause più comuni degli errori di stato includono <li> un gruppo di sicurezza di rete che blocca l'accesso in uscita toohello internet <li> Se hello rete virtuale con i server DNS locale e si perde la connettività DNS <br><br> Se si continua toosee uno stato non supportato, è possibile disinstallare hello estensioni tooskip questo controllo e continuare con la migrazione. |
| La migrazione non è supportata per la distribuzione {nome-distribuzione} in HostedService {nome-servizio-ospitato} poiché esso dispone di più set di disponibilità. |Attualmente è possibile migrare solo i servizi ospitati che dispongono di un massimo di 1 set di disponibilità. toowork questo problema, spostare hello altre set di disponibilità e le macchine virtuali in tali tooa di set di disponibilità diverso servizio ospitato. |
| Migrazione non è supportata per la distribuzione nel servizio ospitato di {deployment-name} {ospitato-service-name perché contiene macchine virtuali che non fanno parte del Set di disponibilità hello anche se è presente un servizio ospitato hello. |soluzione alternativa Hello per questo scenario è tooeither Sposta tutte le macchine virtuali hello in un singolo disponibilità impostare o rimuovere tutte le macchine virtuali dal set di disponibilità nel servizio ospitato hello hello. |
| Account di archiviazione/servizio ospitato/virtuale rete {virtual-network-name} è in corso di hello di viene eseguita la migrazione e quindi non può essere modificato |Questo errore si verifica quando è stata completata l'operazione di migrazione "Preparazione" hello sulla risorsa hello e viene attivata un'operazione che renderebbe una risorsa toohello di modifica. A causa di blocco hello sul piano di gestione di hello dopo un'operazione "Preparare", qualsiasi risorsa toohello le modifiche vengono bloccate. piano di gestione di hello toounlock, è possibile eseguire hello "Commit" migrazione operazione toocomplete o hello "Interruzione" migrazione operazione tooroll nuovamente hello "Preparare" operazione. |
| La migrazione non è consentita per HostedService {nome-servizio-ospitato} perché comprende una macchina virtuale {nome-vm} con stato: RoleStateUnknown. La migrazione è consentita solo quando hello macchina virtuale è in uno dei seguenti hello stati: in esecuzione, arrestato, arresto deallocazione. |Hello VM potrebbe essere in corso mediante una transizione di stato, in genere si verifica quando durante un'operazione di aggiornamento in hello servizio ospitato, ad esempio un riavvio, l'installazione dell'estensione e così via. È consigliabile per hello aggiornamento operazione toocomplete nel servizio ospitato hello prima di tentare la migrazione. |
| Distribuzione {deployment-name} nel servizio ospitato {ospitato-service-name} contiene una macchina virtuale {vm-name} con un disco dati {dati-disco-name} i cui blob fisico {size-of-the-vhd-blob-backing-the-data-disk} dimensioni non corrisponde a {dimensione logica di hello disco dati della macchina virtuale Size-of-the-Data-Disk-specified-in-the-VM-API} byte. La migrazione viene eseguita senza specificare una dimensione per il disco dati hello per hello VM di Azure Resource Manager. | Questo errore si verifica se è stato ridimensionato blob VHD hello senza aggiornare dimensioni hello nel modello di macchina virtuale API hello. Procedure di prevenzione dettagliate sono descritte [di seguito](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Si è verificata un'eccezione di archiviazione durante la convalida del disco dati {nome del disco dati} con collegamento ai file multimediali {URI disco dati} per la macchina virtuale {nome VM} nel servizio Cloud {nome del servizio Cloud}. Verificare che il collegamento multimediale di disco rigido virtuale hello è accessibile per la macchina virtuale | Questo errore può verificarsi se i dischi di hello di hello VM sia stato eliminato o non sono accessibili più. Verificare che hello i dischi per hello VM esiste.|
| La macchina virtuale {vm-name} nel servizio ospitato {cloud-service-name} contiene un disco che presenta il collegamento multimediale {vhd-uri} e il nome di BLOB {vhd-blob-name} che non è supportato in Azure Resource Manager. | Questo errore si verifica quando il nome di hello del blob hello ha un "/", che attualmente non è supportata nel Provider di risorse di calcolo. |
| La migrazione non è consentita per la distribuzione nel servizio ospitato {cloud-service-name} di {deployment-name} perché non è nell'ambito regionale hello. Consultare toohttp://aka.ms/regionalscope per lo spostamento di questo ambito tooregional di distribuzione. | Nel 2014, Azure ha annunciato che risorse di rete verranno spostati da un ambito tooregional ambito di livello di cluster. Vedere [http://aka.ms/regionalscope] per altri dettagli (http://aka.ms/regionalscope). Questo errore si verifica quando un'operazione di aggiornamento, che sposta automaticamente tooa internazionali ambito non è stato distribuzione hello viene eseguita la migrazione. Soluzione alternativa migliore è tooeither aggiungere un tooa endpoint macchina virtuale o un tipo di dati disco toohello macchina virtuale, quindi ripetere la migrazione. <br> Vedere [come tooset degli endpoint in una macchina virtuale di Windows classica in Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) o [collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Soluzioni di prevenzione dettagliate

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Macchina virtuale con un disco dati il cui fisica dimensione in byte del blob non corrisponde a byte la dimensione logica di hello disco dati della macchina virtuale.

Ciò accade quando hello dimensione logica del disco dati può ottenere sincronizzato con dimensioni di blob VHD effettive hello. Ciò può essere verificato con facilità utilizzando hello seguenti comandi:

#### <a name="verifying-hello-issue"></a>Verifica per determinare se il problema di hello

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Riduzione del rischio problema hello

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Lo spostamento di una sottoscrizione diversa tooa VM dopo il completamento della migrazione

Dopo aver completato il processo di migrazione hello, si consiglia di sottoscrizione di tooanother toomove hello macchina virtuale. Tuttavia, se è installato un certificato di chiave privata/hello Sposta macchina virtuale che fa riferimento a una risorsa dell'insieme di credenziali chiave, hello non è supportato. Hello istruzioni seguenti consentirà problema hello tooworkaround. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
