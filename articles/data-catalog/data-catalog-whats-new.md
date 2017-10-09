---
title: aaaWhat di nuovo in Azure Data Catalog | Documenti Microsoft
description: "Questo articolo fornisce che una panoramica delle nuove funzionalità aggiunte tooAzure catalogo dati."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Novità di Azure Data Catalog
Aggiorna troppo**Azure Data Catalog** periodicamente vengono rilasciate. Non tutte le nuove versioni includono tuttavia nuove funzionalità destinate all'utente, in quanto alcune sono incentrate sulle funzionalità del servizio back-end. Questa pagina sono evidenziate nuovo servizio Azure Data Catalog toohello aggiunta di funzionalità rivolta all'utente.

## <a name="whats-new-for-august-2017"></a>Novità di agosto 2017 
A partire da agosto 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

*   Un nuovo campione developer è disponibile per la creazione e gestione dei metadati di relazione con hello API REST di catalogo dati. Hello *importare le informazioni sulle relazioni nel catalogo dati* esempio è disponibile in hello [pagina degli esempi di codice catalogo dati](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0). 
* Supporto per l'estrazione di aggiungere i metadati di relazione da origini dati Teradata durante la registrazione di tabelle correlate utilizzando strumento di registrazione di origine dati hello.
* Supporto per la funzione con valori di tabella di SQL Server oggetti (TVF) durante la registrazione delle origini dati di SQL Server utilizzando lo strumento di registrazione hello dati origine.
* Più aggiornamenti e miglioramenti delle prestazioni di hello tooincrease e facilità di utilizzo del portale di hello catalogo dati.

## <a name="whats-new-for-july-2017"></a>Novità di luglio 2017 
A partire da luglio 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Supporto per un controllo più granulare sulle operazioni consentite sui metadati, tra cui:
    - Gli amministratori del catalogo possono limitare i tag toocontribute possibilità degli utenti e i metadati correlati toohello catalogo, l'abilitazione di catalogo toohello accesso in sola lettura.
    - Gli amministratori del catalogo è possono limitare possibilità tooregister nuove origini dati degli utenti nel catalogo di hello.
    - Gli amministratori del catalogo è possono limitare la proprietà di tootake possibilità degli utenti dei metadati di asset di dati nel catalogo di hello.
    - È possibile concedere autorizzazioni tooAzure gruppi di sicurezza di Active Directory e gli utenti per facilitare la gestione delle autorizzazioni.
* Supporto per le relazioni tra gli asset di dati registrati e individuazione asset di dati correlati nel portale di catalogo dati hello, tra cui:
    - Estrazione dei metadati di relazione di MySQL, Oracle e SQL Server (inclusi i Database SQL di Azure), origini dati quando si utilizza hello strumento per la registrazione di origine dati del catalogo dati.
    - Individuazione di asset di dati correlati quando si visualizzano i metadati degli asset nel portale di hello catalogo dati.
    - Operazioni toodefine, individuare e gestire le relazioni tra gli asset di dati tramite l'API REST di catalogo dati hello.

Per ulteriori informazioni sulla gestione delle autorizzazioni nel catalogo dati, vedere [modalità di accesso di asset di dati e di catalogo toodata toosecure](data-catalog-how-to-secure-catalog.md).
Per ulteriori informazioni sulle relazioni nel catalogo dati, vedere [asset di dati in Azure Data Catalog di correlazione tooview](data-catalog-how-to-view-related-data-assets.md).

## <a name="whats-new-for-june-2017"></a>Novità di giugno 2017 
A partire da giugno 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Supporto per le origini dati Sybase, Apache Cassandra e MongoDB. Gli utenti ora possono registrare e trovare i database e le tabelle di Cassandra e MongoDB e i database, le tabelle e le visualizzazioni di Sybase.

> [!NOTE]
> Quando la registrazione di MongoDB e Cassandra tabelle che includono colonne con tipi di dati complessi, ad esempio i record e matrici, queste non verranno inclusi nei metadati hello aggiunto tooData catalogo.

