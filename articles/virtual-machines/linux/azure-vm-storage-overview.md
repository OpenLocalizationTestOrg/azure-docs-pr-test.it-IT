---
title: aaaAzure le macchine virtuali Linux e archiviazione di Azure | Documenti Microsoft
description: Descrive l'archiviazione Standard e Premium di Azure, Managed Disks e i dischi non gestiti con le macchine virtuali Linux.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Archiviazione delle macchine virtuali Linux e Azure
Archiviazione di Azure è una soluzione di archiviazione cloud hello per le moderne applicazioni che si basano su esigenze di hello toomeet scalabilità dei clienti, disponibilità e durata.  In aggiunta toomaking è possibile per gli sviluppatori toobuild applicazioni su larga scala toosupport nuovi scenari, archiviazione di Azure fornisce inoltre foundation archiviazione hello macchine virtuali di Azure.

## <a name="managed-disks"></a>Managed Disks

Macchine virtuali di Azure sono ora disponibili tramite [dischi gestiti di Azure](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), che consente le macchine virtuali si toocreate senza creare o gestire qualsiasi [gli account di archiviazione di Azure](../../storage/common/storage-introduction.md) manualmente. Specificare se si desidera Premium o archiviazione Standard e dimensioni disco hello devono essere e Azure hello dischi di macchina virtuale viene creato. Le macchine virtuali con Managed Disks hanno diverse funzionalità importanti, tra cui:

- Supporto per la scalabilità automatica. Azure Crea dischi hello e gestisce hello toosupport di archiviazione sottostante backup too10, 000 dischi per ogni sottoscrizione.
- Maggiore affidabilità con i set di disponibilità. Azure assicura che i dischi di macchine virtuali siano isolati automaticamente tra loro all'interno dei set di disponibilità.
- Maggiore controllo degli accessi. Managed Disks espone varie operazioni controllate dal [Controllo degli accessi in base al ruolo di Azure](../../active-directory/role-based-access-control-what-is.md).

