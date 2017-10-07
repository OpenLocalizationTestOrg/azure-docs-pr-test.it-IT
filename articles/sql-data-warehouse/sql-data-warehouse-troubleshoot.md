---
title: Azure SQL Data Warehouse aaaTroubleshooting | Documenti Microsoft
description: Risoluzione dei problemi relativi a SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Risoluzione dei problemi relativi a SQL Data Warehouse di Azure
Questo argomento sono elencati alcuni dei hello domande sulla risoluzione dei problemi più comuni dei clienti.

## <a name="connecting"></a>Connessione
| Problema | Risoluzione |
|:--- |:--- |
| Accesso non riuscito per l'utente 'NT AUTHORITY\ANONYMOUS LOGON'. (Microsoft SQL Server, Errore: 18456) |Questo errore si verifica quando un utente AAD tooconnect toohello master database di prova, ma non dispone di un utente nel database master.  Questo problema specificare toocorrect hello SQL Data Warehouse si desiderano tooconnect tooat tempi di connessione o si aggiunta database master di hello utente toohello.  Per altri dettagli, vedere l'articolo [Panoramica della sicurezza][Security overview]. |
| server Hello "Nomeutente" principale non è in grado di tooaccess hello database "master" nel contesto di sicurezza corrente hello. Impossibile aprire il database predefinito dell'utente. Accesso non riuscito. Accesso non riuscito per l'utente 'MyUserName'. (Microsoft SQL Server, Errore: 916) |Questo errore si verifica quando un utente AAD tooconnect toohello master database di prova, ma non dispone di un utente nel database master.  Questo problema specificare toocorrect hello SQL Data Warehouse si desiderano tooconnect tooat tempi di connessione o si aggiunta database master di hello utente toohello.  Per altri dettagli, vedere l'articolo [Panoramica della sicurezza][Security overview]. |
| Errore CTAIP |Questo errore può verificarsi quando un account di accesso è stato creato nel database master hello SQL server, ma non nel database di SQL Data Warehouse hello.  Se si verifica questo errore, esaminare hello [Cenni preliminari sulla sicurezza] [ Security overview] articolo.  Questo articolo spiega toocreate come creare un account di accesso e un utente sul master e quindi come toocreate un utente in hello database SQL Data Warehouse. |
| Blocco da parte del firewall |Database SQL di Azure sono protetti da tooensure di firewall di livello server e database noti solo gli indirizzi IP sono database di access tooa. i firewall Hello sono protette per impostazione predefinita, il che significa che è necessario abilitare in modo esplicito e indirizzo IP o l'intervallo di indirizzi prima di poter connettere.  tooconfigure il firewall per l'accesso, seguire i passaggi hello [configurare l'accesso al server di firewall per l'indirizzo IP del client] [ Configure server firewall access for your client IP] in hello [Provisioning istruzioni] [Provisioning instructions]. |
| Impossibile connettersi con lo strumento o il driver |Consiglia l'utilizzo di SQL Data Warehouse [SSMS][SSMS], [SSDT per Visual Studio][SSDT for Visual Studio], o [sqlcmd] [ sqlcmd] tooquery i dati. Per ulteriori informazioni sul driver e tooSQL connessione Data Warehouse, vedere [driver per Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] e [connettersi tooAzure SQL Data Warehouse] [ Connect tooAzure SQL Data Warehouse] articoli. |

