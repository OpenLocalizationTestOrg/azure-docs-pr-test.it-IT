---
title: un database SQL di Azure in un'applicazione multi-tenant aaaRestore | Documenti Microsoft
description: Informazioni su come toorestore un singolo tenant SQL database dopo l'eliminazione accidentale di dati
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Ripristinare un database SQL a tenant Wingtip SaaS

app SaaS Wingtip Hello viene compilato mediante un modello di database per tenant, in cui ogni tenant ha il proprio database. Uno dei vantaggi di hello di questo modello è che è facile toorestore dati di un singolo tenant in isolamento senza alcun impatto sugli altri tenant.

Questa esercitazione illustra due modelli di ripristino dei dati:

> [!div class="checklist"]

> * Ripristinare un database in un database parallelo (side-by-side)
> * Ripristinare un database sul posto


|||
|:--|:--|
| **Ripristinare tenant tooa precedente punto nel tempo, in parallelo di un database** | Questo modello può essere utilizzato dal tenant hello per la revisione, il controllo e la conformità, database originale di hello e così via rimane invariato e non in linea. |
| **Ripristinare un tenant sul posto** | Questo modello è toorecover in genere utilizzato un punto di tenant tooa precedente nel tempo e dopo che un tenant elimina accidentalmente dati. database originale Hello viene portato offline e sostituito con il database ripristinato hello. |
|||

toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Modello di ripristino di introduzione toohello SaaS tenant

Per tenant hello modello di ripristino, sono disponibili due modelli semplice per il ripristino dei dati di un singolo tenant. Poiché i database dei tenant sono isolati tra loro, il ripristino di un tenant non ha alcun impatto sui dati di qualsiasi altro tenant.

Nel primo modello hello, i dati vengono ripristinati in un nuovo database. tenant Hello del database di access toothis insieme ai relativi dati di produzione viene quindi specificato. Questo modello consente un tenant admin tooreview hello ripristino dei dati e utilizzarla potenzialmente tooselectively sovrascrivere i valori di dati corrente. È attivo toohello SaaS app progettazione toodetermine come sofisticate hello devono essere le opzioni di ripristino dei dati. Semplicemente tooreview in grado di dati in hello stato in un determinato punto nel tempo potrebbe essere tutto ciò che serve in alcuni scenari. Se viene utilizzato il database di hello [-replica geografica](sql-database-geo-replication-overview.md), è consigliabile copiare i dati necessario hello dalla copia hello ripristinato nel database originale hello. Se si sostituisce database originale hello con database hello ripristinato, è necessario tooreconfigure e risincronizzare la replica geografica.

Nel modello secondo hello, che presuppone tenant hello ha subito una perdita o danneggiamento dei dati, viene ripristinato il database di produzione del tenant hello tooa punto precedente nel tempo. Ripristino hello nel modello sul posto, tenant hello viene portato offline per un breve periodo di tempo durante il ripristino e portato nuovamente online database hello. Hello database originale viene eliminato, ma possono essere ripristinati da ancora se è necessario tooan indietro toogo anche precedente punto nel tempo. Una variante di questo modello è stato possibile rinominare database hello anziché eliminarlo, anche se il database hello ridenominazione non offre alcun vantaggio in termini di sicurezza dei dati aggiuntiva.

## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Simulare un tenant che elimina accidentalmente i dati

toodemonstrate questi scenari di ripristino, è necessario troppo*accidentalmente* eliminare alcuni dati in uno dei database tenant hello. Mentre è possibile eliminare qualsiasi record, hello successivo passaggio Imposta hello demo toonot essere bloccato da violazioni di integrità referenziale. Aggiunge anche alcuni dati di acquisto di ticket è possibile utilizzare più avanti in hello *esercitazioni Wingtip SaaS Analitica*.

Eseguire hello ticket generatore script e creare dati aggiuntivi. i ticket per ogni evento ultimo tenant generatore ticket Hello non intenzionalmente acquistato.

1. Apri... \\Moduli learning\\utilità\\*Demo TicketGenerator.ps1* in hello *PowerShell ISE*
1. Premere **F5** toorun hello script e generare i clienti e i dati di vendita del ticket.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Aprire hello app tooreview hello correnti eventi

