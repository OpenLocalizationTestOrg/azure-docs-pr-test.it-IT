Questo articolo vengono illustrati un set di procedure comprovate per una macchina virtuale di Windows (VM) è in esecuzione in Azure, prestando attenzione tooscalability, disponibilità, gestibilità e sicurezza.

> [!NOTE]
> Azure offre due diversi modelli di distribuzione, ovvero [Azure Resource Manager][resource-manager-overview] e la distribuzione classica. Questo articolo usa Azure Resource Manager, consigliato da Microsoft per le nuove distribuzioni.
>
>

Non è consigliabile usare una singola VM per carichi di lavoro di importanza strategica perché crea un singolo punto di guasto. Per una disponibilità più elevata, distribuire più VM in un [set di disponibilità][availability-set]. Per altre informazioni, vedere [Esecuzione di più VM in Azure][multi-vm].

## <a name="architecture-diagram"></a>Diagramma dell'architettura

Provisioning di una macchina virtuale in Azure comporta più lo spostamento di parti di hello solo macchina virtuale stessa. Sono presenti elementi di calcolo, rete e archiviazione.

> Un documento di Visio che include questo diagramma dell'architettura è disponibile per il download da hello [Microsoft download center][visio-download]. Questo diagramma è hello "Calcolo - singola macchina virtuale" pagina.
>
>

![[0]][0]

* **Gruppo di risorse.** Un [*gruppo di risorse*][resource-manager-overview] è un contenitore in cui risiedono le risorse correlate. Creare una risorsa di risorse del gruppo toohold hello per questa macchina virtuale.
* **VM**. È possibile eseguire il provisioning di una macchina virtuale da un elenco di immagini pubblicate o da un file di disco rigido virtuale (VHD) che si carica tooAzure nell'archiviazione Blob.
* **Disco del sistema operativo.** disco del sistema operativo Hello è un disco rigido virtuale archiviato in [di archiviazione di Azure][azure-storage]. Ciò significa che persiste anche se i computer host hello diventa inattivo.
* **Disco temporaneo.** Hello macchina virtuale viene creato con un disco temporaneo (hello `D:` unità in Windows). Questo disco è archiviato in un'unità fisica nel computer host hello. *Non* viene salvato nell'Archiviazione di Azure ed è possibile che venga eliminato durante i riavvii e altri eventi del ciclo di vita della VM. Usare questo disco solo per dati temporanei, ad esempio file di paging o di scambio.
* **Dischi dati.** Un [disco dati][data-disk] è un VHD persistente usato per i dati dell'applicazione. I dischi dati vengono archiviati in archiviazione di Azure come disco di hello del sistema operativo.
* **Rete virtuale (VNet) e subnet.** Ogni VM in Azure viene distribuita in una rete virtuale (VNet), che viene a sua volta suddivisa in subnet.
* **Indirizzo IP pubblico.** Un indirizzo IP pubblico è necessario toocommunicate con hello VM&mdash;ad esempio tramite desktop remoto (RDP).
* **Interfaccia di rete (NIC)**. Hello NIC consente hello VM toocommunicate con la rete virtuale hello.
* **Gruppo di sicurezza di rete**. Hello [NSG] [ nsg] tooallow/deny utilizzato rete traffico toohello subnet. Un NSG può essere associato a una singola scheda di interfaccia di rete o a una subnet. Se si associa una subnet, hello NSG regole tooall macchine virtuali nella subnet.
* **Diagnostica.** La registrazione diagnostica è fondamentale per la gestione e risoluzione dei problemi hello macchina virtuale.

## <a name="recommendations"></a>Raccomandazioni

Hello indicazioni seguenti si applica per la maggior parte degli scenari. Seguire queste indicazioni, a meno che non si disponga di un requisito specifico che le escluda.

### <a name="vm-recommendations"></a>Indicazioni per le VM

Azure offre diverse dimensioni di macchina virtuale diversa, ma è consigliabile DS e GS serie hello perché supporta le dimensioni delle macchine [archiviazione Premium][premium-storage]. Selezionare una di queste dimensioni del computer, a meno che non si abbia un carico di lavoro specializzato, ad esempio di high-performance computing. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali in Azure][virtual-machine-sizes].

Se si sta spostando un tooAzure del carico di lavoro esistente, iniziare con dimensioni VM hello sono tooyour corrispondenza più vicina hello server locali. Hello misurazione delle prestazioni del carico di lavoro effettivo con rispettano tooCPU, memoria e operazioni di input/output su disco al secondo (IOPS), quindi, se necessario, modificare le dimensioni di hello. Se si richiedono più schede di rete per la macchina virtuale, tenere presente che numero massimo di hello di schede di rete è una funzione di hello [dimensioni delle macchine Virtuali][vm-size-tables].   