## <a name="whats-new-for-may-2017"></a>Novità di maggio 2017 
A partire da maggio 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Un nuovo campione developer è disponibile per l'importazione bulk hello di termini del glossario aziendale. esempio di importazione Bulk glossario Hello è disponibile in hello [pagina degli esempi per sviluppatori di catalogo dati](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples). 
*   Supporto per la modifica delle informazioni di connessione ODBC nel portale di Azure Data Catalog hello. I proprietari di asset di dati e gli amministratori del catalogo dati ora possono modificare le informazioni di connessione hello per le origini dati ODBC registrate senza la necessità di origini dati di registrazione toore hello.
*   Supporto per gli URL selezionabili nelle definizioni e nelle descrizioni del glossario aziendale. Quando gli URL sono incluse nelle proprietà di descrizione e la definizione di hello per i termini del glossario aziendale, hello URL verrà visualizzato come collegamenti ipertestuali nel portale di hello catalogo dati.
*   Inoltre il supporto per la visualizzazione esperto nomi tooexpert indirizzi di posta elettronica. Quando si visualizzano gli esperti nelle proprietà hello per un asset di dati nel portale di catalogo dati hello, nome completo dell'esperto hello da Azure Active Directory verrà visualizzato nella descrizione comando hello.

## <a name="whats-new-for-april-2017"></a>Novità di aprile 2017 
A partire da aprile 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Supporto per origini dati ODBC. Gli utenti possono ora registrare e individuare i database, tabelle e viste mediante strumento per la registrazione di origine dati di hello catalogo dati ODBC.

## <a name="whats-new-for-march-2017"></a>Novità di marzo 2017 
A partire da marzo 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Supporto per l'uso dei gruppi di sicurezza AAD per gli amministratori di Data Catalog.
*   Azure Data Catalog è ora disponibile in una nuova area di Azure. I clienti possono eseguire il provisioning di hello Azure Data Catalog in hello occidentale Stati Uniti centro area, in aggiunta tooEast, Stati Uniti, Stati Uniti occidentali, Europa occidentale e Australia orientale, Europa settentrionale e Asia sudorientale. Per altre informazioni, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

## <a name="whats-new-for-february-2017"></a>Novità di febbraio 2017 
A partire da febbraio 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Supporto per le impostazioni avanzate di strumento per la registrazione di origine dati di hello catalogo dati. Gli utenti possono specificare i valori di timeout comando quando registrano origini dati di grandi dimensioni.
*   Supporto per le origini dati FTP e PostgreSQL. Gli utenti ora possono registrare e trovare i file e le directory FTP e i database, le tabelle e le visualizzazioni di PostgreSQL.