1. Aprire hello *Hub eventi* (http://events.wtp.&lt; utente&gt;. trafficmanager.net) e fare clic su **Contoso insieme Hall**:

   ![Hub eventi](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Scorrere l'elenco di hello degli eventi e prendere nota dell'ultimo evento hello nell'elenco di hello:

   ![ultimo evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Eseguire hello demo scenario tooaccidentally delete hello ultimo evento

1. Apri... \\Moduli learning\\la continuità aziendale e ripristino di emergenza\\RestoreTenant\\*Demo RestoreTenant.ps1* in hello *PowerShell ISE*, e hello set il valore seguente:
   * **$DemoScenario** = **1**, impostare troppo**1** -Elimina gli eventi senza vendite ticket.
1. Premere **F5** toorun hello script ed eliminare l'ultimo evento hello. Dovrebbe essere conferma messaggio simili toohello di seguito:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. verrà visualizzata la pagina eventi di Hello Contoso. Scorrere verso il basso e verificare l'evento di hello è più presente. Se evento hello è ancora nell'elenco di hello, fare clic su Aggiorna e verificare che venga rimossa.

   ![ultimo evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Ripristinare un database tenant in parallelo con i database di produzione hello

Questo esercizio Ripristina punto tooa database Contoso insieme Hall di hello prima hello evento è stato eliminato. Dopo l'eliminazione di eventi hello nei passaggi precedenti hello, toorecover che desideri visualizzare dati hello eliminato. È necessario toorestore il database di produzione con record hello eliminato, ma è necessario toorecover hello precedente database tooaccess hello dati precedenti per altri motivi aziendali.

 Hello *ripristino TenantInParallel.ps1* script crea un tenant parallelo, database e una voce di catalogo parallelo entrambi a denominata *ContosoConcertHall\_precedente*. Questo modello di ripristino è più adatto per il ripristino da una perdita di dati minore o per la conformità e il controllo di scenari di ripristino. È inoltre hello approccio consigliato quando si utilizza [-replica geografica](sql-database-geo-replication-overview.md).

1. Hello completo [simulare un utente di eliminazione accidentale di dati](#simulate-a-tenant-accidentally-deleting-data) sezione.
1. Apri... \\Moduli learning\\la continuità aziendale e ripristino di emergenza\\RestoreTenant\\_Demo RestoreTenant.ps1_ in hello *PowerShell ISE*.
1. Impostare **$DemoScenario** = **2**, impostare questa proprietà troppo**2** troppo*ripristino tenant in parallelo*.
1. Premere **F5** script hello toorun.

lo script di Hello ripristinate hello tenant database (database paralleli tooa) tooa punto nel tempo prima dell'eliminazione evento hello nella sezione precedente hello. Viene creato un secondo database e rimuove i metadati del catalogo esistente nel database esiste e aggiunge catalogo toohello hello in hello *ContosoConcertHall\_precedente* voce.

script dimostrativo Hello verrà visualizzata la pagina eventi hello nel browser. Nota dall'URL hello: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` che questa è la visualizzazione di dati dal database ripristinato hello in *old* viene aggiunto il nome toohello.

Eventi di hello scorrimento elencati in hello browser tooconfirm hello di eliminazione nella sezione precedente hello dell'evento è stato ripristinato.

Si noti che espone tenant hello ripristinato un tenant aggiuntivi, con i ticket toobrowse propria app eventi, è improbabile che toobe come è necessario fornire che un dati toorestored accesso del tenant, ma funge da tooeasily illustrato il criterio di ripristino hello.

In realtà, è probabile che venga conservato solo il database ripristinato per un periodo definito. È possibile eliminare voce tenant hello ripristinato dopo aver dal chiamante hello *Remove RestoredTenant.ps1* script.

1. Impostare **$DemoScenario** troppo**4** tooselect hello *remove ripristinato tenant* scenario.
1. **Eseguire** **tramite** **F5**
1. Hello *ContosoConcertHall\_precedente* voce ora è stata eliminata dal catalogo hello. Vado avanti e chiudere pagina eventi hello per questo tenant nel browser.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Ripristinare un tenant sul posto, sostituendo i database tenant esistente hello

Questo esercizio Ripristina punto tooa tenant Contoso insieme Hall di hello prima hello evento è stato eliminato. Hello *ripristino TenantInPlace* script ripristinato hello corrente tenant database tooa nuovo database che punta tooa precedente punto nel tempo e le eliminazioni hello database originale. Questo modello di ripristino è più adatto per il ripristino dal danneggiamento dei dati grave perché potrebbe verificarsi la perdita di dati significativi che hello tenant avrebbe tooaccommodate.

1. Aprire il file **Demo-RestoreTenant.ps1** in PowerShell ISE
1. Impostare **$DemoScenario** troppo**5** tooselect hello *tenant in uno scenario di punto di ripristino*.
1. Eseguire tramite **F5**.

script Hello Ripristina punto tooa database tenant di hello cinque minuti prima che l'evento hello è stato eliminato. Questa operazione viene eseguita prima tenendo hello Contoso insieme Hall tenant offline in modo non sono presenti ulteriori aggiornamenti toohello dati. Quindi, parallelo di un database creato tramite il ripristino dal punto di ripristino hello e denominato con un timestamp tooensure hello database non in conflitto con il nome di database hello esistente tenant. Successivamente, viene eliminato il vecchio database di tenant hello e database ripristinato hello è nome del database originale rinominato toohello. Infine, Contoso insieme Hall viene portato il database ripristinato toohello accesso di tooallow online hello app.

È stato ripristinato correttamente hello database tooa punto nel tempo prima di hello evento è stato eliminato. verrà visualizzata la pagina eventi di Hello, pertanto verificare ultimo evento hello è stato ripristinato.


## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione illustra come:

> [!div class="checklist"]

> * Ripristinare un database in un database parallelo (side-by-side)
> * Ripristinare un database sul posto

[Gestire lo schema del database tenant](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni in cui si basano su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md)
* [Informazioni sul backup del database SQL](sql-database-automated-backups.md)
