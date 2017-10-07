---
title: i database in Azure SQL Data Warehouse aaaManage | Documenti Microsoft
description: "Panoramica della gestione dei database di SQL Data Warehouse. Include strumenti di gestione, prestazioni di DWU e di scalabilità orizzontale, risoluzione dei problemi di prestazioni delle query, definizione dei criteri di protezione e ripristino di un database da un danneggiamento dei dati o da un'interruzione dell'alimentazione locale."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Gestire i database in Azure SQL Data Warehouse
SQL Data Warehouse automatizza molti aspetti della gestione dei database. Ad esempio, prestazioni tooscale sufficiente tooadjust e pagare hello livello a destra delle risorse di calcolo e quindi consentire SQL Data Warehouse eseguire tutto il lavoro hello di scalabilità orizzontale e scalabilità back.

È sicuramente consigliabile toomonitor tooidentify il carico di lavoro, le prestazioni è necessario, nonché risolvere i problemi relativi a query con esecuzione prolungata. È inoltre necessario tooperform alcune autorizzazioni toomanage attività di protezione per gli utenti e account di accesso.

Questa panoramica illustra questi aspetti della gestione di SQL Data Warehouse.

* Strumenti di gestione
* Ridimensionare le risorse di calcolo
* Sospendere e riprendere
* Procedure consigliate per le prestazioni
* Monitoraggio delle query
* Sicurezza
* Backup e ripristino

## <a name="management-tools"></a>Strumenti di gestione
È possibile utilizzare vari strumenti toomanage database in SQL Data Warehouse. Per la gestione di database, si svilupperà preferenze dello strumento per ogni tipo di attività è necessario tooperform.

### <a name="azure-portal"></a>Portale di Azure
Hello [portale di Azure] [ Azure portal] è un portale basato sul web in cui è possibile creare, aggiornare ed eliminare i database e monitorare le risorse del database. Questo strumento è molto utile se sta semplicemente Introduzione a Azure, gestisce un numero ridotto di database del data warehouse o necessario tooquickly eseguire un'operazione.

tooget introduttiva hello portale di Azure, vedere [creare un Data Warehouse di SQL (portale di Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools in Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) in Visual Studio consente tooconnect gestire e sviluppare i database. È opportuno che gli sviluppatori di applicazioni con una certa familiarità con Visual Studio o altri ambienti di sviluppo integrato (IDE), provino a usare SSDT in Visual Studio.

SSDT include hello Esplora oggetti SQL Server che consentono di toovisualize, connettersi ed eseguire gli script nei database di SQL Data Warehouse. tooquickly connettersi tooSQL Data Warehouse, è possibile scegliere semplicemente hello **aperta in Visual Studio** pulsante nella barra dei comandi di hello quando si visualizzano i dettagli del database hello in hello portale classico di Azure.  

tooget introduttivi di SSDT in Visual Studio, vedere [Query Azure SQL Data Warehouse con Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Strumenti da riga di comando
Gli strumenti da riga di comando sono ideali per l'automazione dei carichi di lavoro.  PowerShell e sqlcmd sono due modi tooautomate dei processi.  Si consiglia di questi strumenti per gestire un numero elevato di server logici e distribuire le modifiche di risorsa in un ambiente di produzione come attività hello necessarie possono essere inseriti nello script e quindi automatizzata.

### <a name="dynamic-management-views"></a>Viste a gestione dinamica
Viste a gestione dinamica sono hello Pane and burro della gestione di SQL Data Warehouse. Quasi tutte le informazioni che rende visibili nel portale di hello si basano su viste a gestione dinamica. vedere un elenco di SQL Data Warehouse DMV, toosee [viste di sistema di SQL Data Warehouse][SQL Data Warehouse system views].

tooget introduzione, vedere [Connect e query con sqlcmd][Connect and query with sqlcmd], e [creare un database (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Ridimensionare le risorse di calcolo
In SQL Data Warehouse, è possibile aumentare o ridurre rapidamente le prestazioni aumentando o riducendo le risorse di calcolo di CPU, memoria e larghezza di banda di I/O. prestazioni tooscale, toodo è sufficiente modificare il numero di hello warehouse delle unità di dati (Dwu) in cui SQL Data Warehouse alloca tooyour database. SQL Data Warehouse rapidamente hello apportata la modifica e gestisce tutti hello sottostante modifiche toohardware o software.

vedere toolearn più sulla scalabilità Dwu, [scalare prestazioni].

## <a name="pause-and-resume"></a>Sospendere e riprendere
toosave costi, è possibile sospendere e riprendere calcolo risorse su richiesta. Ad esempio, se si prevede di usare database hello durante la notte hello e i fine settimana, è possibile sospenderla durante le ore e riprenderlo giornata hello. È non verrà addebitato Dwu mentre hello database resta sospesa.

Per altre informazioni, vedere le sezioni [Sospendere il calcolo][Pause compute] e [Riprendere il calcolo][Resume compute].

## <a name="performance-best-practices"></a>Procedure consigliate per le prestazioni
Attività iniziali con una nuova tecnologia, individuazione hello suggerimenti e consigli che funzionano migliore destra dall'inizio hello può consentire di risparmiare molto tempo.  Sono disponibili procedure consigliate in molti di questi argomenti.

toosee molti un riepilogo delle considerazioni più importanti di hello quando si sviluppa il carico di lavoro, vedere [procedure consigliate di SQL Data Warehouse][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Monitoraggio delle query
Talvolta una query è in esecuzione troppo lungo, ma non si è certi di quale è provocato da hello. SQL Data Warehouse con viste a gestione dinamica (DMV) che è possibile utilizzare toofigure timeout query in cui sta richiedendo troppo tempo.

query con esecuzione prolungata toofind, vedere [monitorare il carico di lavoro mediante DMV][Monitor your workload using DMVs].

## <a name="security"></a>Sicurezza
toomaintain un sistema sicuro, è necessario essere su avviso hello e proteggersi da qualsiasi tipo di accesso non autorizzato. Un sistema di sicurezza deve toomake che le regole del firewall siano soddisfatti autorizzato in modo che solo gli indirizzi IP possono connettersi. È necessaria l'autenticazione corretta delle credenziali dell'utente. Dopo che un utente è connesso toohello database, hello utente deve solo disporre delle autorizzazioni tooperform un numero minimo di azioni. toosecure dati, è possibile utilizzare la crittografia. È inoltre importante toohave controllo e di rilevamento in modo è possibile ripercorrere eventi nel caso di eventuali attività sospette.

toolearn sulla gestione della sicurezza, head su toohello [Cenni preliminari sulla sicurezza][Security overview].

## <a name="backup-and-restore"></a>Backup e ripristino
Eseguire backup affidabili dei dati è una parte fondamentale di qualsiasi database di produzione. SQL Data Warehouse tiene al sicuro i dati eseguendo automaticamente il backup dei database attivi a intervalli regolari. Questi backup consentono toorecover dagli scenari in cui è stato danneggiato i dati o l'eliminazione accidentale dei dati o database.  Per hello dati pianificazione del backup, criteri di conservazione e toorestore un database, vedere [ripristino da snapshot][Restore from snapshot].

## <a name="next-steps"></a>Passaggi successivi
Principi di progettazione di database appropriata utilizzando renderà più facile toomanage i database in SQL Data Warehouse. altre, toolearn head su toohello [Cenni preliminari sullo sviluppo][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[scalare prestazioni]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
