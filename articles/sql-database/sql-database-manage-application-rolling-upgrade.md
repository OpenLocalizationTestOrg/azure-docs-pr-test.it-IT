---
title: gli aggiornamenti dell'applicazione aaaRolling - Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toouse Database SQL di Azure-replica geografica toosupport aggiornamenti dell'applicazione cloud.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Gestione degli aggiornamenti in sequenza delle applicazioni cloud con la replica geografica attiva del database SQL
> [!NOTE]
> La [replica geografica attiva](sql-database-geo-replication-overview.md) è ora disponibile per tutti i database in tutti i livelli.
> 

Informazioni su come toouse [-replica geografica](sql-database-geo-replication-overview.md) in Database SQL tooenable gli aggiornamenti dell'applicazione cloud in sequenza. L'aggiornamento dovrebbe far parte della pianificazione e della progettazione della continuità aziendale perché è un'operazione che comporta interruzioni. In questo articolo che verranno esaminate due metodi diversi di orchestrazione hello processo di aggiornamento e discutere i vantaggi di hello e i vantaggi e svantaggi di ogni opzione. Ai fini di hello di questo articolo si utilizzerà una semplice applicazione costituita da un singolo database di sito web tooa connesso come relativo livello dati. L'obiettivo è tooupgrade versione 1 di hello applicazione tooversion 2 senza un impatto significativo sull'esperienza dell'utente finale di hello. 

Durante la valutazione delle opzioni di aggiornamento hello è opportuno considerare hello seguenti fattori:

* Impatto sulla disponibilità dell'applicazione durante gli aggiornamenti. Funzione applicazione hello quanto tempo può essere limitato o danneggiato.
* Possibilità tooroll nuovamente in caso di un aggiornamento non riuscito.
* Vulnerabilità di un'applicazione hello se si verifica un errore irreversibile non correlato durante l'aggiornamento di hello.
* Costo totale.  Ciò include un'ulteriore ridondanza e i costi incrementali dei componenti di hello temporanea utilizzati dal processo di aggiornamento hello. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Aggiornamento di applicazioni basate sui backup del database per il ripristino di emergenza
Se l'applicazione si basa sul backup automatici del database e utilizza ripristino a livello geografico per il ripristino di emergenza, è in genere distribuito tooa singola regione di Azure. In questo caso processo di aggiornamento hello implica la creazione di una distribuzione di backup di tutti i componenti coinvolti nell'aggiornamento hello. toominimize hello interruzioni è possibile utilizzare Azure Traffic Manager (WATM) con il profilo di failover hello.  Hello seguente diagramma illustra hello ambiente operativo toohello precedente aggiornamento. Hello endpoint <i>contoso 1.azurewebsites.net</i> rappresenta uno slot di produzione dell'applicazione hello necessarie toobe aggiornato. tooenable hello possibilità tooroll nuovamente hello l'aggiornamento, è necessario creare uno slot di fase con una copia di un'applicazione hello completamente sincronizzata. Hello passaggi seguenti sono un'applicazione hello tooprepare necessarie per l'aggiornamento di hello:

1. Creare uno slot di fase per l'aggiornamento di hello. toodo creare un database secondario (1) e distribuire un sito web identico in hello stessa area di Azure. Monitorare toosee secondario hello se hello seeding processo viene completato.
2. Creare un profilo di failover in Gestione traffico di Azure con <i>contoso-1.azurewebsites.net</i> come endpoint online e <i>contoso-2.azurewebsites.net</i> come endpoint offline. 

> [!NOTE]
> Passaggi di preparazione hello nota non avrà impatto sulle applicazioni hello nello slot di produzione hello e funzionare in modalità di accesso completo.
>  

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Dopo aver completati i passaggi di preparazione hello applicazione hello è pronta per l'aggiornamento effettivo hello. Hello seguente diagramma illustra i passaggi di hello coinvolti nel processo di aggiornamento hello. 

1. Impostare i database primario hello in hello slot tooread sola modalità di produzione (3). Ciò garantisce che hello istanza di produzione di un'applicazione hello (V1) rimarrà sola lettura durante l'aggiornamento di hello, impedendo così divergenze di dati hello tra hello V1 e V2 le istanze del database.  
2. Disconnettere i database secondari di hello utilizzando la modalità di terminazione pianificata hello (4). Creerà una copia indipendente completamente sincronizzata del database primario hello. Questo database verrà aggiornato.
3. Attivare la modalità di scrittura di tooread hello database primario ed eseguire script di aggiornamento hello nello slot di fase hello (5).     

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Aggiornamento hello completato, è possibile l'applicazione di hello copia tooswitch pronto hello agli utenti finali toohello gestione temporanea. Ora diventerà lo slot di produzione hello di un'applicazione hello.  Questo implica alcuni passaggi aggiuntivi, come illustrato nel seguente diagramma hello.

