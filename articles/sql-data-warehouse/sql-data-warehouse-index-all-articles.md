---
title: argomenti aaaAll per il servizio SQL Data Warehouse | Documenti Microsoft
description: Tabella di tutti gli argomenti per il servizio di Azure hello denominata SQL Data Warehouse che esiste nel http://azure.microsoft.com/documentation/articles/, titolo e descrizione.
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Tutti gli argomenti per il servizio SQL Data Warehouse di Azure
Questo argomento vengono elencati tutti gli argomenti che si applica direttamente toohello **SQL Data Warehouse** servizio di Azure. È possibile cercare la pagina Web per le parole chiave tramite **Ctrl + F**, toofind hello argomenti corrente.

## <a name="new"></a>Nuovo
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 1 |[Backup di SQL Data Warehouse](sql-data-warehouse-backups.md) |Per informazioni sui backup di database predefiniti SQL Data Warehouse che consentono di toorestore un punto di ripristino di Azure SQL Data Warehouse tooa oppure un'area geografica diversa. |

## <a name="updated-articles-sql-data-warehouse"></a>Articoli aggiornati, SQL Data Warehouse
Questa sezione contiene articoli che sono stati aggiornati di recente, in cui aggiornare hello è grande o significativo. Per ogni articolo aggiornato, un frammento approssimativo di hello aggiunto viene visualizzato il testo di markdown. sono stati aggiornati gli articoli di Hello nell'intervallo di date hello di **2016-08-22** troppo**2016-10-05**.