## <a name="tools"></a>Strumenti
| Problema | Risoluzione |
|:--- |:--- |
| Esplora oggetti di Visual Studio non riconosce gli utenti di AAD |Questo è un problema noto.  In alternativa, consente di visualizzare gli utenti di hello [Sys. database_principals][sys.database_principals].  Vedere [tooAzure l'autenticazione SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn ulteriori informazioni sull'utilizzo di Azure Active Directory con SQL Data Warehouse. |
|Manuale di scripting, guidata scripting hello o la connessione tramite SQL Server Management Studio è lenti, bloccati o produzione errori| Assicurarsi che gli utenti siano stati creati nel database master hello. Nelle opzioni di scripting, assicurarsi che l'edizione del motore di hello è impostato come "Microsoft Azure SQL Data Warehouse Edition" e tipo di motore è "Database SQL di Microsoft Azure".|

## <a name="performance"></a>Prestazioni
| Problema | Risoluzione |
|:--- |:--- |
| Risoluzione dei problemi di prestazioni delle query |Se si sta tentando una particolare query tootroubleshoot, iniziare con [apprendimento come toomonitor query][Learning how toomonitor your queries]. |
| Piani e prestazioni delle query di scarsa qualità sono spesso causati dalla mancanza di statistiche |causa più comune di Hello di una riduzione delle prestazioni è la mancanza di statistiche per le tabelle.  Vedere [gestione delle statistiche sulla tabella] [ Statistics] per informazioni dettagliate su come statistiche toocreate e perché sono critici tooyour prestazioni. |
| Concorrenza bassa/query in coda |Informazioni sui [del carico di lavoro] [ Workload management] è importante in ordine toounderstand come toobalance l'allocazione della memoria con la modalità simultanea. |
| Come tooimplement procedure consigliate |sono Hello migliore sul posto toostart toolearn modi tooimprove le prestazioni delle query [le procedure consigliate di SQL Data Warehouse] [ SQL Data Warehouse best practices] articolo. |
| Come tooimprove prestazioni con scalabilità |In alcuni casi tooimproving le prestazioni della soluzione hello sono toosimply aggiungere più query tooyour potenza di calcolo [scalabilità il Data Warehouse SQL][Scaling your SQL Data Warehouse]. |
| Scarse prestazioni delle query a causa di scarsa qualità degli indici |A volte le query possono rallentare a causa della [scarsa qualità degli indici columnstore][Poor columnstore index quality].  Vedere l'articolo per altre informazioni e come troppo[Ricompila indici qualità segmento tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Gestione del sistema
| Problema | Risoluzione |
|:--- |:--- |
| Msg 40847: Impossibile eseguire l'operazione hello perché il server avrebbe superato hello quota di unità di transazione di Database di 45000 è consentito. |Ridurre hello [DWU] [ DWU] del database hello che si sta tentando di toocreate o [richiedere un aumento della quota][request a quota increase]. |
| Analisi dell'uso dello spazio |Vedere [tabella dimensioni] [ Table sizes] utilizzo dello spazio di hello toounderstand del sistema. |
| Aiuto nella gestione delle tabelle |Vedere hello [Cenni preliminari su tabella] [ Overview] articolo per informazioni sulla gestione delle tabelle.  Questo articolo contiene anche collegamenti ad articoli più dettagliati, ad esempio relativi a [tipi di dati delle tabelle][Data types], [distribuzione di una tabella][Distribute], [indicizzazione di una tabella][Index],  [partizionamento di una tabella][Partition], [gestione delle statistiche delle tabelle][Statistics] e [tabelle temporanee][Temporary]. |
|Barra di avanzamento di Transparent data encryption (TDE) non viene aggiornata in hello portale di Azure|È possibile visualizzare lo stato di hello di Transparent Data Encryption tramite [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>PolyBase
| Problema | Risoluzione |
|:--- |:--- |
| Caricamento non riuscito a causa di un elevato numero di righe |Attualmente PolyBase non supporta un elevato numero di righe.  Ciò significa che se la tabella contiene varchar (max), nvarchar (max) o varbinary (max), le tabelle esterne non possono essere utilizzati tooload i dati.  Carica per le righe di grandi dimensioni è attualmente supportata solo tramite Data Factory di Azure (con BCP), Azure flusso Analitica, SSIS, BCP o hello classe .NET SQLBulkCopy. Il supporto di un elevato numero di righe in PolyBase verrà aggiunto in una versione futura. |
| Esito negativo del caricamento bcp della tabella con tipo di dati MAX |Si verifica un problema noto che richiede che venga inserito varchar (max), nvarchar (max) o varbinary (max) alla fine di hello della tabella hello in alcuni scenari.  Provare a spostare la fine di toohello MAX colonne della tabella hello. |

## <a name="differences-from-sql-database"></a>Differenze rispetto al database SQL
| Problema | Risoluzione |
|:--- |:--- |
| Funzionalità non supportate del database SQL |Vedere [Funzionalità non supportate delle tabelle][Unsupported table features]. |
| Tipi di dati non supportati del database SQL |Vedere [Tipi di dati non supportati][Unsupported data types]. |
| Limitazioni DELETE e UPDATE |Vedere [soluzioni alternative aggiornamento][UPDATE workarounds], [soluzioni alternative DELETE] [ DELETE workarounds] e [toowork utilizzando un'istruzione CTAS intorno a un aggiornamento non supportato e Sintassi DELETE][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Istruzione MERGE non supportata |Vedere [Soluzioni alternative MERGE][MERGE workarounds]. |
| Limitazioni delle stored procedure |Vedere [archiviati limitazioni procedure] [ Stored procedure limitations] toounderstand hello limitazioni delle stored procedure. |
| Le UDF non supportano istruzioni SELECT |Si tratta di una limitazione corrente delle UDF.  Vedere [CREATE FUNCTION] [ CREATE FUNCTION] per la sintassi di hello è supportato. |

## <a name="next-steps"></a>Passaggi successivi
Se si trattasse di toofind non è possibile un problema di tooyour soluzione sopra, di seguito sono riportate altre risorse, è possibile provare.

* [Blog]
* [Richieste di funzionalità]
* [Video]
* [Blog del team CAT]
* [Creare un ticket di supporto]
* [Forum MSDN]
* [Forum su Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Creare un ticket di supporto]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blog]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blog del team CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Richieste di funzionalità]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Forum su Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Video]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