## <a name="whats-new-for-january-2017"></a>Novità di gennaio 2017 
A partire da gennaio January 2017, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Azure Data Catalog ora è conforme a [CSA STAR](https://www.microsoft.com/trustcenter/compliance/csa-star-certification).
*   Integrazione con [Introduzione a Microsoft Power Query per Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605). Gli utenti di Excel possono condividere e trovare le query usando Azure Data Catalog da Excel. Questa funzionalità è disponibile toousers con licenze di Power BI Pro.

## <a name="whats-new-for-december-2016"></a>Novità di dicembre 2016
A partire dal 2016 dicembre, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Azure Data Catalog ora è conforme a [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) e alle [clausole del modello UE](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses).
*   Supporto per la modifica delle informazioni di connessione dell'origine dati. I proprietari di asset di dati e gli amministratori del catalogo dati ora possono modificare le informazioni di connessione hello per le origini dati registrati senza la necessità di origini dati di registrazione toore hello.
*   Supporto per le origini dati Salesforce.com. Gli utenti ora possono registrare e trovare gli oggetti Salesforce.


## <a name="whats-new-for-november-2016"></a>Novità di novembre 2016
A partire da novembre 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:
*   Azure Data Catalog ora è conforme a [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) e [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018).
*   Supporto per la registrazione manuale hello di origini dati ODBC tramite il portale di catalogo dati hello e API REST.

## <a name="whats-new-for-september-2016"></a>Novità di settembre 2016
A partire da settembre 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per origini dati IBM DB2. Gli utenti possono ora registrare e individuare database, tabelle e viste DB2.
* Supporto per le origini dati Azure Cosmos DB. Gli utenti ora possono registrare e trovare i database e le raccolte di Cosmos DB.
* Supporto per la personalizzazione di nome di catalogo hello nel portale di hello catalogo dati. Gli amministratori del catalogo ora possono fornire il testo visualizzato nel titolo del portale hello, ad esempio il nome di organizzazione hello.

## <a name="whats-new-for-august-2016"></a>Novità di agosto 2016
A partire da agosto 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Miglioramenti nella registrazione di origini dati SQL Server Master Data Services (MDS). Gli utenti possono ora includere profili anteprime e i dati durante la registrazione di entità MDS utilizzando strumento per la registrazione di origine dati di hello catalogo dati.
* Supporto di ricerche salvate aziendali definite dall'amministratore. Quando si salva una ricerca nel portale di catalogo dati hello, gli amministratori del catalogo dati possono ora scegliere toosave ricerche per uso personale o per tutti gli utenti del catalogo. Le ricerche salvate aziendali vengono condivise con tutti gli utenti del catalogo e possono offrire punti di partenza standardizzati per l'individuazione delle origini dati.
* Aggiorna visualizzazione delle proprietà toohello nel portale di hello catalogo dati. Tutte le proprietà di asset di dati vengono ora visualizzate e gestiti in un tooprovide riquadro ridimensionabili, solo un'esperienza più uniforme e individuabile.

## <a name="whats-new-for-july-2016"></a>Novità di luglio 2016
A partire da luglio 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per origini dati SQL Server Master Data Services (MDS). Gli utenti possono ora registrare e individuare modelli ed entità MDS.
* Supporto per le stored procedure di SQL Server. Gli utenti possono ora registrare e individuare oggetti stored procedure in origini dati SQL Server.
* Supporto per lingue aggiuntive nel portale di Azure Data Catalog hello e hello dati origine strumento di registrazione per un totale di 18 lingue supportate. Hello esperienza utente di Azure Data Catalog è localizzata in base alle preferenze di lingua hello impostata nella finestra di Windows o nel browser web hello.
* Gli aggiornamenti e ottimizzazione per hello catalogo dati home page del portale, inclusi i miglioramenti delle prestazioni e un'esperienza utente ottimizzata.

## <a name="whats-new-for-june-2016"></a>Novità di giugno 2016
A partire da giugno 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per il ridimensionamento di colonne nella visualizzazione elenco hello durante l'individuazione di asset di dati nel portale di hello catalogo dati. Gli utenti possono ora ridimensionare le singole colonne toomore agevole lettura dei metadati dell'asset di lunga durata, ad esempio tag e le descrizioni.
* Power Query per Excel è stata aggiunta dal menu "Apri in" toohello nel portale di hello catalogo dati. Gli utenti possono ora aprire origini dati supportate in Excel 2016 o in Excel 2010 ed Excel 2013 con hello [Power Query per Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) aggiuntivo installato.
* Supporto per origini dati Archiviazione tabelle di Azure. Gli utenti possono ora registrare e individuare oggetti tabella in origini dati Archiviazione tabelle di Azure.

## <a name="whats-new-for-may-2016"></a>Novità di maggio 2016
A partire da maggio 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Un glossario aziendale che consente agli amministratori di catalogo toodefine business termini e le gerarchie toocreate un vocabolario aziendale comune. Gli utenti possono tag asset di dati registrati con toomake termini di glossario è più facile toodiscover e comprendere il contenuto di hello del catalogo di hello. Per ulteriori informazioni, vedere [come tooset backup hello glossario aziendale per contrassegnare i governato](data-catalog-how-to-business-glossary.md)  
* Miglioramenti toohello glossario aziendale di catalogo dati che consente agli utenti tooupdate più termini di glossario in un'unica operazione. Gli utenti possono selezionare più hello tooedit di termini seguenti campi:
  * Termine padre: hello selezionabili dall'utente un nuovo termine padre e tutti i termini selezionati sono figli toobe aggiornato del termine padre hello selezionato. Se hello selezionata termini che hanno hello stesso elemento padre, quindi tale padre viene visualizzato nella casella di testo hello, in caso contrario campo termine padre di hello è tooblank set.   
  * Tag e le parti interessate: gli utenti possono aggiungere e rimuovere i tag e le parti interessate per più termini di glossario utilizzando hello stesse funzioni come tag più asset di dati.

> [!NOTE]
> Glossario aziendale Hello è disponibile solo nell'edizione Standard di Azure Data Catalog hello. Hello edizione gratuita non fornisce funzionalità per la codifica gestita o un glossario aziendale.

## <a name="whats-new-for-march-2016"></a>Novità di marzo 2016
A partire dal 2016 marzo, hello seguenti funzionalità è state aggiunte tooAzure dati del catalogo: g:

* Un endpoint API REST consolidato per l'accesso a livello di programmazione di funzionalità di ricerca hello e funzionalità di gestione asset di catalogo di hello servizio Azure Data Catalog. L'endpoint API di ricerca e l'endpoint API di catalogo sono stati dichiarati obsoleti e interrotti il 21 marzo 2016. Non sono presenti modifiche toohello semantica di hello API. Solo endpoint di hello URI modificato. Per ulteriori informazioni, vedere hello [riferimento all'API REST di Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267595.aspx). Per esempi di API, vedere gli [esempi per sviluppatori di Azure Data Catalog](data-catalog-samples.md).