| &nbsp; | Articolo | Testo aggiornato, frammento di codice | Data aggiornamento |
| ---:|:--- |:--- |:--- |
| 2 |[Caricare dati dall’archiviazione BLOB di Azure in un SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |byte/tootrack e file selezionare r.command, s.request_id, r.status, count (distinct input_name) come nbr_files, sum (s.bytes_processed) / 1024/1024 come gb_processed sys.dm_pdw_exec_requests r inner join sys.dm_pdw_dms_external_work s su r.request_id = s.request_id WHERE r. label  = 'CTAS : Load  cso . DimProduct  '  OR r. label  = 'CTAS : Load  cso . FactOnlineSales  ' GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |2016-09-07 |
| 3 |[Ripristino di SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |* * È possibile ripristinare un pausa data warehouse? * * toorestore un data warehouse è stato sospeso, è necessario toofirst riportarlo online. Una volta hello data warehouse è in linea, si dispone di sette giorni di toochoose punti di ripristino da. * * Ripristina tooa con ridondanza geografica area * * Se si utilizza l'archiviazione con ridondanza geografica hello, è possibile ripristinare il centro hello dati warehouse tooyour dati associati in un'area geografica diversa. data warehouse di Hello viene ripristinato dal backup giornaliero ultimo hello. * * Il ripristino della sequenza temporale * * è possibile ripristinare un punto di ripristino di database tooany all'interno di hello negli ultimi sette giorni. Gli snapshot avviare ogni quattro ore tooeight e sono disponibili sette giorni. Quando uno snapshot supera i sette giorni di vita, scade e il relativo punto di ripristino non è più disponibile. * * Ripristina i costi di archiviazione hello costi * * per data warehouse di hello ripristinato viene fatturato alla tariffa di archiviazione di Azure Premium hello. Se si sospende un ripristinato data warehouse, viene addebitata per l'archiviazione con frequenza di archiviazione di Azure Premium hello. Il vantaggio di Hello della sospensione non è che si addebito |2016-09-29 |

## <a name="get-started"></a>Introduzione
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 4 |[TooAzure l'autenticazione SQL Data Warehouse](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse. |
| 5 |[Procedure consigliate per Azure SQL Data Warehouse](sql-data-warehouse-best-practices.md) |Indicazioni e procedure consigliate da conoscere per lo sviluppo di soluzioni per Azure SQL Data Warehouse. Queste indicazioni aiuteranno a svolgere al meglio il lavoro. |
| 6 |[Driver per Azure SQL Data Warehouse](sql-data-warehouse-connection-strings.md) |Stringhe di connessione e driver per SQL Data Warehouse |
| 7 |[Connettersi tooAzure SQL Data Warehouse](sql-data-warehouse-connect-overview.md) |La modalità di connessione e il nome di server hello toofind stringa per il tooAzure SQL Data Warehouse |
| 8 |[Analizzare i dati con Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Utilizzare Azure Machine Learning toobuild un stima modello di machine learning basato sui dati archiviati in Azure SQL Data Warehouse. |
| 9 |[Eseguire query in Azure SQL Data Warehouse (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Esecuzione di query su Azure SQL Data Warehouse con sqlcmd hello utilità della riga di comando. |
| 10 |[Creare un database di SQL Data Warehouse usando Transact-SQL (TSQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Informazioni su come toocreate un esempio di SQL Azure Data Warehouse con TSQL |
| 11 |[Modalità di concessione ticket toocreate un supporto per SQL Data Warehouse](sql-data-warehouse-get-started-create-support-ticket.md) |Come supporto toocreate ticket in Azure SQL Data Warehouse. |
| 12 |[Caricare i dati con Azure Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Informazioni su dati tooload con Data Factory di Azure |
| 13 |[Caricare dati con PolyBase in SQL Data Warehouse](sql-data-warehouse-get-started-load-with-polybase.md) |Vengono illustrate le novità PolyBase e come toouse per scenari di data warehouse. |
| 14 |[Creare un Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md) |Informazioni su come toocreate un Azure SQL Data Warehouse in hello portale di Azure |
| 15 |[Creare SQL Data Warehouse con PowerShell](sql-data-warehouse-get-started-provision-powershell.md) |Creare un'istanza di SQL Data Warehouse con PowerShell |
| 16 |[Visualizzare i dati con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Visualizzare i dati di SQL Data Warehouse con Power BI |
| 17 |[Eseguire query in Azure SQL Data Warehouse (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Eseguire query in SQL Data Warehouse con Visual Studio. |

## <a name="develop"></a>Sviluppare
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 18 |[Ottimizzazione delle transazioni per SQL Data Warehouse](sql-data-warehouse-develop-best-practices-transactions.md) |Indicazioni sulle procedure consigliate per la scrittura di aggiornamenti di transazioni efficienti in Azure SQL Data Warehouse |
| 19 |[Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md) |Informazioni sulla gestione della concorrenza e del carico di lavoro nel Data Warehouse di SQL Azure per lo sviluppo di soluzioni. |
| 20 |[Create Table As Select (CTAS) in SQL Data Warehouse](sql-data-warehouse-develop-ctas.md) |Suggerimenti per la codifica con hello creare una tabella come selezionare l'istruzione (un'istruzione CTAS) in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 21 |[SQL dinamico in SQL Data Warehouse](sql-data-warehouse-develop-dynamic-sql.md) |Suggerimenti per l’utilizzo di SQL dinamico in SQL Data Warehouse di Azure per lo sviluppo di soluzioni. |
| 22 |[Opzioni Group by in SQL Data Warehouse](sql-data-warehouse-develop-group-by-options.md) |Suggerimenti per l’implementazione delle opzioni group by in SQL Data Warehouse di Azure per lo sviluppo di soluzioni. |
| 23 |[Utilizzare le query tooinstrument di etichette in SQL Data Warehouse](sql-data-warehouse-develop-label.md) |Suggerimenti per l'utilizzo di query tooinstrument etichette in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 24 |[Cicli in SQL Data Warehouse](sql-data-warehouse-develop-loops.md) |Suggerimenti sui di cicli Transact-SQL e sulla sostituzione di cursori in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 25 |[Stored procedure in SQL Data Warehouse](sql-data-warehouse-develop-stored-procedures.md) |Suggerimenti per l'implementazione delle stored procedure in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 26 |[Transazioni in SQL Data Warehouse](sql-data-warehouse-develop-transactions.md) |Suggerimenti per l'implementazione di transazioni in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 27 |[Schemi definiti dall'utente in SQL Data Warehouse](sql-data-warehouse-develop-user-defined-schemas.md) |Suggerimenti per l'uso di schemi Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 28 |[Assegnare variabili in SQL Data Warehouse](sql-data-warehouse-develop-variable-assignment.md) |Suggerimenti per l'assegnazione di variabili Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 29 |[Viste in SQL Data Warehouse](sql-data-warehouse-develop-views.md) |Suggerimenti per l'uso di viste Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 30 |[Decisioni di progettazione e tecniche di codifica per SQL Data Warehouse](sql-data-warehouse-overview-develop.md) |Concetti di sviluppo, decisioni di progettazione, suggerimenti e tecniche di codifica per SQL Data Warehouse. |

## <a name="manage"></a>Manage
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 31 |[Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica)](sql-data-warehouse-manage-compute-overview.md) |Funzionalità relative alla scalabilità orizzontale delle prestazioni in Azure SQL Data Warehouse. Scalabilità orizzontale grazie alla regolazione Dwu o sospendere e riprendere toosave risorse di calcolo dei costi. |
| 32 |[Gestire la potenza di calcolo in Azure SQL Data Warehouse (portale di Azure)](sql-data-warehouse-manage-compute-portal.md) |Attività del portale Azure toomanage potenza di calcolo. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, è possibile sospendere e riprendere toosave costi delle risorse di calcolo. |
| 33 |[Gestire la potenza di calcolo in Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |Potenza di calcolo toomanage attività PowerShell. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, è possibile sospendere e riprendere toosave costi delle risorse di calcolo. |
| 34 |[Gestire la potenza di calcolo in Azure SQL Data Warehouse (REST)](sql-data-warehouse-manage-compute-rest-api.md) |Potenza di calcolo toomanage attività PowerShell. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, è possibile sospendere e riprendere toosave costi delle risorse di calcolo. |
| 35 |[Gestire la potenza di calcolo in Azure SQL Data Warehouse (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Prestazioni tooscale-out di Transact-SQL (T-SQL) attività regolando Dwu. Risparmiare sui costi eseguendo una scalabilità orizzontale durante le ore non di punta. |
| 36 |[Monitoraggio del carico di lavoro mediante DMV](sql-data-warehouse-manage-monitor.md) |Informazioni su come toomonitor il carico di lavoro mediante DMV. |
| 37 |[Gestire i database in Azure SQL Data Warehouse](sql-data-warehouse-overview-manage.md) |Panoramica della gestione dei database di SQL Data Warehouse. Include strumenti di gestione, prestazioni di DWU e di scalabilità orizzontale, risoluzione dei problemi di prestazioni delle query, definizione dei criteri di protezione e ripristino di un database da un danneggiamento dei dati o da un'interruzione dell'alimentazione locale. |
| 38 |[Monitorare le query utente in Azure SQL Data Warehouse](sql-data-warehouse-overview-manage-user-queries.md) |Panoramica di considerazioni hello, procedure consigliate e le attività per il monitoraggio delle query utente in Azure SQL Data Warehouse |
| 39 |[Ripristino di SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |Panoramica delle opzioni di ripristino di database di hello per il ripristino di un database in Azure SQL Data Warehouse. |
| 40 |[Ripristinare un'istanza di Azure SQL Data Warehouse (portale)](sql-data-warehouse-restore-database-portal.md) |Attività del portale di Azure per il ripristino di un'istanza di Azure SQL Data Warehouse. |
| 41 |[Ripristinare un'istanza di Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Attività di PowerShell per il ripristino di un'istanza di Azure SQL Data Warehouse. |
| 42 |[Ripristinare un'istanza di Azure SQL Data Warehouse (API REST)](sql-data-warehouse-restore-database-rest-api.md) |Attività dell'API REST per il ripristino di un'istanza di Azure SQL Data Warehouse. |

## <a name="tables-and-indexes"></a>Tabelle e indici
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 43 |[Tipi di dati per le tabelle in SQL Data Warehouse](sql-data-warehouse-tables-data-types.md) |Introduzione ai tipi di dati per le tabelle di Azure SQL Data Warehouse. |
| 44 |[Distribuzione di tabelle in SQL Data Warehouse](sql-data-warehouse-tables-distribute.md) |Introduzione alla distribuzione di tabelle in SQL Data Warehouse di Azure. |
| 45 |[Indicizzazione di tabelle in SQL Data Warehouse](sql-data-warehouse-tables-index.md) |Introduzione all'indicizzazione delle tabelle in Azure SQL Data Warehouse. |
| 46 |[Panoramica delle tabelle in SQL Data Warehouse](sql-data-warehouse-tables-overview.md) |Introduzione alle tabelle di SQL Data Warehouse di Azure. |
| 47 |[Tabelle di partizionamento in SQL Data Warehouse](sql-data-warehouse-tables-partition.md) |Introduzione al partizionamento delle tabelle di SQL Data Warehouse di Azure. |
| 48 |[Gestione delle statistiche nelle tabelle in SQL Data Warehouse](sql-data-warehouse-tables-statistics.md) |Introduzione alle statistiche nelle tabelle di SQL Data Warehouse di Azure. |
| 49 |[Tabelle temporanee in SQL Data Warehouse](sql-data-warehouse-tables-temporary.md) |Introduzione alle tabelle temporanee di SQL Data Warehouse di Azure. |

## <a name="integrate"></a>Integrare
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 50 |[Usare Data factory di Azure con SQL Data Warehouse](sql-data-warehouse-integrate-azure-data-factory.md) |Suggerimenti per l'uso di Data factory di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 51 |[Usare Azure Machine Learning con SQL Data Warehouse](sql-data-warehouse-integrate-azure-machine-learning.md) |Suggerimenti per l'uso di Azure Machine Learning con Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 52 |[Usare Analisi di flusso di Azure con SQL Data Warehouse](sql-data-warehouse-integrate-azure-stream-analytics.md) |Suggerimenti per l'uso di Analisi di flusso di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 53 |[Usare Power BI con SQL Data Warehouse](sql-data-warehouse-integrate-power-bi.md) |Suggerimenti per l'uso di Power BI con Azure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 54 |[Utilizzare altri servizi con SQL Data Warehouse](sql-data-warehouse-overview-integrate.md) |Strumenti e partner con soluzioni che interagiscono con SQL Data Warehouse. |

## <a name="load"></a>chiudi
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 55 |[Caricare i dati dall'archivio BLOB di Azure in Azure SQL Data Warehouse (Azure Data Factory)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Informazioni su dati tooload con Data Factory di Azure |
| 56 |[Caricare dati dall’archiviazione BLOB di Azure in un SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Informazioni su come dati di tooload toouse PolyBase da Azure nell'archiviazione blob in SQL Data Warehouse. Caricare alcune tabelle di dati pubblici nello schema di Data Warehouse di Contoso Retail hello. |
| 57 |[Caricare dati da SQL Server in Azure SQL Data Warehouse (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Utilizza bcp tooexport dati da file tooflat di SQL Server, archiviazione blob di AZCopy tooimport dati tooAzure e dati di PolyBase tooingest hello in Azure SQL Data Warehouse. |
| 58 |[Caricare dati da SQL Server in Azure SQL Data Warehouse (file flat)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Per una dimensione dei dati di piccole dimensioni, utilizza bcp tooexport file tooflat di SQL Server e di importazione hello dati direttamente in Azure SQL Data Warehouse. |
| 59 |[Caricare dati da SQL Server in Azure SQL Data Warehouse (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Viene illustrato come toocreate dati toomove di un pacchetto di SQL Server Integration Services (SSIS) da una vasta gamma di dati origini tooSQL Data Warehouse. |
| 60 |[Caricare dati con PolyBase in SQL Data Warehouse](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Utilizza bcp tooexport dati da file tooflat di SQL Server, archiviazione blob di AZCopy tooimport dati tooAzure e dati di PolyBase tooingest hello in Azure SQL Data Warehouse. |
| 61 |[Guida per l'uso di PolyBase in SQL Data Warehouse](sql-data-warehouse-load-polybase-guide.md) |Linee guida e consigli per l'uso di PolyBase in scenari di SQL Data Warehouse. |
| 62 |[Caricare i dati di esempio in SQL Data Warehouse](sql-data-warehouse-load-sample-databases.md) |Caricare i dati di esempio in SQL Data Warehouse |
| 63 |[Caricare dati con bcp](sql-data-warehouse-load-with-bcp.md) |Informazioni su quali bcp e come toouse per scenari di data warehouse. |
| 64 |[Caricare i dati in Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) |Informazioni su scenari comuni di hello per i dati durante il caricamento in SQL Data Warehouse. Questi includono l'uso di PolyBase, dell’archiviazione BLOB di Azure, di file flat e l’invio dei dischi. È anche possibile usare strumenti di terze parti. |

## <a name="migrate"></a>Migrazione
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 65 |[Eseguire la migrazione del tooSQL codice SQL Data Warehouse](sql-data-warehouse-migrate-code.md) |Suggerimenti per la migrazione del database SQL di codice tooAzure SQL Data Warehouse per lo sviluppo di soluzioni. |
| 66 |[Eseguire la migrazione dei dati](sql-data-warehouse-migrate-data.md) |Suggerimenti per la migrazione del tooAzure di dati SQL Data Warehouse per lo sviluppo di soluzioni. |
| 67 |[Utilità di migrazione per data warehouse (anteprima)](sql-data-warehouse-migrate-migration-utility.md) |Eseguire la migrazione tooSQL Data Warehouse. |
| 68 |[Eseguire la migrazione del tooSQL dello schema del Data Warehouse](sql-data-warehouse-migrate-schema.md) |Suggerimenti per la migrazione del tooAzure schema SQL Data Warehouse per lo sviluppo di soluzioni. |
| 69 |[Eseguire la migrazione del Data Warehouse di tooSQL soluzione](sql-data-warehouse-overview-migrate.md) |Materiale sussidiario di migrazione per portare la piattaforma di soluzione tooAzure SQL Data Warehouse. |

## <a name="partners"></a>Partner
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 70 |[Partner di business intelligence per SQL Data Warehouse](sql-data-warehouse-partner-business-intelligence.md) |Elenco di partner di business intelligence di terze parti con soluzioni che supportano SQL Data Warehouse. |
| 71 |[Partner di integrazione di dati di SQL Data Warehouse](sql-data-warehouse-partner-data-integration.md) |Elenco di partner di terze parti con soluzioni per l'integrazione dei dati che supportano Azure SQL Data Warehouse. |
| 72 |[Partner di gestione di dati di SQL Data Warehouse](sql-data-warehouse-partner-data-management.md) |Elenco di partner di gestione dati di terze parti con soluzioni che supportano SQL Data Warehouse. |

## <a name="reference"></a>riferimento
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 73 |[Argomenti di riferimento per SQL Data Warehouse](sql-data-warehouse-overview-reference.md) |Collegamenti a contenuto di riferimento per SQL Data Warehouse. |
| 74 |[Usare i cmdlet di PowerShell e le API REST con SQL Data Warehouse](sql-data-warehouse-reference-powershell-cmdlets.md) |Trovare hello superiore dei cmdlet di PowerShell per Azure SQL Data Warehouse e come toopause e riprendere un database. |
| 75 |[Elementi del linguaggio](sql-data-warehouse-reference-tsql-language-elements.md) |Elenco di collegamenti tooreference contenuti per elementi del linguaggio Transact-SQL hello utilizzato per SQL Data Warehouse. |
| 76 |[Argomenti Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Contenuto tooreference di collegamenti per gli argomenti di Transact-SQL hello utilizzati da SQL Data Warehouse. |
| 77 |[Viste di sistema](sql-data-warehouse-reference-tsql-system-views.md) |Collegamenti toosystem viste contenuto per SQL Data Warehouse. |

## <a name="security"></a>Sicurezza
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 78 |[SQL Data Warehouse - Supporto client di livello inferiore per controllo e maschera dati dinamica](sql-data-warehouse-auditing-downlevel-clients.md) |Informazioni sul supporto di client di livello inferiore di SQL Data Warehouse per il controllo dati |
| 79 |[Servizio di controllo di Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) |Introduzione al servizio di controllo di Azure SQL Data Warehouse |
| 80 |[Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md) |Transparent Data Encryption (TDE) in SQL Data Warehouse. |
| 81 |[Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Transparent Data Encryption (TDE) in SQL Data Warehouse (T-SQL). |
| 82 |[Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md) |Suggerimenti per proteggere un database in Azure SQL Data Warehouse per lo sviluppo di soluzioni. |

## <a name="miscellaneous"></a>Miscellaneous
| &nbsp; | Titolo | Descrizione |
| ---:|:--- |:--- |
| 83 |[Installare Visual Studio e SSDT per SQL Data Warehouse](sql-data-warehouse-install-visual-studio.md) |Installare Visual Studio e SQL Server Data Tools (SSDT) per Azure SQL Data Warehouse |
| 84 |[Migrazione tooPremium dettagli di archiviazione](sql-data-warehouse-migrate-to-premium-storage.md) |Istruzioni per la migrazione di un'archiviazione toopremium SQL Data Warehouse esistente |
| 85 |[Introduzione al rilevamento delle minacce](sql-data-warehouse-security-threat-detection.md) |La modalità di avvio tooget con funzionalità di rilevamento minacce |
| 86 |[Limiti di capacità di SQL Data Warehouse](sql-data-warehouse-service-capacity-limits.md) |I valori massimi per le connessioni, i database, le tabelle e le query per SQL Data Warehouse. |
| 87 |[Risoluzione dei problemi relativi a SQL Data Warehouse di Azure](sql-data-warehouse-troubleshoot.md) |Risoluzione dei problemi relativi a SQL Data Warehouse di Azure. |

