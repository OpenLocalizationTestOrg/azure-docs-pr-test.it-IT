---
title: domande frequenti su Database SQL aaaAzure | Documenti Microsoft
description: I clienti domande toocommon risposte chiedere database cloud e di Database SQL di Azure, di sistema di gestione di Microsoft database relazionali (RDBMS) e di database come servizio nel cloud hello.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>Domande frequenti sul database SQL

## <a name="what-is-hello-current-version-of-sql-database"></a>Qual è la versione corrente di hello del Database SQL?
versione corrente di Hello del Database SQL è V12. La versione V11 è stata ritirata.

## <a name="what-is-hello-sla-for-sql-database"></a>Che cos'è hello contratto di servizio per il Database SQL?
Microsoft garantisce almeno 99,99% dei clienti ora hello avrà la connettività tra loro Basic singola o elastica, Standard o Premium Database SQL di Microsoft Azure e il gateway Internet. Per altre informazioni, vedere [Contratto di servizio](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Come reimpostare la password di hello per l'amministrazione server hello?
In hello [portale di Azure](https://portal.azure.com) fare clic su **istanze di SQL Server**, selezionare server hello hello elenco e quindi fare clic su **Reimposta Password**.

## <a name="how-do-i-manage-databases-and-logins"></a>Come si gestiscono database e accessi?
Vedere [Gestione di database e accessi](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Come effettuare che solo gli indirizzi IP autorizzati siano consentite tooaccess un server?
Vedere [Procedura: configurare le impostazioni del firewall su Database SQL mediante il portale di Azure](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>La modalità utilizzo hello del Database SQL vengono visualizzati nella fattura?
Gli effetti di Database SQL in una tariffa oraria stimabile dipendono sia il livello di servizio hello + prestazioni livello singoli database o di Edtu per pool elastico. L'utilizzo effettivo è calcolato e ripartito su base oraria. È quindi possibile che nella fattura siano indicate frazioni di un'ora. Ad esempio, se un database esiste per 12 ore in un mese, nella fattura viene indicato l'utilizzo di 0,5 giorni. Inoltre, i livelli di servizio + livello di prestazioni e di Edtu per ogni pool vengono interrotte out in hello bill toomake il numero di hello toosee più semplice di giorni di database è usato per ognuna in un mese.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>Cosa succede se un database singolo è attivo per meno di un'ora o utilizza un maggiore livello di servizio per meno di un'ora?
Verrà addebitato per ogni ora che presente un database utilizzando hello più alto livello di servizio + prestazioni livello applicati durante quell'ora, indipendentemente dall'utilizzo o se il database di hello era attivo per meno di un'ora. Ad esempio, se si crea un database singolo che viene eliminato cinque minuti dopo, in fattura viene riportato l'addebito relativo a un'ora di database. 

esempi

* Se si crea un database di base e quindi immediatamente l'aggiornamento tooStandard S1, viene addebitato con frequenza S1 Standard hello per hello prima ora.
* Se si aggiorna un database da base tooPremium alle 10:00 e l'aggiornamento viene completato alle ore 01:35 in hello giorno, viene effettuato alla tariffa Premium hello a partire da 01:00. 
* Se si esegue il downgrade di un database da Premium tooBasic ore 11:00. al completamento alle ore 2:15, quindi database hello viene addebitato con frequenza Premium hello fino a 3:00 p.m., dopo il quale vengono addebitati in base alle tariffe base hello.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Come viene indicato l'utilizzo del pool elastico nella fattura e cosa accade quando si modificano le eDTU per ciascun pool?
Pool elastico spese Mostra nella fattura come Dtu elastico (Edtu) nel visualizzate nella finestra di Edtu per pool in incrementi di hello [hello pagina dei prezzi](https://azure.microsoft.com/pricing/details/sql-database/). Non è previsto alcun costo per database per i pool elastici. Verrà addebitato per ogni ora che un pool esiste nella finestra di eDTU massimo hello, indipendentemente dall'utilizzo o se il pool di hello era attivo per meno di un'ora. 

esempi

* Se si crea un pool elastico Standard con Edtu di 200 ore 11:18, aggiunta di cinque database toohello pool, vengono addebitati i 200 Edtu per ora intera hello e inizio alle ore 11. attraverso il resto hello del giorno hello.
* In 2 giorni, ore 5:05, Database 1 inizia l'utilizzo di 50 Edtu e resta bloccato tramite giorno hello. Il Database 2-5 fluttua tra le 0 e le 80 DTU. Durante il giorno di hello, aggiungere cinque altri database che utilizzano variabili Edtu per tutto il giorno hello. Il giorno 2 viene fatturato interamente a 200 DTU. 
* Il terzo giorno alle 05:00 vengono aggiunti altri 15 database. Utilizzo del database aumenta in punto di toohello hello giorno in cui si decide di tooincrease Edtu per pool hello da 200 too400 alle ore 8:05. Le spese a livello di eDTU hello 200 attive fino alle 20.00 e aumenta too400 Edtu per hello rimanenti quattro ore. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Informazioni su prezzi e fatturazione dei pool elastici
Pool elastici vengono fatturati per hello seguenti caratteristiche:

* Un pool elastico viene fatturato al momento della relativa creazione, anche quando non sono disponibili database nel pool di hello.
* Un pool elastico viene fatturato su base oraria. Questo è hello stessa frequenza per i livelli di prestazioni dei singoli database di controllo.
* Se un pool elastico è ridimensionato tooa nuovo numero di Edtu, quindi pool hello viene fatturato non in base toohello nuova quantità di Edtu fino al completamento dell'operazione di ridimensionamento hello. Di seguito, hello stesso schema come modificare il livello di prestazioni hello di singoli database.
* prezzo di Hello di un pool elastico si basa sul numero di hello di Edtu del pool di hello. prezzo Hello di un pool elastico è indipendente dal numero hello e l'utilizzo di database elastico di hello in esso contenuti.
* Il prezzo di base viene calcolato da (numero di eDTU del pool) x (prezzo unitario per eDTU).

Hello unità eDTU per un pool elastico è più alto hello DTU prezzo unitario un singolo database nel hello stesso livello di servizio. Per ulteriori informazioni, vedere [Database SQL Prezzi](https://azure.microsoft.com/pricing/details/sql-database/). 

livelli di servizio e di Edtu di hello toounderstand, vedere [opzioni del Database SQL e le prestazioni](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>In che modo hello utilizza di replica geografica attiva in un pool elastico visualizzati nella fattura?
A differenza dei database singoli, l'uso della [replica geografica attiva](sql-database-geo-replication-overview.md) con i database elastici non ha un impatto diretto sulla fatturazione.  Vengono addebitati solo i Edtu hello effettuato il provisioning per ognuno dei pool di hello (pool primario e secondario pool)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>In che modo hello utilizza di hello impatto sulle funzionalità di controllo fattura?
Il controllo viene compilato in hello servizio Database SQL senza aggiuntivi costo senza che sia disponibile tooBasic, Standard, Premium e RS Premium database. Tuttavia, toostore hello i log di controllo, hello il controllo viene utilizzato un account di archiviazione di Azure e tariffe per tabelle e code di archiviazione di Azure sono applicabili in base alle dimensioni di hello del Registro di controllo.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Ricerca di livello e le prestazioni del servizio destra hello per singoli database e i pool elastici
Esistono alcuni tooyou disponibili di strumenti. 

* Per i database locali, utilizzare hello [advisor ridimensionamento DTU](http://dtucalculator.azurewebsites.net/) toorecommend hello Dtu necessarie e i database e valutare più database per il pool elastico.
* Se un database singolo potrebbe trarre vantaggio dal far parte di un pool, il motore intelligente di Azure consiglia un pool elastico se rileva un modello di utilizzo cronologico che garantisca tale vantaggio. Vedere [Monitor e gestire un pool elastico con hello Azure portal](sql-database-elastic-pool-manage-portal.md). Per informazioni dettagliate su come toodo hello matematiche manualmente, vedere [prezzo e considerazioni sulle prestazioni per un pool elastico](sql-database-elastic-pool.md)
* toosee se è necessario un singolo database toodial verso l'alto o verso il basso, vedere [linee guida sulle prestazioni per i singoli database](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>La frequenza con cui è possibile modificare livello hello servizio livello o di prestazioni di un singolo database?
È possibile modificare il livello di servizio hello (tra Basic, Standard, Premium e Premium RS) o hello ogni volta che desidera il livello di prestazioni all'interno di un livello di servizio (ad esempio S1 tooS2). Per i database di versioni precedenti, è possibile modificare a livello di livello o di prestazioni di servizio hello un totale di quattro volte in un periodo di 24 ore.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>La frequenza con cui è possibile regolare hello Edtu per pool?
Numero di volte desiderato.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>Quanto tempo toochange hello servizio livello o prestazioni livello di un singolo database o spostare un database da e verso un pool elastico.
Modifica il livello di servizio hello di un database e lo spostamento e la disconnessione di un pool richiede toobe database hello copiati nella piattaforma hello come un'operazione in background. Modifica livello di servizio hello può richiedere da alcuni minuti tooseveral ore a seconda delle dimensioni hello hello database. In entrambi i casi, i database hello rimangano online e disponibili durante lo spostamento di hello. Per informazioni dettagliate sulla modifica dei singoli database, vedere [livello di servizio hello modifica di un database](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Quando è meglio usare un database singolo e quando invece è meglio usare database elastici?
In generale, i pool elastici sono progettati per un [modello di applicazione tipico di software-as-a-service (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md), in cui è presente un solo database per client o tenant. Acquisto di singoli database e di overprovisioning toomeet hello variabile e di picco richiesta per ogni database spesso non è economicamente efficiente. Con pool, gestire le prestazioni di collettivo hello del pool di hello e database hello applicare la scalabilità verticale automaticamente. Il motore intelligente di Azure consiglia un pool per i database se garantito da un modello di utilizzo. Per informazioni, vedere le [linee guida sui pool elastici](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>Che cosa significa toohave too200% dello spazio di archiviazione massime del database sottoposto a provisioning per l'archiviazione di backup?
Archiviazione di backup è associato con i backup automatizzati del database che vengono utilizzati per archiviazione di hello [punto-In--ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) e [ripristino a livello geografico](sql-database-recovery-using-backups.md#geo-restore). Database SQL di Microsoft Azure fornisce too200% dello spazio di archiviazione massime del database sottoposto a provisioning dell'archiviazione di backup senza alcun costo aggiuntivo. Ad esempio, se si usa un'istanza di database Standard con una dimensione di database con provisioning pari a 250 GB, sono disponibili 500 GB di archiviazione di backup senza costi aggiuntivi. Se il database supera hello fornita l'archiviazione di backup, è possibile scegliere di periodo di memorizzazione hello tooreduce contattando il supporto tecnico di Azure o pagare per l'archiviazione extra backup hello fatturato alla tariffa di archiviazione accesso in lettura geograficamente ridondante (RA-GRS) standard. Per altre informazioni sui costi per il servizio RA-GRS, vedere Dettagli prezzi di archiviazione.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Si intende passare da Web/Business toohello nuovi livelli di servizio, cosa devo tooknow?
I database SQL di Azure Web e Business sono stati ritirati i livelli Basic, Standard, Premium, RS Premium ed elastica Hello sostituiscono hello ritiro database Web e Business. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>Che cos'è un ritardo di replica previsto quando la replica geografica un database tra due aree all'interno di hello stessa area geografica di Azure?
Supporto attualmente un RPO di cinque secondi e il ritardo di replica hello è stato minore rispetto a quello quando secondarie geografica hello sono ospitata in Azure consigliato area abbinata hello e in hello stesso livello di servizio.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>Che cos'è un ritardo di replica previsto quando geografica secondario viene creato nel hello stessa area come database primario hello?
In base ai dati empirici, non c'è troppa differenza tra all'interno dell'area e di ritardo di replica tra area quando viene utilizzato hello che Azure consigliato area abbinata. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>Se si verifica un errore di rete tra due aree, come la logica di riesecuzione hello funziona quando è impostata la replica geografica?
Se si verifica una disconnessione, abbiamo ripetere toore ogni 10 secondi-stabilire connessioni.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>Che cosa può fare tooguarantee che viene replicata una modifica importante sul database primario hello
Hello geo-secondario è una replica asincrona ed effettuato un tentativo non tookeep nella sincronizzazione completa con hello primario. Ma si fornisce un metodo tooforce tooensure hello replica della sincronizzazione le modifiche importanti (ad esempio, gli aggiornamenti della password). La sincronizzazione forzata influisce sulle prestazioni, perché Blocca thread chiamante hello fino a quando non vengono replicate tutte le transazioni completate. Per informazioni dettagliate, vedere [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>Quali strumenti sono disponibili toomonitor intervallo di replica hello tra database primario hello e geografica secondario?
È necessario esporre hello ritardo di replica in tempo reale tra database primario hello e geo-secondario tramite una DMV. Per informazioni dettagliate, vedere [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>un altro server di database tooa in hello toomove stessa sottoscrizione
* In hello [portale di Azure](https://portal.azure.com), fare clic su **database SQL**, selezionare un database dall'elenco hello e quindi fare clic su **copia**. Per altre informazioni, vedere [Copiare un database SQL di Azure](sql-database-copy.md) .

## <a name="toomove-a-database-between-subscriptions"></a>toomove un database tra le sottoscrizioni
* In hello [portale di Azure](https://portal.azure.com), fare clic su **istanze di SQL Server** e quindi selezionare hello server che ospita il database dall'elenco di hello. Fare clic su **spostare**, quindi selezionare hello risorse toomove e toomove sottoscrizione hello per.
