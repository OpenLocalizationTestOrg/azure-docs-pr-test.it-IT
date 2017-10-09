# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Eseguire il backup dei dischi di VM non gestiti con snapshot incrementali
## <a name="overview"></a>Panoramica
Archiviazione di Azure fornisce funzionalità di hello tootake snapshot di BLOB. Gli snapshot acquisiscono lo stato di blob hello a questo punto nel tempo. Questo articolo illustra uno scenario che permette di mantenere backup dei dischi delle macchine virtuali tramite snapshot. È possibile utilizzare questo metodo quando si sceglie di non toouse Azure Backup e ripristino nel servizio e desideri toocreate una strategia di backup personalizzata per i dischi di macchina virtuale.

I dischi delle macchine virtuali di Azure vengono archiviati come BLOB di pagine in Archiviazione di Azure. Poiché ci stiamo che descrive una strategia di backup per i dischi di macchina virtuale in questo articolo, viene fatto riferimento toosnapshots nel contesto di hello del BLOB di pagine. toolearn più informazioni sugli snapshot, fare riferimento troppo[creazione di uno Snapshot di un Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

## <a name="what-is-a-snapshot"></a>Che cos'è uno snapshot?
Uno snapshot di BLOB è una versione di sola lettura di un BLOB acquisito in un determinato momento. Una volta creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo. Gli snapshot forniscono un modo tooback backup di un blob così come viene visualizzato in un momento. Fino ad REST versione 2015-04-05, era gli snapshot di hello possibilità toocopy completo. Con REST versione 2015-07-08 hello e versioni successive, è inoltre possibile copiare gli snapshot incrementali.

## <a name="full-snapshot-copy"></a>Copia di snapshot completi
Gli snapshot possono essere copiati tooanother account di archiviazione da un backup tookeep blob del blob di base hello. È inoltre possibile copiare uno snapshot sul relativo blob di base, che è simile a ripristino hello blob tooan versione precedente. Quando uno snapshot viene copiato da un tooanother di account di archiviazione, occupa hello stesso spazio come blob di pagine base hello. Copia l'intero snapshot da un tooanother di account di archiviazione, pertanto è lenta e utilizza una quantità di spazio nell'account di archiviazione di destinazione hello.

> [!NOTE]
> Se si copia una destinazione di tooanother hello blob di base, snapshot hello del blob di hello non vengono copiati insieme. Analogamente, se si sovrascrive un blob di base con una copia, gli snapshot associati al blob di base hello non sono interessati e rimangono invariati con il nome di blob di base hello.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Backup di dischi mediante snapshot
Come una strategia di backup per i dischi di macchina virtuale, è possibile eseguire periodicamente snapshot del blob di pagina o disco hello e copiarli usando strumenti come account di archiviazione di tooanother [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) operazione o [AzCopy](../articles/storage/common/storage-use-azcopy.md). È possibile copiare un blob di pagine di destinazione tooa di snapshot con un nome diverso. blob di pagina di destinazione risultante Hello è un blob di pagine modificabili e non è uno snapshot. Più avanti in questo articolo vengono descritte backup tootake passaggi dei dischi di macchina virtuale utilizzando gli snapshot.

### <a name="restore-disks-using-snapshots"></a>Ripristino di dischi mediante snapshot
Quando è ora toorestore tooa il disco stabile versione che in precedenza sono state acquisite in uno degli snapshot di backup hello, è possibile copiare uno snapshot sul blob di pagine di base hello. Dopo aver snapshot hello blob di pagine di base toohello innalzate di livello, hello snapshot viene mantenuto, ma la relativa origine viene sovrascritta con una copia che può essere letta e scritta. Più avanti in questo articolo si descrive i passaggi toorestore una versione precedente del disco da relativi snapshot.

### <a name="implementing-full-snapshot-copy"></a>Implementazione di una copia di snapshot completo
È possibile implementare una copia completa procedendo come indicato di seguito hello,

* Innanzitutto, creare uno snapshot del blob di base hello utilizzando hello [Snapshot Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) operazione.
* Quindi, copia hello snapshot tooa destinazione account di archiviazione con [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob).
* Ripetere questo processo toomaintain copie di backup il blob di base.

## <a name="incremental-snapshot-copy"></a>Copia di snapshot incrementale
nuova funzionalità di Hello in hello [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API fornisce una quantità tooback modo migliore snapshot hello del BLOB di pagine o dischi. Hello API restituisce hello elenco delle modifiche tra i blob di base hello e gli snapshot di hello, che riduce hello quantità di spazio di archiviazione utilizzato nell'account di backup hello. Hello API supporta i BLOB di pagine in archiviazione Premium, nonché di archiviazione Standard. L'API permette di compilare soluzioni di backup più veloci ed efficienti per le macchine virtuali di Azure. Questa API saranno disponibili con la versione REST hello 2015-07-08 e versioni successive.

Toocopy uno storage account tooanother hello differenza tra, consente la copia dello Snapshot incrementale

* BLOB di base e relativo snapshot O
* Le due snapshot di blob di base hello

Condizione hello seguenti condizioni è soddisfatte,

* Hello blob è stato creato in gen-02-2016 o versioni successive.
* blob di Hello non è stato sovrascritto con [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) o [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) tra due snapshot.

**Nota**: questa funzionalità è disponibile per i BLOB di pagine di Azure Standard e Premium.

Quando si dispone di una strategia di backup personalizzata tramite snapshot, la copia snapshot hello da uno tooanother di account di archiviazione può essere lento e consumano spazio di archiviazione. Invece di copiare account di archiviazione di backup tooa intero snapshot hello, è possibile scrivere i blob di pagine di backup di snapshot consecutive tooa di differenza hello. In questo modo, hello ora toocopy hello spazio toostore backup e risulta notevolmente ridotto.

### <a name="implementing-incremental-snapshot-copy"></a>Implementazione di una copia di snapshot incrementale
È possibile implementare la copia dello snapshot incrementale eseguendo hello seguenti,

* Creare uno snapshot dell'utilizzo di blob di base hello [Snapshot Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob).
* Copia hello snapshot toohello destinazione backup account di archiviazione con [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob). Questo è il blob di pagine di backup di hello. Creare uno snapshot del blob di pagine backup hello e archiviarla nell'account di backup hello.
* Creare un altro snapshot del blob di base hello utilizzando Snapshot Blob.
* Ottenere la differenza hello tra gli snapshot prima e seconda hello dell'utilizzo di blob di base hello [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges). Utilizzare il nuovo parametro di hello **prevsnapshot**, toospecify hello hello snapshot di differenza hello tooget con valore DateTime. Quando questo parametro è presente, hello risposta REST include solo le pagine hello che sono state modificate tra snapshot di destinazione e allo snapshot precedente, incluse le pagine non crittografate.
* Utilizzare [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply questi blob di pagine backup toohello di modifiche.
* Infine, creare uno snapshot del blob di pagine backup hello e archiviarla nell'account di archiviazione di backup hello.

Nella sezione successiva hello, si descrive in dettaglio come è possibile gestire i backup di dischi tramite la copia dello Snapshot incrementale

## <a name="scenario"></a>Scenario
Questa sezione illustra uno scenario che comporta una strategia di backup personalizzata per i dischi delle macchine virtuali tramite gli snapshot.

Si consideri una VM Azure serie DS a cui è collegato un disco P30 di Archiviazione Premium. disco Hello P30 chiamato *mypremiumdisk* viene archiviato in un account di archiviazione premium denominato *mypremiumaccount*. Un account di archiviazione standard denominato *mybackupstdaccount* viene utilizzato per archiviare i backup hello del *mypremiumdisk*. Desideriamo tookeep uno snapshot di *mypremiumdisk* ogni 12 ore.

toolearn sulla creazione di account di archiviazione e dischi, fare riferimento troppo[gli account di archiviazione di Azure su](../articles/storage/storage-create-storage-account.md).

toolearn sul backup di macchine virtuali di Azure, fare riferimento troppo[i backup di macchina virtuale di Azure prevede](../articles/backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Backup toomaintain passaggi di un disco con snapshot incrementali
Hello passaggi seguenti viene descritto come snapshot tootake di *mypremiumdisk* e gestire i backup hello in *mybackupstdaccount*. backup Hello è un blob di pagine standard chiamato *mybackupstdpageblob*. Hello blob di pagine backup riflette sempre hello stesso stato come ultimo hello dei *mypremiumdisk*.

1. Creare uno snapshot di creare blob di pagine backup hello per il disco di archiviazione premium, *mypremiumdisk* chiamato *mypremiumdisk_ss1*.
2. Copiare questo toomybackupstdaccount snapshot come blob di pagine chiamato *mybackupstdpageblob*.
3. Creare uno snapshot di *mybackupstdpageblob* denominato *mybackupstdpageblob_ss1* usando [Snapshot Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) e archiviarlo in *mybackupstdaccount*.
4. Durante la finestra di backup hello, creare un altro snapshot di *mypremiumdisk*, ad esempio *mypremiumdisk_ss2*e archiviarlo nella *mypremiumaccount*.
5. Ottenere le modifiche incrementali hello tra gli snapshot hello due, *mypremiumdisk_ss2* e *mypremiumdisk_ss1*tramite [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) su  *mypremiumdisk_ss2* con hello **prevsnapshot** parametro impostato timestamp toohello di *mypremiumdisk_ss1*. Scrittura di blob di pagina backup toohello queste modifiche incrementali *mybackupstdpageblob* in *mybackupstdaccount*. Se sono presenti intervalli eliminati le modifiche incrementali hello, deve essere cancellati dal blob di pagine di backup di hello. Utilizzare [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) blob di pagine di backup di toowrite modifiche incrementali toohello.
6. Creare uno snapshot del blob di pagine backup hello *mybackupstdpageblob*, denominato *mybackupstdpageblob_ss2*. Eliminare lo snapshot precedente hello *mypremiumdisk_ss1* dall'account di archiviazione premium.
7. Ripetere i passaggi da 4 a 6 per ogni finestra di backup. In questo modo, è possibile gestire i backup di *mypremiumdisk* in un account di Archiviazione Standard.

![Eseguire il backup dei dischi con snapshot incrementali](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Passaggi toorestore un disco da snapshot
salve i passaggi seguenti, che descrivono come toorestore hello disco premium, *mypremiumdisk* tooan snapshot in precedenza dall'account di archiviazione di backup hello *mybackupstdaccount*.

1. Identificare hello punto nel tempo per cui si intende toorestore hello premium disco. Si supponga che si è snapshot *mybackupstdpageblob_ss2*, che viene archiviato nell'account di archiviazione di backup hello *mybackupstdaccount*.
2. In mybackupstdaccount, alzare di livello snapshot hello *mybackupstdpageblob_ss2* come blob di pagine di base backup nuovo hello *mybackupstdpageblobrestored*.
3. Creare uno snapshot di questo BLOB di pagine di backup ripristinato, denominato *mybackupstdpageblobrestored_ss1*.
4. Blob di pagine di copia hello ripristinato *mybackupstdpageblobrestored* da *mybackupstdaccount* troppo*mypremiumaccount* come disco premium nuovo hello  *mypremiumdiskrestored*.
5. Creare uno snapshot di *mypremiumdiskrestored* denominato *mypremiumdiskrestored_ss1* per le future operazioni di backup incrementale.
6. Punto serie DS hello disco della macchina virtuale ripristinata toohello *mypremiumdiskrestored* e scollegare hello precedente *mypremiumdisk* da hello macchina virtuale.
7. Avviare il processo di Backup hello descritto nella sezione precedente per il disco di ripristino hello *mypremiumdiskrestored*, utilizzando hello *mybackupstdpageblobrestored* come blob di pagine backup hello.

![Ripristino del disco da snapshot](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Passaggi successivi
Seguente hello utilizzare collega toolearn ulteriori informazioni sulla creazione di snapshot di un blob e pianificazione dell'infrastruttura di backup di VM.

* [Creazione di uno snapshot di un BLOB](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [Pianificare l'infrastruttura di backup delle VM](../articles/backup/backup-azure-vms-introduction.md)