## <a name="whats-new-for-february-2016"></a>Novità di febbraio 2016
A partire da febbraio 2016, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Selezione di un'origine dati appena riprogettato un'esperienza nello strumento per la registrazione di origine dati di hello Azure Data Catalog. Hello strumento per la registrazione di origine dati è stata aggiornata toomake it più semplice è toolocate e selezionare origini dati hello è supportato da Azure Data Catalog.
* Supporto per 10 lingue aggiuntive nel portale di Azure Data Catalog hello e strumento di registrazione di origine dati hello. Inoltre, tooEnglish hello esperienza di Azure Data Catalog è ora disponibile in tedesco, spagnolo, francese, italiano, giapponese, coreano, portoghese brasiliano, russo, cinese semplificato e cinese tradizionale. Hello Azure Data Catalog è localizzata esperienza utente in base alle preferenze di lingua hello impostata nella finestra di Windows o nel web browser dell'utente hello.
* Supporto della replica geografica dei dati di Azure Data Catalog per la continuità aziendale e il ripristino di emergenza. Tutto il contenuto di Azure Data Catalog, inclusi l'origine dei metadati e crowdsourced le annotazioni dei dati, ora viene replicato tra due aree di Azure in toocustomers alcun costo aggiuntivo. pre-vengono abbinate almeno 500 miglia di distanza, Hello aree di Azure e seguire il mapping di hello, come descritto in [Business continuità e ripristino di emergenza (BCDR): aree abbinate Azure](../best-practices-availability-paired-regions.md).
* Supporto per la modifica hello sottoscrizione di Azure usata da Azure Data Catalog. Azure Data Catalog consente agli amministratori pagina Impostazioni hello in hello tooselect portale di Azure Data Catalog un'altra sottoscrizione di Azure per la fatturazione.

## <a name="whats-new-for-january-2016"></a>Novità di gennaio 2016
A partire da gennaio 2016 hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per la registrazione manuale di tipi di origini dati aggiuntive. È ora possibile utilizzare "Crea voce manuale" nel portale di Azure Data Catalog hello o utilizzare hello tooregister di API REST di Azure Data Catalog hello seguenti origini dati:
  * OData: funzione, set di entità e contenitore di entità
  * HTTP: file, endpoint, report e sito
  * File system: file
  * SharePoint: elenco
  * FTP: file e directory
  * Salesforce.com: oggetto
  * DB2: tabella, vista e database
  * PostgreSQL: tabella, vista e database
