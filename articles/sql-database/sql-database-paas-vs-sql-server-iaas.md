---
title: Visual Studio Database aaaSQL (PaaS). SQL Server nel cloud hello in macchine virtuali (IaaS) | Documenti Microsoft
description: 'Informazioni su quale opzione di SQL Server cloud adatta all''applicazione: Database SQL di Azure (PaaS) o SQL Server nel cloud hello in macchine virtuali di Azure.'
services: sql-database, virtual-machines
keywords: Cloud di SQL Server, SQL Server nel cloud hello, database PaaS, cloud di SQL Server, DBaaS
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Scegliere un'opzione di SQL Server cloud: database SQL di Azure (PaaS) o SQL Server in VM di Azure (IaaS)
Azure offre due opzioni per l'hosting dei carichi di lavoro di SQL Server in Microsoft Azure:

* [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/): cloud toohello native di database A SQL, noto anche come una piattaforma come un database del servizio (PaaS) o un database come servizio (DBaaS) che è ottimizzato per lo sviluppo di app di software come servizio (SaaS). Offre la compatibilità con la maggior parte delle funzionalità di SQL Server. Per altre informazioni su PaaS, vedere [Cos'è il modello PaaS?](https://azure.microsoft.com/overview/what-is-paas/)
* [SQL Server in macchine virtuali di Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server installati e ospitate nel cloud hello in Server macchine virtuali (VM) in esecuzione in Azure, noto anche come un'infrastruttura come servizio (IaaS).
  SQL Server in macchine virtuali di Azure è ottimizzato per la migrazione delle applicazioni SQL Server esistenti. Tutti hello versioni ed edizioni di SQL Server sono disponibili. Offre compatibilità 100% con SQL Server, consentendo di toohost tutti i database come transazioni tra database necessari e in esecuzione. oltre al pieno controllo su SQL Server e Windows.

Scopri ogni opzione inserisca nella piattaforma di dati Microsoft hello e ottenere Guida corrispondente hello opzione destra tooyour requisiti aziendali. Se è la priorità risparmi sui costi o amministrazione minimo avanti rispetto a altro, in questo articolo consente di decidere quale approccio offre rispetto ai requisiti di business hello che più importanti.

## <a name="microsofts-data-platform"></a>Piattaforma dati Microsoft
Uno dei hello prima cose toounderstand qualsiasi discussione di Azure e database di SQL Server locale è possibile utilizzare tutto. La piattaforma dei dati Microsoft si basa sulla tecnologia SQL Server e la rende disponibile nei computer fisici locali, negli ambienti cloud privati, negli ambienti cloud privati ospitati da terze parti e nel cloud pubblico. SQL Server in macchine virtuali di Azure consente toomeet univoco e diverse esigenze tramite una combinazione di on-premise e distribuzioni di cloud ospitato, mentre tramite hello stesso set di prodotti server, strumenti di sviluppo e competenze tra questi ambienti.

   ![Opzioni di SQL Server del cloud: database di SQL server su IaaS o SaaS SQL nel cloud hello.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Come illustrato nel diagramma hello, ogni offerta può essere caratterizzato da livello hello di amministrazione su infrastruttura hello (sull'asse delle X hello) e dal grado di hello di convenienza economica grazie al consolidamento a livello di database e l'automazione (asse Y hello).

Quando si progetta un'applicazione, sono disponibili per l'hosting di parte di SQL Server hello di un'applicazione hello quattro opzioni di base:

* SQL Server in computer fisici non virtualizzati
* SQL Server in macchine virtualizzate locali (cloud privato)
* SQL Server in una macchina virtuale di Azure (cloud Microsoft pubblico)
* Database SQL di Azure (cloud Microsoft pubblico)

In hello nelle sezioni che seguono, viene illustrato come SQL Server nel cloud pubblico Microsoft hello: Database SQL di Azure e SQL Server in macchine virtuali di Azure. L'articolo illustra anche i vantaggi aziendali più diffusi che permettono di determinare l'opzione ottimale per l'applicazione.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Informazioni dettagliate sul database SQL di Azure e su SQL Server in macchine virtuali di Azure
**Database SQL di Azure** è un relazionale database-as-a-service (DBaaS) ospitato nel cloud di Azure che può essere suddiviso in categorie di settore hello di hello *Software-as-a-Service (SaaS)* e *Platform-as-a-Service (PaaS)* . [database SQL](sql-database-technical-overview.md) si basa su hardware e software standardizzati appartenenti, ospitati e gestiti da Microsoft. Con il Database SQL, è possibile sviluppare direttamente nel servizio hello utilizzando le funzionalità incorporate. Quando si utilizza il Database SQL, di pagamento con opzioni tooscale verticale o per una maggiore potenza senza interruzioni.

**SQL Server in macchine virtuali di Azure (VM)** rientra nel settore hello *Infrastructure-as-a-Service (IaaS)* nonché toorun SQL Server in una macchina virtuale nel cloud hello. Simile tooSQL Database, è stato progettato su hardware standardizzato ed è di proprietà, ospitato e gestito da Microsoft. Quando si usa SQL Server in una macchina virtuale, è possibile scegliere una licenza di SQL Server con pagamento in base al consumo già inclusa in un'immagine di SQL Server oppure una licenza esistente. È inoltre possibile facilmente scala-su/giù e sospendere o riprendere hello macchina virtuale in base alle esigenze.

In generale, queste due opzioni SQL sono ottimizzate per scopi diversi:

* **Database SQL di Azure** è ottimizzato tooreduce i costi complessivi toohello minimo per il provisioning e la gestione di molti database. Riduce i costi di amministrazione in corso perché non è toomanage macchine virtuali, il sistema operativo o software del database. Gli aggiornamenti toomanage, non è a disponibilità elevata o [backup](sql-database-automated-backups.md). In generale, Database SQL di Azure può aumentare notevolmente il numero di hello di database gestito da un singolo IT o risorse di sviluppo.
* **SQL Server in esecuzione in macchine virtuali di Azure** è ottimizzato per la migrazione esistente tooAzure applicazioni o estendere locali esistenti cloud toohello applicazioni nelle distribuzioni ibride. Inoltre, è possibile utilizzare SQL Server in una macchina virtuale di toodevelop e testare applicazioni tradizionali di SQL Server. Con SQL Server in macchine virtuali di Azure, si dispone di diritti amministrativi completi hello su un'istanza dedicata di SQL Server e una macchina virtuale basata su cloud. È la soluzione ottimale quando un'organizzazione ha già le macchine virtuali IT le risorse disponibili toomaintain hello. Queste funzionalità consentono di toobuild tooaddress un sistema altamente personalizzati prestazioni specifici dell'applicazione e i requisiti di disponibilità.

Hello nella tabella seguente vengono riepilogate le caratteristiche principali di hello di Database SQL e SQL Server in macchine virtuali di Azure:

| **Ideale per:** | **Database SQL di Azure** | **SQL Server in una macchina virtuale di Azure** |
| --- | --- | --- |
|  |Nuove applicazioni progettate per il cloud con vincoli di tempo per lo sviluppo e il marketing. |Applicazioni esistenti che richiedono cloud toohello migrazione rapida con modifiche minime. Rapido sviluppo e test scenari quando non si desidera hardware del Server SQL toobuy locale non di produzione. |
|  | Team che necessitano di aggiornamento, il ripristino di emergenza e disponibilità elevata incorporata per il database di hello. |Team che possono configurare e gestire la disponibilità elevata, il ripristino di emergenza e l'applicazione di patch per SQL Server. Alcune funzionalità automatiche fornite semplifica notevolmente queste operazioni. | |
|  | Team che non si desidera che il sistema operativo sottostante di toomanage hello e le impostazioni di configurazione. |Casi in cui è necessario un ambiente personalizzato con diritti amministrativi completi. | |
|  | Database di backup too4 TB o database di grandi dimensioni che possono essere [partizionata orizzontalmente o verticalmente](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) utilizzando un modello di scalabilità orizzontale. |Istanze di SQL Server con backup too64 TB di spazio di archiviazione. istanza di Hello può supportare tutti i database in base alle esigenze. | |
|  | [Compilazione di applicazioni software come un servizio (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Migrazione e compilazione di applicazioni aziendali e ibride. | |
|  | | |
| **Risorse:** |Non si desidera tooemploy IT risorse per la configurazione e gestione di hello sottostante l'infrastruttura, ma desidera toofocus sul livello di applicazione hello. |Sono disponibili alcune risorse IT per la configurazione e la gestione. Alcune funzionalità automatiche fornite semplifica notevolmente queste operazioni. |
| **Costo totale di proprietà:** |Elimina i costi associati all'hardware e riduce i costi amministrativi. |Elimina i costi associati all'hardware. |
| **Continuità aziendale:** |Nella funzionalità di infrastruttura tolleranza di errore toobuilt-in aggiunta, Database SQL di Azure fornisce le funzionalità, ad esempio [backup automatici](sql-database-automated-backups.md), [momento ripristino](sql-database-recovery-using-backups.md#point-in-time-restore), [diripristinoalivellogeografico](sql-database-recovery-using-backups.md#geo-restore), e [replica geografica attiva](sql-database-geo-replication-overview.md) tooincrease continuità aziendale. Per altre informazioni, vedere [Panoramica: Continuità aziendale del cloud e ripristino di emergenza del database con database SQL](sql-database-business-continuity.md). |SQL Server in macchine virtuali di Azure consente di configurare una soluzione con disponibilità elevata e ripristino di emergenza per le esigenze specifiche del database. È quindi possibile avere un sistema altamente ottimizzato per la propria applicazione. È possibile testare ed eseguire i failover autonomamente quando necessario. Per altre informazioni, vedere [Disponibilità elevata e ripristino di emergenza per SQL Server nelle macchine virtuali di Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Cloud ibrido:** |L'applicazione locale può accedere ai dati nel database SQL di Azure. |Con SQL Server in macchine virtuali di Azure, possono avere le applicazioni eseguite in parte nel cloud di hello e in parte in locale. Ad esempio, è possibile estendere la rete locale e cloud toohello di dominio Active Directory tramite [rete virtuale di Azure](../virtual-network/virtual-networks-overview.md). È anche possibile archiviare i file di dati locali nell'archiviazione di Azure usando [File di dati di SQL Server in Azure](http://msdn.microsoft.com/library/dn385720.aspx). Per ulteriori informazioni, vedere [introduzione tooSQL Cloud ibride di Server 2014](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Supporta [la replica transazionale di SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) come dati tooreplicate sottoscrittore. |Supporta completamente [la replica transazionale di SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [gruppi di disponibilità AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services e il Log Shipping tooreplicate dati. Supporta pienamente anche i backup di SQL Server tradizionali. | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Motivazioni aziendali alla base della scelta del database SQL di Azure o di SQL Server nelle macchine virtuali di Azure
### <a name="cost"></a>Costi
Se si è un tipo di avvio è strapped contanti o un team di una società consolidata che opera in stretta limiti di budget, limitati finanziamento comporta spesso hello primario quando si decide come toohost dei database. In questa sezione informazioni sulla fatturazione hello e licenze nozioni di base in Azure con l'attributo due opzioni di database relazionale toothese: Database SQL e SQL Server in macchine virtuali di Azure. Inoltre, conoscere il calcolo del costo totale applicazione hello.

#### <a name="billing-and-licensing-basics"></a>Nozioni di base su fatturazione e licenze
**Database SQL** venduto toocustomers come servizio, non con una licenza.  [SQL Server in macchine virtuali di Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) viene venduto con una licenza inclusa, pagata al minuto. È anche possibile usare una licenza esistente, se disponibile.  

Attualmente, **Database SQL** è disponibile nei livelli di servizio diversi, ognuno dei quali vengono fatturate con tariffe orarie a un corrispettivo fisso, in base a hello servizio livello di prestazioni e si sceglie. Viene inoltre fatturato il traffico Internet in uscita a una [velocità di trasferimento dati](https://azure.microsoft.com/pricing/details/data-transfers/)normale. Hello Basic, Standard e Premium e il servizio Premium RS livelli sono progettato toodeliver prestazioni prevedibili con toomatch livelli di prestazioni più i requisiti dell'applicazione punta. È possibile modificare tra i livelli di servizio e toomatch livelli di prestazioni che esigenze di velocità effettiva di variabili dell'applicazione. Se il database dispone di molti utenti simultanei elevato transazionale toosupport di volume e delle esigenze, è consigliabile il livello di servizio Premium hello. Per informazioni più recenti di hello nei livelli di servizio corrente hello supportato, vedere [livelli di servizio di Azure SQL Database](sql-database-service-tiers.md). È inoltre possibile creare [pool elastici](sql-database-elastic-pool.md) tooshare risorse per le prestazioni tra le istanze di database.

Con **Database SQL**, hello database software viene automaticamente configurato, patch e aggiornato da Microsoft, che consente di ridurre i costi di amministrazione. Le funzionalità di [backup predefinite](sql-database-automated-backups.md) consentono anche di ottenere una significativa riduzione dei costi, specialmente per un numero elevato di database.

Con **SQL Server in macchine virtuali di Azure**, è possibile utilizzare uno qualsiasi dei hello fornita dalla piattaforma immagini di SQL Server (che include una licenza) o aggiornare la licenza di SQL Server. Hello tutte supportate le versioni di SQL Server (2008 R2, 2012, 2014, 2016) e le edizioni (Developer, Express, Web, Standard, Enterprise) sono disponibili. Inoltre, le versioni Bring-Your-proprietari-licenza (BYOL) delle immagini hello sono disponibili. Quando si utilizza hello che immagini fornito da Azure, costo operativo hello dipende dalle dimensioni della macchina virtuale hello ed hello edizione di SQL Server, si sceglie. Indipendentemente dalla dimensione della macchina virtuale o edizione di SQL Server, si paga al minuto costo sulle licenze di SQL Server e Windows Server, insieme a un costo di archiviazione di Azure per i dischi VM hello hello. opzione di fatturazione al minuto Hello consente toouse SQL Server per il tempo necessario senza acquistare inoltre licenze per SQL Server. Se si introducono proprio tooAzure di licenza di SQL Server, vengono addebitati i Server di Windows e solo i costi di archiviazione. Per altre informazioni sulla funzionalità Bring Your Own License, vedere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Il calcolo del costo totale dell'applicazione di hello
Quando si inizia a usare una piattaforma cloud, il costo di hello dell'esecuzione dell'applicazione include sviluppo hello e i costi di amministrazione, nonché i costi del servizio di piattaforma cloud pubblico hello.

Ecco hello calcolo del costo dettagliate per l'applicazione in esecuzione nel Database SQL e SQL Server in macchine virtuali di Azure:

**Quando si usa il database SQL di Azure:**

*Costo totale dell'applicazione = Costi amministrativi molto ridotti + costi di sviluppo del software + costi del servizio per il database SQL*

**Quando si usa SQL Server nelle macchine virtuali di Azure:**

*Costo totale dell'applicazione = Costi di sviluppo del software molto ridotti + costi amministrativi + costi di licenza per SQL Server e Windows Server + costi di archiviazione di Azure*

Per ulteriori informazioni sui prezzi, vedere hello seguenti risorse:

* [Database SQL - Prezzi](https://azure.microsoft.com/pricing/details/sql-database/)
* [Prezzi per le macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/) per [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) e per [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)
* [Calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> In SQL Server è presente un piccolo subset di funzionalità non applicabili o non disponibili con il database SQL. Per altre informazioni, vedere [SQL Database Features](sql-database-features.md) (Funzionalità del database SQL) e [SQL Database Transact-SQL information](sql-database-transact-sql-information.md) (Informazioni su Transact-SQL del database SQL). Se si sta spostando un cloud di toohello soluzione SQL Server esistente, vedere [la migrazione di un tooAzure di database di SQL Server Database SQL](sql-database-cloud-migrate.md). Quando si esegue la migrazione di un tooSQL di applicazioni SQL Server Database locale esistente, prendere in considerazione l'aggiornamento di hello applicazione tootake sfruttare funzionalità hello offerta di servizi cloud. Ad esempio, è consigliabile utilizzare [servizio App Web di Azure](https://azure.microsoft.com/services/app-service/web/) o [servizi Cloud di Azure](https://azure.microsoft.com/services/cloud-services/) toohost vantaggi economici il tooincrease di livello applicazione.
> 
> 

### <a name="administration"></a>Amministrazione
Per molte aziende, il servizio cloud tooa di hello decisione tootransition è molto sull'offload complessità di amministrazione perché è costo. Con **Database SQL**, Microsoft amministra l'hardware sottostante hello. Microsoft automaticamente tutti tooprovide elevata disponibilità dei dati di replica, configura e aggiornamento del software di database hello, gestisce il bilanciamento del carico e non il failover trasparente, se si verifica un errore server. È possibile continuare a tooadminister del database, ma non è più necessario motore di database toomanage hello, sistema operativo server o dell'hardware.  Esempi di elementi è possibile continuare tooadminister includono database e account di accesso, indice e ottimizzazione delle query e il controllo e sicurezza.

Con **SQL Server in macchine virtuali di Azure**, si dispone di controllo completo sul sistema operativo hello e configurazione dell'istanza di SQL Server. Con una macchina virtuale, è attivo tooyou toodecide quando l'aggiornamento tooupdate hello software di sistema e il database operativo e tooinstall software aggiuntivo, ad esempio software antivirus. Alcune funzionalità automatiche vengono forniti toodramatically semplificare la gestione delle patch, backup e la disponibilità elevata. Inoltre, è possibile controllare dimensioni hello di hello VM, hello numero di dischi e le relative configurazioni di archiviazione. Azure consente dimensioni hello toochange di una macchina virtuale in base alle esigenze. Per informazioni, vedere [Dimensioni delle macchine virtuali e del servizio cloud per Azure](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Contratto di servizio (SLA)
Per molti reparti IT rispettare gli obblighi relativi al tempo di attività di un contratto di servizio è della massima priorità. In questa sezione viene analizzato in ciò che si applica contratto di servizio database tooeach opzione di hosting.

Per i livelli di servizio Basic, Standard, Premium e Premium RS del **database SQL** Microsoft fornisce un contratto di servizio con disponibilità del 99,99%. Per informazioni più recenti di hello, vedere [Service Level Agreement](https://azure.microsoft.com/support/legal/sla/sql-database/). Per informazioni più recenti di hello sui livelli di servizio di Database SQL e piani di continuità aziendale hello supportato, vedere [livelli di servizio](sql-database-service-tiers.md).

Per **SQL Server in esecuzione in macchine virtuali di Azure**, Microsoft fornisce un contratto di servizio del 99,95% di disponibilità che include solo hello macchina virtuale. Questo contratto di servizio non comprende i processi di hello (ad esempio SQL Server) in esecuzione nella macchina virtuale hello e richiede almeno due istanze di macchina virtuale in un set di disponibilità ospitati. Per informazioni più recenti di hello, vedere hello [contratto di servizio VM](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Per database disponibilità elevata (HA) all'interno delle macchine virtuali, è necessario configurare una delle opzioni di disponibilità elevata hello è supportato in SQL Server, ad esempio [gruppi di disponibilità AlwaysOn](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Utilizzando l'opzione disponibilità elevata supportate non fornisce un contratto di servizio aggiuntiva, ma consente tooachieve > disponibilità del 99,99% database.

### <a name="market"></a>Tempo toomarket
**Database SQL** è soluzione hello per le applicazioni progettate cloud quando è fondamentale veloce time-to-market e la produttività degli sviluppatori. Con funzionalità di amministratore di database a livello di codice, è ideale per sviluppatori e progettisti cloud come riduce hello necessario per la gestione del sistema operativo sottostante hello e database. Ad esempio, è possibile utilizzare hello [API REST](http://msdn.microsoft.com/library/azure/dn505719.aspx) e [PowerShell Cmdlets](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate e gestire le operazioni amministrative per migliaia di database. Le funzionalità, ad esempio [pool elastici](sql-database-elastic-pool.md) consentono toofocus sul livello di applicazione hello e fornire più rapidamente il proprio mercato toohello soluzione.

**SQL Server in esecuzione in macchine virtuali di Azure** è perfetto se le applicazioni nuove o esistenti richiedono di database di grandi dimensioni, database correlati, o accedere alle funzionalità tooall in SQL Server o Windows. È anche una scelta ottimale quando si desidera toomigrate esistente locale tooAzure database e applicazioni come-è. Poiché non è necessario toochange hello presentazione, applicazione e i livelli di dati, si risparmiare tempo e denaro rielaborazione la soluzione esistente. In alternativa, è possibile concentrarsi sulla migrazione di tutti i tooAzure di soluzioni e in questo modo alcune ottimizzazioni delle prestazioni che possono essere richiesto da hello piattaforma Azure. Per altre informazioni, vedere [Procedure consigliate per le prestazioni di SQL Server nelle macchine virtuali di Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Riepilogo
Questo articolo ha illustrato il database SQL e SQL Server nelle macchine virtuali (VM) di Azure, nonché i vantaggi aziendali comuni che possono influire sulla decisione. di seguito Hello è un riepilogo dei suggerimenti per tooconsider è:

Scegliere il **database SQL di Azure** se:

* Si è creazione nuovo basato su cloud di applicazioni forniscono tootake sfruttare hello costo risparmio e ottimizzazione delle prestazioni che i servizi cloud. Questo approccio offre vantaggi hello di un servizio cloud completamente gestito consente inferiore iniziale time-to-market e può fornire a lungo termine ottimizzazione dei costi.
* Si desidera toohave Microsoft eseguire operazioni comuni di gestione dei database di e richiedono una maggiore disponibilità contratti di servizio per i database.

Scegliere **SQL Server nelle macchine virtuali di Azure** se:

* Si dispone di applicazioni locali che si desidera toomigrate o estendere toohello cloud, oppure se si desidera più di 4 TB toobuild le applicazioni aziendali. Questo approccio offre il vantaggio di hello di compatibilità SQL 100%, capacità del database di grandi dimensioni, il controllo completo su SQL Server e Windows e tunneling tooon sedi locali. oltre a ridurre al minimo i costi per lo sviluppo e la modifica delle applicazioni esistenti.
* Sono disponibili risorse IT esistenti ed è possibile essere il proprietario di operazioni relative ad applicazione di patch, backup e disponibilità elevata del database. Alcune funzionalità automatizzate semplificano notevolmente queste operazioni. 

## <a name="next-steps"></a>Passaggi successivi
* Vedere [il primo Database di SQL Azure](sql-database-get-started-portal.md) tooget avviato con il Database SQL.
* Vedere [Prezzi di Database SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* Vedere [il provisioning di una macchina virtuale di SQL Server in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget avviato con SQL Server in macchine virtuali di Azure.