1. Opzione endpoint online hello nel profilo di Traffic Manager di AZURE hello troppo<i>contoso 2.azurewebsites.net</i>, la versione V2 toohello punti del sito web di hello (6). Ora diventa uno slot di produzione hello con hello V2 applicazione e il traffico degli utenti finali di hello è tooit diretto.  
2. Se non è più necessario componenti dell'applicazione hello V1 in modo è possibile rimuoverli (7).   

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Se il processo di aggiornamento hello ha esito negativo, ad esempio a causa di errore tooan in uno script di aggiornamento hello slot fase hello da considerare compromessi. tooroll di eseguire il backup hello toohello pre-aggiornamento lo stato dell'applicazione è sufficiente ripristinare un'applicazione hello Access toofull slot produzione di hello. passaggi Hello vengono visualizzati nel diagramma successivo hello.    

1. Impostare la modalità di scrittura di tooread hello database copia (8). Verranno ripristinati hello completo V1 funzionalmente nello slot di produzione hello.
2. Eseguire l'analisi delle cause principali hello e rimuovere componenti hello compromesso nello slot di fase hello (9). 

A questo punto l'applicazione hello è completamente funzionale e passaggi di aggiornamento hello possono essere ripetuti.

> [!NOTE]
> Hello rollback non richiede modifiche nel profilo di Traffic Manager di AZURE come già punti troppo<i>contoso 1.azurewebsites.net</i> come hello endpoint attivo.
> 
> 

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

chiave Hello **vantaggio** di questa opzione è che è possibile aggiornare un'applicazione in una singola area usando un set di semplici passaggi. costo Hello dell'aggiornamento hello è relativamente bassa. Hello principale **compromesso** è che se si verifica un errore irreversibile durante lo stato di pre-aggiornamento hello hello aggiornamento ripristino toohello comporterà la distribuzione dell'applicazione hello in un'area diversa e il ripristino database di hello da backup con ripristino a livello geografico. Questo processo causa tempi di inattività significativi.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Aggiornamento di applicazioni basate sulla replica geografica del database per il ripristino di emergenza
Se l'applicazione usa la replica geografica per la continuità aziendale, è distribuito tooat almeno due aree diverse con una distribuzione attiva nell'area primaria e una distribuzione di standby nell'area di Backup. Inoltre fattori toohello indicato in precedenza, processo di aggiornamento hello deve garantire che:

* un'applicazione Hello rimane protetta da errori irreversibili in qualsiasi momento durante il processo di aggiornamento hello
* componenti di archiviazione con ridondanza geografica Hello di un'applicazione hello vengono aggiornati in parallelo con i componenti active hello

tooachieve tali obiettivi è possibile utilizzare Azure Traffic Manager (WATM) tramite failover hello profilo con uno attivo e tre gli endpoint di backup.  Hello seguente diagramma illustra hello ambiente operativo toohello precedente aggiornamento. siti web di Hello <i>contoso 1.azurewebsites.net</i> e <i>contoso dr.azurewebsites.net</i> rappresentano uno slot di produzione dell'applicazione hello con ridondanza geografica completa. tooenable hello possibilità tooroll nuovamente hello l'aggiornamento, è necessario creare uno slot di fase con una copia di un'applicazione hello completamente sincronizzata. Poiché è necessario tooensure che un'applicazione hello è possibile ripristinare rapidamente nel caso in cui si verifica un errore irreversibile durante il processo di aggiornamento hello, slot fase hello deve toobe con ridondanza geografica anche. Hello passaggi seguenti sono un'applicazione hello tooprepare necessarie per l'aggiornamento di hello:

1. Creare uno slot di fase per l'aggiornamento di hello. toodo creare un database secondario (1) e distribuire una copia identica del sito web hello hello stessa area di Azure. Monitorare toosee secondario hello se hello seeding processo viene completato.
2. Creare un database secondario con ridondanza geografica nello slot di fase hello mediante la replica geografica hello database secondario toohello backup area (è chiamata "concatenate replica geografica"). Se il processo di seeding hello è completato (3), monitorare toosee secondario backup hello.
3. Creare una copia di standby del sito web hello area backup hello e collegarlo toohello con ridondanza geografica secondario (4).  
4. Aggiungere altri endpoint hello <i>contoso 2.azurewebsites.net</i> e <i>contoso 3.azurewebsites.net</i> toohello un profilo di failover in Traffic Manager di AZURE come endpoint offline (5). 