* Supporto per "Apri in SQL Server Data Tools" per le origini dati SQL Server, inclusi il database SQL di Azure e Azure SQL Data Warehouse.  
* Supporto per la registrazione e l'individuazione di viste e pacchetti SAP HANA. È possibile registrare SAP HANA origini dati utilizzando i dati di Azure Data Catalog hello strumento di registrazione di origine e possono aggiungere annotazioni e individuare origini di dati SAP HANA registrate tramite il portale di Azure Data Catalog hello.
* Hello toopin possibilità e rimozione di un asset di dati nel portale di Azure Data Catalog hello. È possibile scegliere toopin dati asset toomake li toorediscover e riutilizzo.
* Pagina iniziale riprogettata nel portale di Azure Data Catalog hello. Hello nuova home page include approfondite corrente utenti attività hello - inclusi recente pubblicato asset, aggiunto asset e ricerche salvate - e approfondite attività hello in hello catalogo nel suo complesso.
* Supporto per le impostazioni utente persistente nel portale di Azure Data Catalog hello. Le impostazioni esperienza utente - visualizzazione griglia o riquadro inclusi hello numero di risultati per pagina e raggiunge o disabilita evidenziazione - sono persistenti tra le sessioni utente.
* Azure Data Catalog è ora disponibile in due nuove aree di Azure. I clienti possono eseguire il provisioning di hello Azure Data Catalog in hello Nord Europa e Asia sudorientale aree, in aggiunta tooEast, Stati Uniti, Australia orientale, Europa occidentale e Stati Uniti occidentali. Per altre informazioni, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