Il prezzo di Managed Disks è diverso da quello dei dischi non gestiti. Per le relative informazioni, vedere [Prezzi e fatturazione di Managed Disks](../windows/managed-disks-overview.md#pricing-and-billing).

È possibile convertire le macchine virtuali esistenti che usano dischi gestiti toouse dischi non gestito con [az vm convertire](/cli/azure/vm#convert). Per ulteriori informazioni, vedere [come tooconvert una VM Linux da non gestito dischi dischi gestiti tooAzure](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Non è possibile convertire un disco non gestito in un disco gestito se hello non gestito disco in un account di archiviazione, o in qualsiasi momento è stata, crittografata con [crittografia Servizio archiviazione di Azure (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). dettagli come tootooconvert non gestita dischi o sono stati, in un account di archiviazione crittografati, i passaggi seguenti di Hello:

- Copiare hello disco rigido virtuale (VHD) con [avvio di copia blob archiviazione az](/cli/azure/storage/blob/copy#start) tooa account di archiviazione che non è mai stato abilitato per la crittografia del servizio di archiviazione di Azure.
- Creare una macchina virtuale che usi dischi gestiti e specificare il file del disco rigido virtuale durante la creazione con [az vm create](/cli/azure/vm#create) o
- Collegare hello copiati VHD con [collegare il disco di macchina virtuale az](/cli/azure/vm/disk#attach) tooa in esecuzione sulla macchina virtuale con dischi gestiti.


## <a name="azure-storage-standard-and-premium"></a>Archiviazione di Azure: Standard e Premium
È possibile creare macchine virtuali di Azure, con Managed Disks o dischi non gestiti, basate su dischi di archiviazione Standard o Premium. Quando si utilizza toochoose portale hello la macchina virtuale è necessario attivare o disattivare un elenco a discesa in hello **nozioni di base** tooview schermata dischi standard e premium. Quando le unità attivato/disattivato tooSSD, solo le macchine virtuali abilitate, verranno visualizzate di archiviazione premium tutte supportate dalle unità SSD.  Quando vengono visualizzati tooHDD attivato/disattivato, le macchine virtuali abilitati archiviazione standard supportate da ruotando le unità disco, con archiviazione premium macchine virtuali supportate da unità SSD.

Quando si crea una macchina virtuale da hello `azure-cli` è possibile scegliere tra standard e premium, quando si sceglie di dimensioni della macchina virtuale tramite hello hello `-z` o `--vm-size` flag cli.

## <a name="creating-a-vm-with-a-managed-disk"></a>Creazione di una macchina virtuale con un disco gestito

l'esempio Hello necessario hello CLI di Azure 2.0, è possibile [installare qui](/cli/azure/install-azure-cli).

Creare innanzitutto un hello toomanage gruppo di risorse alle risorse con [gruppo az creare](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Creare ora hello macchina virtuale con [creare vm az](/cli/azure/vm#create). Specificare un argomento `--public-ip-address-dns-name` univoco, in quanto viene usato probabilmente `mypublicdns`.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

esempio di Hello precedente crea una macchina virtuale con un disco gestito in un account di archiviazione Standard. toouse un account di archiviazione Premium, aggiungere hello `--storage-sku Premium_LRS` argomento, ad esempio hello di esempio seguente:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Archiviazione standard
Standard di archiviazione Azure è il tipo predefinito hello di archiviazione.  Archiviazione standard è conveniente e garantisce ottime prestazioni.  

## <a name="premium-storage"></a>Archiviazione Premium
Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con I/O intensivo. I dischi delle macchine virtuali (VM) che usano Archiviazione Premium archiviano i dati in unità SSD (Solid State Drive). È possibile migrare tooAzure di dischi macchina virtuale dell'applicazione velocità hello sfruttare tootake archiviazione Premium e le prestazioni di questi dischi.

Funzionalità di Archiviazione Premium:

* I dischi di archiviazione Premium: Archiviazione Premium di Azure supporta dischi di macchina virtuale che possono essere collegato tooDS, DSv2 o GS serie macchine virtuali di Azure.
* Blob di pagine Premium: Archiviazione Premium supporta BLOB di pagine di Azure, che vengono utilizzati toohold dischi persistenti per macchine virtuali di Azure (VM).
* Archiviazione con ridondanza locale Premium: Un account di archiviazione Premium solo supporta localmente ridondante archiviazione (LRS) come opzione di replica hello e mantiene tre copie dei dati hello all'interno di una singola area.
* [Archiviazione Premium](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>VM supportate da Archiviazione Premium
Archiviazione Premium supporta Macchine virtuali di Azure (VM) delle serie DS, DSv2, GS e Fs. Con le VM supportate da Archiviazione Premium è possibile usare dischi sia di Archiviazione Standard che di Archiviazione Premium. Non è tuttavia possibile usare i dischi di Archiviazione Premium con le macchine virtuali di serie non compatibili con Archiviazione Premium.

Di seguito sono hello distribuzioni di Linux che è stati convalidati con archiviazione Premium.

| Distribuzione | Versione | Kernel supportato |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Archiviazione file di Azure
Archiviazione di File di Azure offre le condivisioni di file in un cloud di hello tramite il protocollo SMB standard di hello. I file di Azure, è possibile eseguire la migrazione di applicazioni aziendali che si basano su file server tooAzure. Le applicazioni in esecuzione in Azure possono montare condivisioni file dalle macchine virtuali di Azure con Linux. E con una versione più recente di hello di archiviazione di File, è inoltre possibile collegare una condivisione file da un'applicazione locale che supporta SMB 3.0.  Poiché le condivisioni file sono condivisioni SMB, è possibile accedervi tramite le API del file system standard.

Archiviazione di file è basata su hello stessa tecnologia di archiviazione Blob, tabelle e code, in modo da archiviazione di File offre disponibilità hello, durata, scalabilità e ridondanza geografica che viene compilata nella piattaforma di archiviazione di Azure hello. Per informazioni sugli obiettivi di prestazioni e sui limiti di Archiviazione file, vedere Obiettivi di scalabilità e prestazioni per Archiviazione di Azure.

* [Come toouse archiviazione di File di Azure con Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Archiviazione ad accesso frequente
livello di archiviazione di Azure a caldo Hello è ottimizzato per l'archiviazione dei dati che si accede frequentemente.  Archiviazione a caldo è tipo di archiviazione hello predefinito per gli archivi blob.

## <a name="cool-storage"></a>Archiviazione ad accesso sporadico
livello di archiviazione Azure sporadico Hello è ottimizzato per l'archiviazione dei dati sono raramente accessibile e lunga durata. Esempi di casi d'uso dell'archiviazione ad accesso sporadico includono backup, contenuti multimediali, dati scientifici, conformità e archiviazione dati. In generale, i dati usati raramente sono i candidati ideali per l'archiviazione ad accesso sporadico.

|  | livello di archiviazione ad accesso frequente | livello di archiviazione ad accesso sporadico |
|:--- |:---:|:---:|
| Disponibilità |99,9% |99% |
| Disponibilità (letture RA-GRS) |99,99% |99,9% |
| Addebiti per utilizzo |Costi di archiviazione più elevati |Costi di archiviazione più bassi |
| Accesso inferiore |Accesso superiore | |
| e costi di transazione |e costi di transazione | |

## <a name="redundancy"></a>Ridondanza
dati Hello in di Microsoft Azure è sempre l'account di archiviazione replicata tooensure durabilità e disponibilità elevata, riunione hello contratto di servizio di archiviazione Azure, anche in faccia hello di errori hardware temporanei.

Quando si crea un account di archiviazione, è necessario selezionare una delle seguenti opzioni di replica hello:

* Archiviazione con ridondanza locale (LRS)
* Archiviazione con ridondanza della zona (ZRS).
* Archiviazione con ridondanza geografica (GRS)
* Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).

### <a name="locally-redundant-storage"></a>Archiviazione con ridondanza locale
I dati all'interno di area hello in cui viene creato l'account di archiviazione vengono replicati archiviazione localmente ridondante (LRS). toomaximize durabilità, ogni richiesta effettuata per i dati nell'account di archiviazione vengono replicate tre volte. Queste tre repliche risiedono ognuna in domini di errore e domini di aggiornamento distinti.  Una richiesta viene restituita correttamente solo dopo che è stato scritto tooall tre repliche.

### <a name="zone-redundant-storage"></a>Archiviazione con ridondanza della zona
Archiviazione con ridondanza della zona (ZRS), i dati vengono replicati tra due strutture toothree, all'interno di una singola area o in due aree, fornendo una durabilità maggiore rispetto a ridondanza locale. Se l'account di archiviazione dispone di ridondanza della zona abilitata, i dati sono durevoli anche in caso di errore a una delle strutture di hello di hello.

### <a name="geo-redundant-storage"></a>Archiviazione con ridondanza geografica
Archiviazione con ridondanza geografica (GRS) consente di replicare i dati tooa area secondaria a centinaia di miglia di distanza area primaria hello. Se l'account di archiviazione con ridondanza geografica abilitata, i dati sono durevoli anche in caso di hello di una completa interruzione dell'alimentazione locale o di emergenza in cui hello area primaria non è recuperabile.

### <a name="read-access-geo-redundant-storage"></a>Archiviazione con ridondanza geografica e accesso in lettura
Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) ottimizza la disponibilità dell'account di archiviazione, fornendo i dati di accesso in sola lettura toohello nella posizione secondaria hello, inoltre toohello replica tra due aree fornito dalla funzionalità GRS. In caso di hello che i dati diventino non disponibili nell'area primaria hello, l'applicazione può leggere i dati dall'area secondaria hello.

Per un approfondimento sulla ridondanza dell'Archiviazione di Azure, vedere:

* [Replica di Archiviazione di Azure](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Scalabilità
Archiviazione di Azure è altamente scalabile, pertanto è possibile archiviare ed elaborare centinaia di terabyte di scenari di dati toosupport hello dati necessari per l'analisi di scientifici, finanziari e applicazioni multimediali. Oppure è possibile archiviare hello piccole quantità di dati necessari per un sito Web di piccole aziende. Ogni volta che sono comprese le proprie esigenze, si paga solo per i dati di hello che si desidera archiviare. In Archiviazione di Azure sono al momento archiviate decine di migliaia di miliardi di oggetti univoci dei clienti e sono gestiti in media milioni di richieste al secondo.

Per gli account di archiviazione standard: un account di archiviazione standard con una frequenza totale massima di richieste di 20.000 IOPS. Hello IOPS totali per tutti i dischi di macchina virtuale in un account di archiviazione standard non deve superare questo limite.

Per gli account di archiviazione Premium: un account di archiviazione Premium ha una velocità effettiva totale massima di 50 Gbps. velocità effettiva totale Hello in tutti i dischi di macchina virtuale non deve superare questo limite.

## <a name="availability"></a>Disponibilità
È garantito che almeno 99,99% (99,9% per il livello di accesso sporadico) di tempo hello, si verrà correttamente elaborare richieste tooread dati dagli account di archiviazione con ridondanza geografica di accesso in lettura (RA-GRS), condizione che non è stato possibile tentativi tooread dati dall'area primaria hello Ritentare in area secondaria hello.

È garantito che almeno il 99,9% (99% per il livello di accesso sporadico) di tempo hello, verrà completata processo richiede i dati tooread archiviazione con ridondanza locale (LRS), archiviazione ridondante zona (ZRS) e account di archiviazione con ridondanza geografica (GRS).

È garantito che almeno il 99,9% (99% per il livello di accesso sporadico) di tempo hello, verrà completata processo richiede toowrite dati tooLocally archiviazione ridondante (LRS), zona ridondanti archiviazione (ZRS) e gli account di archiviazione (GRS) con ridondanza geografica e con ridondanza geografica di accesso in lettura Account di archiviazione (RA-GRS).

* [Contratto di servizio per l'archiviazione di Azure](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Regioni
Azure è in genere disponibile nelle 30 aree tutto il mondo hello e ha annunciato piani per le aree aggiuntive 4. Espansione geografica è una priorità per Azure, perché consente prestazioni più elevate di tooachieve nostri clienti e supporta i requisiti e le preferenze relative al percorso dei dati.  Azures toolaunch area più recente è in Germania.

Hello Germania Microsoft Cloud fornisce un toohello opzione differenziati già disponibili i servizi Cloud Microsoft in Europa, creazione di maggiori opportunità di innovazione e la crescita economica per elevata regolamentato partner e clienti in Germania, Hello (unione) e hello associazione franca europea (EFTA).

Dati del cliente in questi Data Center di nuovo, Magdeburg e Francoforte, viene gestiti nel controllo del codice di un dominio trusted di dati, T sistemi internazionali, una società tedesca indipendente e figlia di Deutsche Telekom hello. Servizi cloud commerciali di Microsoft in questi Data Center rispettare norme di gestione dei dati di tooGerman e offrono ai clienti le scelte aggiuntive di come e dove i dati vengono elaborati.

* [Mappa delle aree di Azure](https://azure.microsoft.com/regions/)

## <a name="security"></a>Sicurezza
Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza che insieme consentono agli sviluppatori di applicazioni sicure toobuild. account di archiviazione Hello stesso può essere protetto tramite controllo di accesso basato sui ruoli e Azure Active Directory. È possibile proteggere i dati in transito tra un'applicazione e Azure usando la crittografia lato client, HTTPS o SMB 3.0. Dati possono essere impostati toobe crittografato automaticamente quando scritti tooAzure archiviazione mediante la crittografia del servizio di archiviazione (SSE). I dischi del sistema operativo e i dati utilizzati dalle macchine virtuali possono essere impostati toobe crittografata con la crittografia del disco di Azure. È possibile concedere l'accesso delegato toohello dati oggetti nell'archiviazione di Azure tramite firme di accesso condiviso.

### <a name="management-plane-security"></a>Sicurezza del piano di gestione
il piano di gestione di Hello è costituito da toomanage le risorse usate hello account di archiviazione. In questa sezione verrà descritto come modello di distribuzione Azure Resource Manager hello e modalità di accesso di account di archiviazione tooyour toouse toocontrol di controllo di accesso basato sui ruoli (RBAC). Verranno inoltre presentati gestire le chiavi di account di archiviazione e come tooregenerate li.

### <a name="data-plane-security"></a>Sicurezza del piano dati
In questa sezione verrà esaminato consentire l'accesso agli oggetti di dati effettivi di toohello nell'account di archiviazione, ad esempio BLOB, file, code e tabelle, tramite firme di accesso condiviso e criteri di accesso archiviati. Vengono trattate anche le firme di accesso condiviso sia a livello di servizio che di account. Si noterà anche come toolimit accedere tooa specifico indirizzo IP (o un intervallo di indirizzi IP), come protocollo di hello toolimit utilizzato tooHTTPS e come toorevoke una firma di accesso condiviso senza attendere che tooexpire.

## <a name="encryption-in-transit"></a>Crittografia in transito
Questa sezione viene descritto come toosecure dati durante il trasferimento da o verso l'archiviazione di Azure. Parleremo hello consigliato l'utilizzo della crittografia hello e HTTPS utilizzata da SMB 3.0 per condivisioni File di Azure. È inoltre verrà dare un'occhiata crittografia lato Client, che consentono di tooencrypt hello prima di essere trasferiti nell'account di archiviazione in un'applicazione client e toodecrypt hello dati dopo che viene trasferita all'esterno di archiviazione.

## <a name="encryption-at-rest"></a>Crittografia di dati inattivi
Si parlerà crittografia del servizio di archiviazione (SSE) e come è possibile abilitare la funzionalità per un account di archiviazione, pertanto i BLOB in blocchi, BLOB di pagine e aggiungere BLOB viene crittografato automaticamente quando scritti tooAzure archiviazione. Verranno inoltre esaminati come è possibile utilizzare la crittografia del disco di Azure e analizzare le differenze di base hello e casi di crittografia del disco e SSE e crittografia lato Client. Si esaminerà brevemente la conformità FIPS per i computer del Governo degli Stati Uniti.

* [Guida alla sicurezza di Archiviazione di Azure](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Disco temporaneo
Ogni VM contiene un disco temporaneo. disco temporaneo Hello fornisce l'archiviazione a breve termine per i processi e le applicazioni e dati di archivio tooonly desiderato, ad esempio i file di paging o di scambio. Dati su disco temporaneo hello potrebbero andare persi durante un [evento di manutenzione](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o quando si [ridistribuire una macchina virtuale](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante un riavvio standard di hello VM, dati hello nell'unità temporanea hello devono essere rese persistenti.

Nelle macchine virtuali Linux, hello disco è in genere **dev/sdb** formattato e montato troppo**/mnt** da hello agente Linux di Azure. dimensioni Hello del disco temporaneo hello variano in base alle dimensioni di hello della macchina virtuale hello. Per altre informazioni, vedere [Dimensioni per le macchine virtuali Linux](sizes.md).

Per ulteriori informazioni sulle modalità di utilizzo disco temporaneo hello Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Risparmi sui costi
* [Costi di archiviazione](https://azure.microsoft.com/pricing/details/storage/)
* [Calcolatore dei costi di archiviazione](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Limiti relativi ad Archiviazione
* [Limiti del servizio di archiviazione](../../azure-subscription-service-limits.md#storage-limits)