Quando si esegue il provisioning hello VM e altre risorse, è necessario specificare un'area. In generale, scegliere un'area più vicina agli utenti interni di tooyour o ai clienti. È tuttavia possibile che non tutte le dimensioni della VM siano disponibili in tutte le località. Per informazioni dettagliate, vedere i [servizi disponibili in base all'area][services-by-region]. un elenco di hello dimensioni delle macchine Virtuali disponibili in base all'area geografica, eseguire il comando di Azure interfaccia della riga di comando (CLI) seguente hello toosee:

```
azure vm sizes --location <location>
```

Per informazioni sulla scelta di un'immagine di VM pubblicata, vedere [Esplorare e selezionare immagini di macchine virtuali Windows in Azure con PowerShell o l'interfaccia della riga di comando][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Indicazioni per il disco e l'archiviazione

Per ottimizzare le prestazioni I/O del disco, si consiglia di usare [Archiviazione Premium][premium-storage], che archivia i dati in unità SSD (Solid State Drive). Costo si basa su dimensioni hello del disco di provisioning hello. Anche IOPS e velocità effettiva dipendono dalle dimensioni del disco. Quando si effettua il provisioning di un disco è quindi consigliabile tenere in considerazione tutti e tre i fattori, ovvero capacità, IOPS e velocità effettiva.

Creare gli account di archiviazione di Azure separato per ogni VM toohold hello rigido i dischi virtuali (VHD) in ordine tooavoid raggiungere i limiti IOPS hello per gli account di archiviazione.

Aggiungere uno o più dischi dati. Quando si crea un nuovo VHD, il disco non è formattato. Accedere al disco di hello VM tooformat hello. Se si dispone di un numero elevato di dischi dati, essere consapevoli dei limiti dei / o totali di hello hello dell'account di archiviazione. Per altre informazioni, vedere [Limiti relativi ai dischi della macchina virtuale][vm-disk-limits].

Se possibile, installare applicazioni su un disco dati, non su disco del sistema operativo hello. Tuttavia, alcune applicazioni legacy potrebbe essere necessario componenti tooinstall in unità c: hello. In tal caso, è possibile [ridimensionamento del disco del sistema operativo hello] [ resize-os-disk] tramite PowerShell.

Per prestazioni ottimali, creare un account di archiviazione separata toohold i log di diagnostica. Un account di archiviazione con ridondanza locale standard è sufficiente per i log di diagnostica.

### <a name="network-recommendations"></a>Indicazioni per la rete

indirizzo IP pubblico Hello può essere dinamico o statico. valore predefinito di Hello è dinamico.

* Riserva un [indirizzo IP statico] [ static-ip] se è necessario un indirizzo IP fisso che non cambia &mdash; , ad esempio, se è necessario toocreate un record in DNS o necessario hello elenco provvisoria tooa aggiunto toobe indirizzi IP.
* È anche possibile creare un nome di dominio completo (FQDN) per l'indirizzo IP hello. È quindi possibile registrare un [record CNAME] [ cname-record] in DNS che punta toohello FQDN. Per ulteriori informazioni, vedere [creare un nome di dominio completo nel portale di Azure hello][fqdn].

Tutti i gruppi di sicurezza di rete contengono un set di [regole predefinite][nsg-default-rules], inclusa una regola che blocca tutto il traffico Internet in ingresso. le regole predefinite di Hello non possono essere eliminate, ma altre regole possono eseguirne l'override. tooenable il traffico Internet, creare regole che consentano il traffico in entrata toospecific porte &mdash; , ad esempio, la porta 80 per HTTP.  

tooenable RDP, aggiungere una regola di gruppo che consenta il traffico in entrata tooTCP porta 3389.

## <a name="scalability-considerations"></a>Considerazioni sulla scalabilità

È possibile ridimensionare una macchina virtuale verso l'alto o verso il basso per [la modifica delle dimensioni della macchina virtuale hello](../articles/virtual-machines/windows/sizes.md). tooscale out orizzontalmente, inserire due o più macchine virtuali in un set di bilanciamento del carico di disponibilità. Per informazioni dettagliate, vedere [Running multiple VMs on Azure for scalability and availability][multi-vm] (Esecuzione di più VM in Azure per la scalabilità e la disponibilità).

## <a name="availability-considerations"></a>Considerazioni sulla disponibilità

Per una disponibilità più elevata, distribuire più VM in un set di disponibilità. Sarà così disponibile anche un [contratto di servizio][vm-sla] (SLA) di livello più elevato.

È possibile che la VM sia interessata da attività di [manutenzione pianificata][planned-maintenance] o [manutenzione non pianificata][manage-vm-availability]. È possibile utilizzare [VM riavviare registri] [ reboot-logs] toodetermine se una macchina virtuale di riavviare il computer è stato causato da attività di manutenzione pianificato.

I dischi rigidi virtuali vengono archiviati nell'[archivio di Azure][azure-storage] e l'archivio di Azure viene replicato per assicurare durabilità e disponibilità.

tooprotect contro la perdita di dati accidentali durante le normali operazioni (ad esempio, a causa di errori dell'utente), è inoltre necessario implementare backup temporizzati in, utilizzando [blob snapshot] [ blob-snapshot] o un altro strumento.

## <a name="manageability-considerations"></a>Considerazioni sulla gestibilità

**Gruppi di risorse.** Risorse strettamente a tale condivisione hello del ciclo di vita stesso in hello stesso [gruppo di risorse][resource-manager-overview]. Gruppi di risorse consentono toodeploy e monitoraggio risorse come un gruppo e rollup fatturazione i costi dovuti al gruppo di risorse. È inoltre possibile eliminare un intero set di risorse, operazione molto utile nelle distribuzioni di test. Assegnare alle risorse nomi significativi. Che rende più semplice toolocate una risorsa specifica e comprendere il ruolo. Vedere [Recommended Naming Conventions for Azure Resources][naming conventions] (Convenzioni di denominazione consigliate per le risorse di Azure).

**Diagnostica delle VM.** Abilitare il monitoraggio e la diagnostica, tra cui le metriche di base sull'integrità, i log relativi all'infrastruttura di diagnostica e la [diagnostica di avvio][boot-diagnostics]. La diagnostica di avvio permette di diagnosticare gli errori di avvio quando la VM passa a uno stato non avviabile. Per altre informazioni, vedere [Abilitare il monitoraggio e la diagnostica][enable-monitoring]. Hello utilizzare [raccolta di Log di Azure] [ log-collector] toocollect estensione della piattaforma Azure registra e caricarli tooAzure archiviazione.   

Hello comando CLI seguente abilita la diagnostica:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Arresto di una VM.** Azure distingue tra gli stati "Arrestato" e "Deallocato". Vengono addebitati quando hello stato della macchina virtuale viene arrestato, ma non quando viene deallocato hello macchina virtuale.

Utilizzare hello toodeallocate comando CLI una macchina virtuale seguente:

```
azure vm deallocate <resource-group> <vm-name>
```

Nel portale di Azure hello, hello **arrestare** pulsante dealloca hello macchina virtuale. Tuttavia, se si arresta tramite hello del sistema operativo mentre si è connessi, hello macchina virtuale è stato arrestato ma *non* deallocazione viene comunque addebitata.

**Eliminazione di una VM.** Se si elimina una macchina virtuale, i dischi rigidi virtuali hello non vengono eliminati. Ciò significa che è possibile eliminare in modo sicuro hello VM senza perdita di dati. Verranno tuttavia applicati comunque addebiti per l'archiviazione. hello toodelete disco rigido virtuale, eliminare il file hello da [nell'archiviazione Blob][blob-storage].

tooprevent accidentali, utilizzare un [blocco di risorsa] [ resource-lock] toolock hello intera risorsa blocco o gruppo singole risorse, ad esempio hello macchina virtuale.

## <a name="security-considerations"></a>Considerazioni relative alla sicurezza

Utilizzare [Centro sicurezza di Azure] [ security-center] tooget una vista centrale dello stato di sicurezza hello di risorse di Azure. Centro sicurezza PC monitora i potenziali problemi di sicurezza e offre un quadro completo dell'integrità di protezione hello della distribuzione. Il Centro sicurezza è configurato per ogni sottoscrizione di Azure. Abilitare la raccolta dei dati di sicurezza come descritto in [Usare il Centro sicurezza]. Quando la raccolta dei dati è abilitata, il Centro sicurezza analizza automaticamente tutte le macchine virtuali create nell'ambito della sottoscrizione.

**Gestione delle patch.** Se abilitato, Centro sicurezza PC controlla se mancano aggiornamenti critici e della sicurezza. Utilizzare [le impostazioni di criteri di gruppo] [ group-policy] per gli aggiornamenti automatici del sistema di hello VM tooenable.

**Antimalware.** Se abilitato, Centro sicurezza PC controlla se è installato il software antimalware. È inoltre possibile utilizzare il Centro sicurezza PC tooinstall software antimalware all'interno di hello portale di Azure.

**Operazioni.** Utilizzare [controllo di accesso basato sui ruoli] [ rbac] (RBAC) toocontrol accesso toohello Azure le risorse da distribuire. RBAC consente di assegnare l'autorizzazione ruoli toomembers del team DevOps. Ad esempio, il ruolo di lettore hello può visualizzare le risorse di Azure, ma non creare, gestire o eliminarli. Alcuni ruoli sono tooparticular specifici tipi di risorse di Azure. Ad esempio, il ruolo di collaboratore alla macchina virtuale hello possibile riavviare o deallocare una macchina virtuale, reimpostare la password di amministratore di hello, creare una nuova macchina virtuale e così via. Altri [ruoli predefiniti di Controllo degli accessi in base al ruolo][rbac-roles] che potrebbero essere utili per questa architettura di riferimento includono [Utente DevTest Labs][rbac-devtest] e [Collaboratore Rete][rbac-network]. Un utente può essere assegnato ruoli toomultiple, ed è possibile creare ruoli personalizzati per anche altre autorizzazioni specifiche.

> [!NOTE]
> RBAC non limita le azioni che un utente connesso in una macchina virtuale è possibile eseguire hello. Tali autorizzazioni sono determinate dal tipo di account hello del sistema operativo guest hello.   
>
>

password dell'amministratore locale hello tooreset, eseguire hello `vm reset-access` comando CLI di Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Utilizzare [log di controllo] [ audit-logs] toosee provisioning azioni e altri eventi della macchina virtuale.

**Crittografia dei dati.** Prendere in considerazione [crittografia del disco Azure] [ disk-encryption] se è necessario tooencrypt hello del sistema operativo e i dischi dati.

## <a name="solution-deployment"></a>Distribuzione della soluzione

Una distribuzione di questa architettura di riferimento è disponibile in [GitHub][github-folder]. Include una rete virtuale, un gruppo di sicurezza di rete e una singola VM. toodeploy hello architettura, seguire questi passaggi:

1. Fare clic con il pulsante destro pulsante hello e selezionare entrambi "Apri collegamento in una nuova scheda" o "Apri collegamento in una nuova finestra."  
   [![Distribuire tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Se il collegamento hello è aperta in hello portale di Azure, è necessario immettere valori per alcune delle impostazioni di hello:

   * Hello **gruppo di risorse** nome è già definito nel file di parametro hello, pertanto selezionare **Crea nuovo** e immettere `ra-single-vm-rg` nella casella di testo hello.
   * Area hello selezionare da hello **percorso** elenchi a discesa.
   * Non modificare hello **Uri radice modello** o hello **Uri radice parametro** caselle di testo.
   * Selezionare **windows** in hello **tipo di sistema operativo** elenchi a discesa.
   * Esaminare le condizioni di hello, quindi fare clic su hello **accetto le condizioni indicate in precedenza toohello** casella di controllo.
   * Fare clic su hello **acquisto** pulsante.
3. Attendere hello toocomplete di distribuzione.
4. i file dei parametri Hello includono un nome utente dell'amministratore a livello di codice e una password, pertanto è consigliabile immediatamente modificare entrambe. Fare clic sulla macchina virtuale denominata hello `ra-single-vm0 `in hello portale di Azure. Quindi, fare clic su **reimpostazione password** in hello **supporto + risoluzione dei problemi** blade. Selezionare **reimpostazione password** in hello **modalità** casella a discesa, quindi selezionare un nuovo **nome utente** e **Password**. Fare clic su hello **aggiornamento** pulsante toopersist hello nuovo nome utente e password.

Per informazioni su altri modi toodeploy questa architettura di riferimento, vedere il file Leggimi hello in hello [materiale sussidiario per singola macchina virtuale][github-folder]] cartella GitHub.

## <a name="customize-hello-deployment"></a>Personalizzare la distribuzione di hello
Se è necessario toochange hello distribuzione toomatch le proprie esigenze, seguire le istruzioni hello hello [Leggimi][github-folder].

## <a name="next-steps"></a>Passaggi successivi
Per una maggiore disponibilità, distribuire due o più macchine virtuali dietro un servizio di bilanciamento del carico. Per altre informazioni, vedere [Esecuzione di più VM in Azure][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Usare il Centro sicurezza]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Singola architettura VM di Windows in Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