> [!NOTE]
> "Apri in SQL Server Data Tools" richiede Visual Studio 2013 con Update 4 e gli strumenti di SQL Server toobe installato. tooinstall hello più recente di SQL Server Data Tools, visitare [SQL Download di Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


## <a name="whats-new-for-december-2015"></a>Novità di dicembre 2015
A partire da dicembre 2015, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per profili dati per le origini dati di SQL Data Warehouse di Azure. Durante la registrazione di viste e tabelle di Azure SQL Data Warehouse, è possibile scegliere le metriche di profilo dati tooinclude con metadati hello estratti dall'origine dati hello.
* Supporto per la registrazione e l'individuazione degli oggetti e dei database MySQL. Gli utenti possono registrare MySQL origini dati utilizzando i dati di Azure Data Catalog hello strumento di registrazione di origine e possono aggiungere annotazioni e individuare origini di dati MySQL registrate tramite il portale di Azure Data Catalog hello.
* Supporto per l'autenticazione SPNEGO e Windows per le origini dati di Teradata. Quando si registra Teradata tabelle e viste, gli utenti possono scegliere tooTeradata tooconnect utilizzando l'autenticazione SPNEGO e Windows, LDAP e TD2.
* Supporto per le origini dati di Archivio Azure Data Lake. Gli utenti possono ora registrarsi e individuare le origini dati di Archivio Azure Data Lake tramite Azure Data Catalog.
* Supporto per specificare manualmente le impostazioni proxy di rete nello strumento di registrazione origine di dati di hello Azure Data Catalog. Gli utenti possono selezionare "Modificare le impostazioni di proxy" dalla pagina di benvenuto hello dello strumento e possono specificare hello proxy indirizzo e porta toobe utilizzato dallo strumento hello.

## <a name="whats-new-for-november-2015"></a>Novità di novembre 2015
A partire da novembre 2015, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Hello tooview possibilità e copiare le stringhe di connessione dal portale di Azure Data Catalog hello per SQL Server (inclusi i Database SQL di Azure) e origini dati Oracle. Gli utenti possono selezionare il collegamento "Visualizza le stringhe di connessione" nelle informazioni di connessione hello per un Server SQL o tabella, vista o un database, toosee hello stringhe di connessione Oracle utilizzato tooconnect toohello origine dei dati. Le stringhe di connessione ADO.NET, ODBC, OLEDB e JDBC sono disponibili per le origini dati di SQL Server. Le stringhe di connessione ODBC e OLEDB vengono fornite per le origini dati di Oracle.
* Supporto per includere i profili dati durante la registrazione delle tabelle Teradata e visualizzazioni.
* Supporto per "Apri in Power BI Desktop" per le origini di SQL Server (inclusi i database SQL di Azure e SQL Data Warehouse di Azure), SQL Server Analysis Services. Archiviazione di Azure e HDFS.  
* Supporto per l'autenticazione LDAP per le origini dati di Teradata. Quando si registra Teradata tabelle e viste, gli utenti possono scegliere tooTeradata tooconnect tramite LDAP e l'autenticazione TD2.
* Supporto per "Apri in Excel" per le origini dati di Teradata.
* Supporto per i termini di ricerca recenti nel portale di Azure Data Catalog hello. Quando una ricerca nel portale di hello, gli utenti possono selezionare esperienza di ricerca usati di recente termini tooaccelerate hello di individuazione.
* Supporto per l’anteprima per le origini dati Teradata. Durante la registrazione Teradata tabelle e viste, gli utenti possono scegliere record snapshot tooinclude con metadati hello estratti dall'origine dati hello.
* Supporto per "Apri in Excel" per le origini dati di SQL Data Warehouse di Azure.
* Supporto per la definizione e la modifica di schemi a livello di colonna per gli asset di dati registrati manualmente. Dopo aver creato manualmente un asset di dati tramite il portale di Azure Data Catalog hello, gli utenti possono aggiungere definizioni di colonna nelle proprietà di asset di dati hello.
* Supporto per le query "ha" durante la ricerca di Azure Data Catalog, individuazione di hello tooenable degli asset di dati registrati che dispone dei metadati specifici. La sintassi di query di Azure Data Catalog ora include:

| Sintassi delle query | Scopo |
| --- | --- |
| `has:previews` |Trova gli asset di dati che includono un'anteprima |
| `has:documentation` |Trova gli asset di dati per i quali è stata fornita la documentazione |
| `has:tableDataProfiles` |Trova gli asset di dati con informazioni sul profilo dei dati a livello di tabella |
| `has:columnsDataProfiles` |Trova gli asset di dati con informazioni sul profilo dei dati a livello di colonna |


> [!NOTE]
> "Apri in Power BI Desktop" richiede una versione corrente di hello toobe di applicazione di Power BI Desktop installata. Se si verificano problemi o errori durante l'utilizzo di questa funzionalità, assicurarsi di aver hello la versione più recente di Power BI Desktop da [PowerBI.com](https://powerbi.com).


## <a name="whats-new-for-october-2015"></a>Novità di ottobre 2015
A partire da ottobre 2015, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per la crittografia locale delle anteprime e dei profili dati per le origini dati registrate. Azure Data Catalog crittografa in modo trasparente i record di anteprima e dati dei profili di origini dati registrate con il servizio di hello, senza necessità di gestione delle chiavi per gli amministratori del catalogo.
* Supporto per origini dati Teradata. Gli utenti possono ora registrarsi e individuare tabelle e viste Teradata.
* Supporto per le origini dati Hive locali. Gli utenti possono ora registrarsi e individuare tabelle Hive per Apache Hive di Hadoop in origini dati locali.
* Supporto per le ricerche salvate nel portale di Azure Data Catalog hello. Gli utenti possono salvare i termini di ricerca e filtro selezioni tooeasily ripetere ricerche precedenti e definire viste utile del contenuto del catalogo hello. Possono anche contrassegnare una ricerca salvata come ricerca predefinita. Quando un utente fa clic sull'icona di ricerca hello "lente di ingrandimento" hello Azure Data Catalog home page portale o dalla pagina "getting started" hello, utente hello viene eseguita direttamente toohello contrassegnata come predefinite ricerca salvata.
* Supporto per la documentazione di testo RTF per asset di dati registrati e i contenitori nel portale di Azure Data Catalog hello. Gli utenti ora possono fornire la documentazione per asset di dati, ad esempio tabelle, viste e report, e per i contenitori, ad esempio database e modelli, per gli scenari in cui tag e descrizioni non sono sufficienti.
* Supporto per la registrazione manuale di tipi di origini dati conosciuti. Gli utenti possono immettere manualmente le informazioni sull'origine dati utilizzando il portale di Azure Data Catalog hello per tutti i tipi di origini dati supportati da Azure Data Catalog.
* Supporto per l'autorizzazione di gruppi di sicurezza di Azure Active Directory. Gli amministratori del catalogo è possono abilitare catalogo toosecurity gruppi di accesso, account utente, rendendo più semplice toomanage accesso tooAzure catalogo dati.
* Supporto per l'apertura di origini dati di Hive dal portale di Azure Data Catalog hello in Excel.

> [!NOTE]
> Per la versione corrente di hello, è supportata solo l'autenticazione Teradata TD2. Nelle versioni future saranno supportati meccanismi di autenticazione aggiuntivi.

> [!NOTE]
> funzionalità di "Apri in Excel" toouse hello per le origini dati Hive, gli utenti sia installato il driver ODBC di hello per l'Hive.

## <a name="whats-new-for-september-2015"></a>Novità di settembre 2015
A partire da settembre 2015, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per includere i profili dati durante la registrazione delle origini dati Hive.
* Supporto per l'individuazione a livello di codice hello API di catalogo, rendendo più semplice per toointegrate di applicazioni con Azure Data Catalog.
* Un nuova "getting started" origine dati individuazione esperienza nel portale di Azure Data Catalog hello. Quando gli utenti immettono pagina "individua" hello del portale di Azure Data Catalog hello senza immettere un termine di ricerca, viene visualizzata un'anteprima del contenuto di catalogo hello inclusi tag hello utilizzato più di frequente, gli esperti, tipi di origini dati e tipi di oggetto.
* Supporto per la registrazione e l'individuazione degli oggetti e dei database di Azure SQL Data Warehouse. Per altre informazioni su Azure SQL Data Warehouse, vedere [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
* Supporto per la registrazione e l'individuazione di modelli di SQL Server Analysis Services e di server SQL Server Reporting Services come contenitori. Quando si registra gli oggetti SSRS e SSAS, Azure Data Catalog crea una voce per il modello SSAS hello e server SSRS e per i report di hello e altri oggetti. i contenitori di Hello possono essere individuati e annotate tramite il portale di Azure Data Catalog hello. Gli utenti possono inoltre cercare e filtrare contenuto hello di un modello o un server toosearching aggiunta e il filtro contenuto hello del catalogo di hello.
* Supporto per la registrazione e l'individuazione degli oggetti di SQL Server Analysis Services tramite HTTP/HTTPS. Gli utenti possono ora connettersi tooSSAS server tramite un URL (ad esempio https://servername/olap/msmdpump.dll) anziché un nome di server e possono utilizzare l'autenticazione di base e le connessioni anonime nell'autenticazione tooWindows aggiunta. Per ulteriori informazioni su tooSSAS connessioni HTTP/HTTPS, vedere [configurare l'accesso HTTP tooAnalysis servizi](https://msdn.microsoft.com/library/gg492140.aspx).
* Supporto per le origini dati Hive in HDInsight. Gli utenti possono ora registrarsi e individuare le tabelle Hive per Apache Hive di Hadoop sulle origini dati HDInsight. Per ulteriori informazioni su Hive in HDInsight, vedere hello [Centro documentazione di HDInsight](../hdinsight/hdinsight-use-hive.md).
* Supporto per la registrazione e l'individuazione dei database Oracle e dei cluster HDFS come contenitori. Quando si registra tabelle Oracle e visualizzazioni o HDFS, Azure Data Catalog crea una voce per il database di hello, tabelle e viste. database Hello è possibile individuare e annotata con il portale di Azure Data Catalog hello. Gli utenti possono inoltre cercare e filtrare hello contenuto di un database o del cluster inoltre toosearching e filtrare il contenuto di hello del catalogo hello.
* Supporto per la registrazione manuale di tipi di origini dati sconosciute. Gli utenti possono immettere manualmente le informazioni sull'origine dati usando il portale di Azure Data Catalog hello, in modo che le origini dati supportate in modo non esplicito dall'hello strumento per la registrazione di origine dati può essere annotato ed individuato.
* Supporto per la registrazione e l'individuazione dei database di SQL Server come contenitori. Durante la registrazione di viste e tabelle di SQL Server, Azure Data Catalog crea una voce per il database di hello, tabelle e viste. database Hello è possibile individuare e annotata con il portale di Azure Data Catalog hello. Inoltre, gli utenti possono cercare e filtrare contenuto hello di un database toosearching aggiunta e il filtro contenuto hello del catalogo di hello.

> [!NOTE]
> SSRS e SSAS oggetti che sono stato registrato toohello precedente versione di settembre 18 devono essere nuovamente registrati con strumento di registrazione di origine dati hello prima hello del server o del modello viene aggiunta voce toohello catalogo. Nuova registrazione di un'origine dati non influenza le annotazioni che sono stati aggiunti dagli utenti nel portale di Azure Data Catalog hello.

> [!NOTE]
> Le tabelle Oracle, viste e i file HDFS e le directory che sono stato registrato toohello precedente versione 11 settembre devono essere registrate nuovamente mediante strumento di registrazione di origine dati hello prima hello database o del cluster viene aggiunta voce toohello catalogo. Nuova registrazione di un'origine dati non influenza le annotazioni che sono stati aggiunti dagli utenti nel portale di Azure Data Catalog hello.

> [!NOTE]
> Tabelle di SQL Server e le viste che sono stato registrato toohello precedente versione di settembre 4 devono essere registrate nuovamente mediante strumento di registrazione di origine dati hello prima dell'aggiunta di voce del database hello toohello catalogo. Nuova registrazione di un'origine dati non influenza le annotazioni che sono stati aggiunti dagli utenti nel portale di Azure Data Catalog hello.

## <a name="whats-new-for-august-2015"></a>Novità di agosto 2015
A partire da agosto 2015, hello seguenti funzionalità è state aggiunte tooAzure catalogo dati:

* Supporto per l'analisi dei dati di origini dati di SQL Server e Oracle. Durante la registrazione di viste e tabelle di SQL Server e Oracle, gli utenti possono scegliere tooinclude dati le informazioni per gli oggetti hello in corso la registrazione. profilo dati Hello include le statistiche a livello di oggetto e a livello di colonna.
* Supporto per le origini dati HDFS Hadoop. Gli utenti possono ora registrarsi e individuare directory e file HDFS.
* Supporto per fornire informazioni sulla richiesta di accesso per le origini dati registrate. Per un asset di dati registrati, gli utenti ora possono fornire istruzioni per richiedere l'accesso, inclusi i collegamenti di posta elettronica o URL, tooeasily l'integrazione con i processi e gli strumenti esistenti.
* Descrizioni comandi per i tag e gli esperti, toomake è più facile toodiscover quali utenti hanno fornito i metadati per asset di dati registrati.
* È stato aggiunto un nuovo "User" pulsante e menu tooour barra di spostamento superiore. Questo menu consente utente hello vedere hello toolog di account utilizzato nel catalogo dati tooAzure e toosign out se lo si desidera. Questo menu Visualizza anche il nome del catalogo hello, che è utile toodevelopers utilizzando hello API REST di Azure Data Catalog.
* Solo per Standard Edition: Durante l'aggiunta di risorse toodata proprietari, Azure Data Catalog supporta ora sia gli account utente e gruppi di sicurezza come proprietari. tooadd un gruppo di sicurezza come proprietario per gli asset di dati selezionato, è possibile immettere nome visualizzato del gruppo di hello o indirizzo di posta elettronica del gruppo di hello UPN, se presente.
* Supporto per le origini dati dell'archivio BLOB di Azure. Gli utenti possono ora registrarsi e individuare i BLOB e le directory di archiviazione di Azure.