> [!NOTE]
> Passaggi di preparazione hello nota non avrà impatto sulle applicazioni hello nello slot di produzione hello e funzionare in modalità di accesso completo.
> 
> 

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Dopo aver completati i passaggi di preparazione hello, slot fase hello è pronto per l'aggiornamento di hello. Hello seguente diagramma illustra i passaggi di aggiornamento hello.

1. Impostare i database primario hello in hello slot tooread sola modalità di produzione (6). Ciò garantisce che hello istanza di produzione di un'applicazione hello (V1) rimarrà sola lettura durante l'aggiornamento di hello, impedendo così divergenze di dati hello tra hello V1 e V2 le istanze del database.  
2. Disconnettere i database secondari hello in hello stessa regione utilizzando hello in modalità di terminazione (7). Creerà una copia indipendente completamente sincronizzata del database primario hello, che diventerà automaticamente un database primario dopo la terminazione hello. Questo database verrà aggiornato.
3. Attivare database primario hello in modalità di scrittura di tooread di hello fase slot ed eseguire script di aggiornamento hello (8).    

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Se l'aggiornamento di hello è stata completata correttamente, è possibile tooswitch pronto hello agli utenti finali toohello V2 versione di hello applicazione. Hello seguente diagramma illustra hello passaggi della procedura.

1. Opzione endpoint attivo hello nel profilo di Traffic Manager di AZURE hello troppo<i>contoso 2.azurewebsites.net</i>, che ora punta toohello V2 versione del sito web di hello (9). Ora diventa uno slot di produzione con hello V2 applicazione e il traffico dell'utente finale è tooit diretto. 
2. Se non è più necessaria un'applicazione hello V1 in modo è possibile rimuoverlo (10 e 11).  

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Se il processo di aggiornamento hello ha esito negativo, ad esempio a causa di errore tooan in uno script di aggiornamento hello slot fase hello da considerare compromessi. tooroll di eseguire il backup hello toohello pre-aggiornamento lo stato dell'applicazione è sufficiente ripristinare un'applicazione hello toousing nello slot di produzione hello con accesso completo. passaggi Hello vengono visualizzati nel diagramma successivo hello.    

1. Copia del database primario set hello in modalità di scrittura di tooread slot produzione hello (12). Verranno ripristinati hello completo V1 funzionalmente nello slot di produzione hello.
2. Eseguire l'analisi delle cause principali hello e rimuovere componenti hello compromesso nello slot di fase hello (13 e 14). 

A questo punto l'applicazione hello è completamente funzionale e passaggi di aggiornamento hello possono essere ripetuti.

> [!NOTE]
> Hello rollback non richiede modifiche nel profilo di Traffic Manager di AZURE come già punti troppo <i>contoso 1.azurewebsites.net</i> come hello endpoint attivo.
> 
> 

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

chiave Hello **vantaggio** di questa opzione è che è possibile aggiornare un'applicazione hello sia la copia in parallelo con ridondanza geografica senza compromettere la continuità aziendale durante l'aggiornamento di hello. Hello principale **compromesso** è che richiede ridondanza double di ciascun componente dell'applicazione e pertanto comporta un costo superiore. e un flusso di lavoro più complesso. 

## <a name="summary"></a>Riepilogo
diversi metodi di aggiornamento Hello due descritti nell'articolo hello complessità e hello dollaro costo, ma entrambi concentrarsi su riducendo al minimo il tempo di hello quando degli utenti finali di hello è limitate solo tooread operazioni. Tale intervallo di tempo direttamente è definito per la durata dello script di aggiornamento hello hello. Non dipende dalla dimensione del database hello, hello del livello servizio è stata selezionata, la configurazione del sito web hello e altri fattori che non è possibile controllare facilmente. In questo modo tutti i passaggi di preparazione hello vengono disaccoppiati da operazioni di aggiornamento hello e possono essere eseguiti senza alcun impatto sull'applicazione di produzione hello. l'efficienza di Hello dello script di aggiornamento hello è fattore essenziale per hello che determina l'esperienza dell'utente finale di hello durante gli aggiornamenti. Hello modo migliore per migliorare si concentrare le attività in esecuzione dello script di aggiornamento hello più efficiente possibile.  

## <a name="next-steps"></a>Passaggi successivi
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md).
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database da backup automatizzati](sql-database-recovery-using-backups.md).
* toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md).


