# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Aree e disponibilità per le macchine virtuali in Azure
Azure viene eseguita in più Data Center di tutto il mondo hello. Questi Data Center sono raggruppati in aree toogeographic, offrendo maggiore flessibilità nella scelta where toobuild delle applicazioni. È importante toounderstand come e dove le macchine virtuali (VM) opera in Azure, con le opzioni toomaximize prestazioni, disponibilità e la ridondanza. In questo articolo fornisce una panoramica della disponibilità di hello e funzionalità di ridondanza di Azure.

## <a name="what-are-azure-regions"></a>Che cosa sono le aree di Azure?
Le risorse di Azure vengono create in determinate aree geografiche, come "Stati Uniti occidentali", "Europa settentrionale" o "Asia sud-orientale". È possibile esaminare hello [elenco di aree e le relative posizioni](https://azure.microsoft.com/regions/). All'interno di ogni area più Data Center esiste tooprovide per garantire ridondanza e disponibilità. La progettazione toomeet e applicazioni toocreate macchine virtuali più vicino tooyour gli utenti qualsiasi, conformità o scopi fiscali, questo approccio offre flessibilità.

## <a name="special-azure-regions"></a>Aree speciali di Azure
Azure offre alcune aree speciale che può essere utile toouse durante la compilazione di applicazioni per scopi legali o di conformità. Le aree speciali includono:

* **US Gov Virginia** e **US Gov Iowa**
  * Un'istanza logica e fisica di Azure isolata dalla rete per i partner e gli enti pubblici statunitensi, gestita da persone selezionate negli Stati Uniti. Include certificazioni di conformità aggiuntive, come [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) e [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Ulteriori informazioni su [Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/).
* **Cina orientale** e **Cina settentrionale**
  * Tali aree sono disponibili tramite una relazione univoca tra Microsoft e 21Vianet, in base al quale Data Center hello non viene mantenuto direttamente da Microsoft. Altre informazioni sulla [disponibilità di Microsoft Azure in Cina](http://www.windowsazure.cn/).
* **Germania centrale** e **Germania nord-orientale**
  * Tali aree sono disponibili tramite un modello di trustee di dati in base al quale i dati dei clienti rimangono in Germania sotto controllo di T-Systems, una società Deutsche Telekom, che agisce come trustee dati tedesco hello.

## <a name="region-pairs"></a>Coppie di aree
Ogni area di Azure è associato a un'altra area all'interno di hello geography stesso (ad esempio Stati Uniti, Europa o in Asia). Questo approccio consente la replica di hello delle risorse, ad esempio l'archiviazione macchina virtuale, in un'area geografica che dovrebbe ridurre il rischio di hello di calamità naturali, unrest civile, interruzioni dell'alimentazione o interruzioni della rete fisica che interessano entrambe le aree in una sola volta. Tra gli ulteriori vantaggi delle coppie di aree:

* Nell'evento hello di un'interruzione di Azure più ampia, è assegnata la priorità di un'area da ogni coppia toohelp ridurre toorestore ora hello per le applicazioni. 
* Gli aggiornamenti pianificati di Azure vengono implementati aree toopaired uno in un tempo di inattività toominimize ora e rischio di interruzione dell'applicazione.
* Dati continuano tooreside all'interno di hello geography stesso come la relativa coppia (ad eccezione del Brasile) per scopi di competenza imposizione imposte e il diritto.

Esempi di coppie di aree includono:

| Primario | Secondario |
|:--- |:--- |
| Stati Uniti occidentali |Stati Uniti orientali |
| Europa settentrionale |Europa occidentale |
| Asia sudorientale |Asia orientale |

È possibile visualizzare hello completo [elenco internazionali coppie qui](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilità delle funzionalità
Alcuni servizi o funzionalità delle VM sono disponibili solo in determinate aree geografiche, ad esempio alcuni tipi di archiviazione o dimensioni delle VM. Esistono inoltre alcuni servizi globali di Azure che non è necessitano tooselect una determinata area, ad esempio [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), o [DNS di Azure](../articles/dns/dns-overview.md). tooassist si nella progettazione dell'ambiente di applicazione, è possibile controllare hello [disponibilità dei servizi di Azure in ogni area](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Disponibilità dell'archiviazione
Informazioni sulle aree geografiche e aree di Azure diventa importante quando si considera hello le opzioni di replica di archiviazione disponibile. In base al tipo di archiviazione hello, sono disponibili opzioni di replica diversi.

**Azure Managed Disks**
* Archiviazione con ridondanza locale (LRS)
  * I dati tre volte all'interno di area hello in cui viene creato l'account di archiviazione vengono replicati.

**Dischi basati su account di archiviazione**
* Archiviazione con ridondanza locale (LRS)
  * I dati tre volte all'interno di area hello in cui viene creato l'account di archiviazione vengono replicati.
* Archiviazione con ridondanza della zona (ZRS)
  * I dati vengono replicati tre volte tra due strutture toothree, all'interno di una singola area o in due aree.
* Archiviazione con ridondanza geografica (GRS)
  * Consente di replicare i dati tooa area secondaria a centinaia di miglia di distanza area primaria hello.
* Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).
  * Replica l'area secondaria tooa di dati, come con archiviazione con ridondanza geografica, ma anche quindi fornisce i dati di toohello di accesso in sola lettura nel percorso secondario hello.

Hello nella tabella seguente fornisce una rapida panoramica delle differenze di hello tra tipi di replica di archiviazione hello:

| Strategia di replica | Archiviazione con ridondanza locale | ZRS | Archiviazione con ridondanza geografica | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| I dati vengono replicati in più strutture |No |Sì |Sì |Sì |
| Dati possono essere letti dalla posizione secondaria hello e dalla posizione primaria hello. |No |No |No |Sì |
| Numero di copie di dati mantenute in nodi distinti |3 |3 |6 |6 |

Per ulteriori informazioni, consultare [qui le opzioni di replica di Archiviazione di Azure](../articles/storage/common/storage-redundancy.md). Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).

### <a name="storage-costs"></a>Costi di archiviazione
I prezzi variano in base al tipo di archiviazione hello e disponibilità che si seleziona.

**Azure Managed Disks**
* Managed Disks Premium si basa su unità SSD, Managed Disks Standard invece su normali dischi a rotazione. Sia Premium e Standard di dischi gestiti vengono addebitati in base alle capacità di hello il provisioning per il disco di hello.

**Dischi non gestiti**
* Archiviazione Premium è supportato da allo stato solido unità (SSD Solid) e viene addebitato in base alle capacità di hello del disco hello.
* Archiviazione standard supportato da dischi rotante regolari e viene addebitato in base alle capacità di hello in uso e la disponibilità di archiviazione desiderato.
  * Per RA-GRS, è disponibile un costo aggiuntivo trasferimento dati-replica geografica per la larghezza di banda hello di replica che tooanother dati area di Azure.

Vedere [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) per informazioni sulle opzioni di disponibilità di hello diversi tipi di archiviazione e sui prezzi.

## <a name="availability-sets"></a>Set di disponibilità
Un set di disponibilità è un raggruppamento logico di macchine virtuali che Azure toounderstand consente la modalità di compilazione tooprovide per garantire ridondanza e disponibilità dell'applicazione. È consigliabile che i due o più macchine virtuali vengono create all'interno di un tooprovide di set di disponibilità per un disponibilità elevata hello applicazione e toomeet [pari al 99,95% SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Quando si utilizza una singola macchina virtuale [archiviazione Premium di Azure](../articles/storage/common/storage-premium-storage.md), hello SLA di Azure sono valide per gli eventi di manutenzione non pianificata. 

Un set di disponibilità è costituito da due gruppi aggiuntivi che proteggersi da errori hardware e consentono gli aggiornamenti toosafely essere applicato - (Fd) di domini di errore e domini (UD) di aggiornamento.

![Rappresentazione concettuale di hello aggiornamento dominio e errore di configurazione del dominio](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Ulteriori informazioni su come toomanage hello disponibilità [le macchine virtuali Linux](../articles/virtual-machines/linux/manage-availability.md) o [macchine virtuali Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domini di errore
Un dominio di errore è un gruppo logico di hardware sottostante che condividono una comune fonte di alimentazione e del commutatore di rete, rack tooa simili all'interno di un data center locale. Quando si creano le macchine virtuali all'interno di un set di disponibilità, hello piattaforma Azure distribuisce automaticamente le macchine virtuali in questi domini di errore. Questo approccio limita impatto hello di potenziali errori hardware fisico, interruzioni della rete o le interruzioni di alimentazione.

### <a name="update-domains"></a>Domini di aggiornamento
Un dominio di aggiornamento è un gruppo logico di hardware sottostante che può essere sottoposto a manutenzione o riavviato dopo hello contemporaneamente. Quando si creano le macchine virtuali all'interno di un set di disponibilità, hello piattaforma Azure vengono distribuite automaticamente le macchine virtuali in questi domini di aggiornamento. Questo approccio assicura che almeno un'istanza dell'applicazione rimane in esecuzione come hello piattaforma Azure viene sottoposta a manutenzione periodica. ordine di Hello di domini di aggiornamento in corso il riavvio potrebbe non passare in modo sequenziale durante la manutenzione pianificata, ma l'aggiornamento di un solo dominio è stato riavviato alla volta.

### <a name="managed-disk-fault-domains"></a>Domini di errore di Managed Disks
Le VM che usano [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md) sono allineate con i domini di errore dei dischi gestiti quando si usa un set di disponibilità gestito. L'allineamento in quanto assicura che tutti hello gestiti dischi collegato tooa VM sono all'interno di hello stesso dominio di errore di disco gestito. In un set di disponibilità gestito possono essere create solo VM con dischi gestiti. numero di Hello di domini di errore di disco gestito varia in base area - due o tre domini di errore di disco gestito per ogni area.

![Domini di errore dei dischi gestiti](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> numero di Hello di domini di errore per i set di disponibilità gestito varia in base a region - due o tre per ogni area. Hello nella tabella seguente mostra il numero di hello per area

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Passaggi successivi
È ora possibile avviare toouse questi disponibilità e ridondanza delle funzionalità toobuild l'ambiente di Azure. Per altre informazioni, vedere le [procedure consigliate per la disponibilità di Azure](../articles/best-practices-availability-checklist.md).

