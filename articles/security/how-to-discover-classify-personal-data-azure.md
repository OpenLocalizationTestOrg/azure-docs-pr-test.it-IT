---
title: aaaDiscover, identificare e classificare i dati personali in Microsoft Azure | Documenti Microsoft
description: Informazioni sulla ricerca, la classificazione, l'individuazione e l'identificazione di dati
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Individuare, identificare e classificare i dati personali in Microsoft Azure

In questo articolo vengono fornite indicazioni su come toodiscover, identificare e classificare i dati personali in diversi strumenti di Azure e servizi, incluso l'uso di Azure Data Catalog, Azure Active Directory, Database SQL, Power Query per i cluster Hadoop in HDInsight di Azure, Azure Query di Information Protection, ricerca di Azure e SQL di Azure Cosmos DB.

## <a name="scenario-problem-statement-and-goal"></a>Scenario, presentazione del problema e obiettivo

Una società sportiva statunitense raccoglie una varietà di dati personali e di altro tipo, tra cui quelli relativi a clienti e dipendenti. società Hello li mantiene in più database e lo archivia in diverse posizioni nel proprio ambiente Azure. Inoltre tooselling Sport apparecchiature, inoltre ospitare e gestire la registrazione degli eventi sportivi importanti mondo hello, inclusi in Europa, hello e in hello alcuni casi i dati dei clienti che raccolti includono informazioni mediche.

Poiché società hello ospita molte tours bicycling internazionali ogni anno e ha lo staff nelle posizioni in tutto il mondo hello, un paio di hello dei set di dati sono molto grandi. società Hello ha anche le applicazioni compilate per sviluppatori utilizzate dai clienti e dipendenti.

società Hello desidera hello tooaddress seguenti problemi:

- Dati personali di clienti e dipendenti devono essere classificati/distinto da hello altre società di hello dati raccoglie in ordine tooensure corretto accesso e protezione.
- Hello dati necessari tooeasily per individuare il percorso di hello dei dati personali dei clienti in varie aree di hello ambiente Azure.
- Dati personali di clienti e dipendenti che viene visualizzato in documenti condivisi e le comunicazioni di posta elettronica devono essere identificate toohelp assicurarsi che venga mantenuto sicura.
- gli sviluppatori di app della società Hello devono una ricerca tooeasily modo per i dati personali a clienti e dipendenti nel proprio web e App per dispositivi mobili.
- Gli sviluppatori devono inoltre tooquery i database di documenti per i dati personali.

### <a name="company-goals"></a>Obiettivi dell'azienda

- Tutti i dati personali di clienti e dipendenti devono essere contrassegnati/annotati in Azure Data Catalog in modo da consentirne una facile individuazione. Preferibilmente i dati personali di clienti e dipendenti vengono contrassegnati o annotati separatamente.
- È necessario che i dati personali contenuti nei profili utente e le informazioni sull'ufficio di clienti e dipendenti che risiedono in Azure Active Directory siano facilmente individuabili.
- È necessario poter eseguire facilmente query sui dati personali presenti in più database SQL. 
- Alcune grandi set di dati della società hello vengono gestite tramite Azure HDInsight e archiviati in Hadoop. Per poter eseguire query sui dati personali, i dati devono essere importati in Excel.
- I dati personali condivisi nei documenti e nelle comunicazioni via e-mail devono essere classificati, etichettati e protetti con Azure Information Protection.
- Hello agli sviluppatori di app della società devono essere in grado di toodiscover clienti e dipendenti dati personali nelle App hello che una volta compilato, che si può fare con ricerca di Azure.
- Gli sviluppatori devono essere in grado di toofind dati personali nel corrispondente database di documento.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: individuazione di dati

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) è un servizio Microsoft per la gestione delle identità e delle directory multi-tenant, basato sul cloud. È possibile individuare i clienti e dipendenti profili utente e le informazioni utente lavoro che contengono dati personali nel [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) ambiente (AAD) utilizzando hello [portale di Azure](https://portal.azure.com/).

Ciò è particolarmente utile se si desidera toofind o modificare i dati personali per un utente specifico. È possibile anche aggiungere o modificare il profilo utente e le informazioni sull'ufficio. È necessario accedere con un account che sia un amministratore globale per la directory di hello.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Come è possibile individuare o visualizzare il profilo utente e le informazioni sull'ufficio?

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.

2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![come individuare le informazioni sul profilo utente e sull'ufficio](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. In hello **utenti e gruppi** pannello seleziona **utenti**.

  ![Apertura del pannello Utenti e gruppi](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. In hello **utenti e gruppi di utenti -** pannello selezionare un utente dall'elenco di hello, quindi, nel Pannello di hello per l'utente selezionato hello, **profilo** tooview informazioni del profilo utente che potrebbero contenere dati personali .

  ![Seleziona utente](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Se è necessario tooadd o modificare informazioni del profilo utente, è possibile eseguire questa operazione e quindi nella barra dei comandi di hello, selezionare **salvare.**
6. Nel Pannello di hello per l'utente selezionato hello, selezionare **Info lavoro** tooview lavoro le informazioni utente che possono contenere dati personali.

 ![visualizzazione delle informazioni sull'ufficio](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Se è necessario tooadd o modificare le informazioni di lavoro utente, è possibile eseguire questa operazione e quindi nella barra dei comandi di hello, selezionare **salvare.**

## <a name="azure-sql-database-data-discovery"></a>Database SQL di Azure: individuazione di dati

Il [database SQL di Microsoft Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) è un database basato su cloud che consente agli sviluppatori di compilare e gestire le applicazioni. I dati personali sono reperibili nel [database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando le query SQL standard. Azure elastico nella query SQL (anteprima) consente di eseguire query tra database di tooperform di utenti.

Dettagliate [database SQL](../sql-database/sql-database-technical-overview.md) esercitazione illustra molti aspetti dell'utilizzo di un database SQL, compresa la modalità toobuild uno e come toorun query dei dati. di seguito Hello è un riepilogo delle informazioni di hello disponibili nell'esercitazione hello con sezioni toospecific collegamenti.

### <a name="how-do-i-build-a-sql-database"></a>Come si compila un database SQL?

Esistono tre modi toodo è:

- È possibile creare un database SQL di Azure in hello [portale di Azure](https://portal.azure.com/). Nell'esercitazione di hello, si userà un set specifico di risorse di calcolo e archiviazione all'interno di un gruppo di risorse e il server logico. Si useranno i dati di esempio di una società fittizia, AdventureWorks. Verrà anche creata una regola del firewall a livello di server. toolearn come toodo hello, visitare [creare un database SQL di Azure nel portale di Azure hello](../sql-database/sql-database-get-started-portal.md) esercitazione.

  ![Creare un database SQL di Azure](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Un database SQL può essere creato anche in hello [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, uno strumento da riga di comando basata su browser. strumento Hello è disponibile nel portale di Azure hello e può essere eseguito direttamente da questa posizione. In questa esercitazione, avviare lo strumento di hello, definire le variabili dello script, creare un gruppo di risorse e il server logico e configurare una regola firewall del server. Creare quindi un database con dati di esempio. toolearn come toocreate il database in questo modo, visitare hello [creare un singolo database di SQL Azure mediante Azure CLI hello](../sql-database/sql-database-get-started-cli.md) esercitazione.

  ![Esercitazione sull'interfaccia della riga di comando](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Gli sviluppatori e gli amministratori di Linux usano in genere l'interfaccia della riga di comando di Azure. Alcuni utenti la considerano più semplice e intuitiva della terza opzione: PowerShell.

- Infine, è possibile creare un database SQL tramite PowerShell, ovvero un toocreate strumento della riga di comando o script e gestire Azure e altre risorse. In questa esercitazione, avviare lo strumento di hello, definire le variabili dello script, creare un gruppo di risorse e il server logico e configurare una regola firewall del server. Si creerà quindi un database con dati di esempio.

esercitazione Hello richiede hello Azure PowerShell versione 4.0 o versione successiva del modulo. Eseguire Get-Module - ListAvailable AzureRM toofind la versione in uso. Se è necessario tooinstall o l'aggiornamento, vedere il modulo di installare Azure PowerShell.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn come toocreate il database in questo modo, visitare hello [creare un singolo database di SQL Azure con Powershell](../sql-database/sql-database-get-started-powershell.md) esercitazione.

>[!Note]
Gli amministratori Windows tendono toouse PowerShell, ma alcuni di essi preferibile CLI di Azure.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Come è possibile cercare i dati personali nel database SQL nel portale di Azure hello? * *

È possibile utilizzare lo strumento di editor di query incorporata hello all'interno di hello toosearch portale Azure per i dati personali. Si sarà accedere nello strumento toohello utilizzando l'account di amministratore di accesso SQL server e la password e quindi immettere una query.

  ![eseguire la ricerca tramite il portale di hello sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Passaggio 5 dell'esercitazione hello Mostra un esempio di query nel riquadro dell'editor di query hello, ma non lo stato attivo si informazioni sensibili o personali (inoltre combina i dati da due tabelle e crea gli alias per la colonna di origine hello nel set di dati hello restituito). Hello schermata riportata di seguito viene illustrata hello query dal passaggio 5, nonché hello riquadro dei risultati restituiti:

  ![Editor di query](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Se il database è stato chiamato MyTable, una query di esempio per le informazioni personali può includere nome, numero di previdenza sociale e numero di ID e sarà simile alla seguente:

"SELECT Name, SSN, ID number FROM MyTable"

È necessario eseguire query di hello e quindi visualizzare i risultati di hello nella hello **risultati** riquadro.

Per ulteriori informazioni su come tooquery un SQL database hello portale di Azure, visitare hello [database SQL di Query hello](../sql-database/sql-database-get-started-portal.md) sezione dell'esercitazione hello.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Come cercare i dati in più database?

Query elastica SQL (anteprima) consente di più query di database e si tooperform tra database e restituire un singolo risultato. Hello [esercitazione Panoramica](../sql-database/sql-database-elastic-query-overview.md) include una descrizione dettagliata degli scenari e viene illustrata la differenza hello tra il partizionamento verticale e orizzontale del database. Il partizionamento orizzontale è chiamato "sharding".

  ![Il partizionamento verticale](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![partizionamento orizzontale](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget avviato, visitare hello [panoramica delle query elastico Database SQL di Azure (anteprima)](../sql-database/sql-database-elastic-query-overview.md) pagina.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query per l'importazione di cluster Azure HDInsight Hadoop: individuazione di dati per set di dati di grandi dimensioni

Hadoop è un servizio di archiviazione ed elaborazione Apache open source per set di dati di grandi dimensioni, che vengono analizzati e archiviati in cluster Hadoop. [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) consente agli utenti toowork con Hadoop cluster in Azure. Power Query è un componente aggiuntivo per Excel che, tra le altre cose, consente agli utenti di individuare i dati da origini diverse.

Dati personali associati a cluster Hadoop in HDInsight di Azure possono essere importato tooExcel con Power Query. Una volta hello dati in Excel è possibile utilizzare una query tooidentify è.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Utilizzo di cluster Hadoop tooimport Excel Power Query in Azure HDInsight in Excel?

Un'esercitazione HDInsight illustra l'intero processo. Illustra i prerequisiti e include un collegamento di tooa [Guida introduttiva di Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) esercitazione. Istruzioni illustrano Excel 2016, nonché 2013 e 2010 (passaggi sono leggermente diversi per le versioni precedenti di Excel hello). Se non si dispone di componente aggiuntivo Excel Power Query hello, hello esercitazione viene illustrato come tooget è. Si inizierà esercitazione hello in Excel e sarà necessario toohave un account di archiviazione Blob di Azure associato al cluster.

  ![Eseguire query in Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn come toodo hello, visitare [tooHadoop Excel connettersi tramite Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) esercitazione.

Origine: [tooHadoop Excel Connetti tramite Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: classificazione dei dati personali per i documenti e i messaggi di posta elettronica

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) consente ai clienti di Azure si applicano tooclassify etichette e proteggere i documenti condivisi internamente o esternamente e le comunicazioni di posta elettronica. Alcuni di questi elementi possono contenere informazioni personali di clienti o dipendenti. Le regole e le condizioni possono essere definite automaticamente o manualmente dagli amministratori o dagli utenti. Ad esempio, se un utente salva un documento che include informazioni di carta di credito, egli vedrà un suggerimento di etichetta che è stato configurato dall'amministratore di hello.

### <a name="how-do-i-try-it"></a>Come si esegue una prova?

Se si desidera toogive Azure Information Protection toosee un blocco try, potrebbe essere un adattamento per l'organizzazione, visitare la pagina hello [esercitazione rapida](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Contiene cinque passaggi base, ovvero dall'installazione tooconfiguring criteri tooseeing classificazione, aggiunta di etichette e la condivisione in azione: e deve accettare inferiore a mezz'ora.

### <a name="how-do-i-deploy-it"></a>Come si esegue la distribuzione?

Se si desidera toodeploy Azure Information Protection per l'organizzazione, visitare la pagina hello [Guida alla distribuzione per la classificazione, aggiunta di etichette e protezione](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Quali altre informazioni è necessario conoscere?

Per informazioni complementari che consentono di valutare come tooset, configurarlo, visitare hello [pronto, set, proteggere!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
. E controllo hello ulteriori collegamenti elencati di seguito per ulteriori informazioni su Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Ricerca di Azure: individuazione di dati per le app di sviluppatori

[Ricerca di Azure](https://azure.microsoft.com/services/search/) è una soluzione di ricerca basata su cloud per gli sviluppatori che offre un'esperienza di ricerca avanzata di dati per le applicazioni. Ricerca di Azure consente toolocate dati tra gli indici definiti dall'utente, originati da database di installazione di Azure, Database SQL di Azure, archiviazione Blob di Azure, archiviazione tabelle di Azure o per i clienti personalizzata dati JSON. È anche possibile strutturare query Lucene utilizzando hello toosearch di API REST di ricerca di Azure per i tipi di dati personali hello dati personali o di altre persone. Le funzionalità includono la ricerca full-text, una semplice sintassi di query e la sintassi di query Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Utilizzo di dati SQL tooquery

toobegin con i concetti di base hello visitare hello [DB CosmosD Azure: modalità tooquery utilizzando SQL](../cosmos-db/tutorial-query-documentdb.md) esercitazione. esercitazione Hello fornisce un documento di esempio e due esempi di query SQL e risultati.

Per altre informazioni dettagliate sulla creazione di query SQL, visitare [Query SQL per l'API DocumentDB di Azure Cosmos DB](../cosmos-db/documentdb-sql-query.md).

Se si sta tooAzure nuova DB Cosmos e sarebbe simile toolearn come toocreate un database, aggiungere una raccolta e aggiungere dati, visitare hello [DB Cosmos Azure: creare un'app web API DocumentDB](../cosmos-db/create-documentdb-dotnet.md) esercitazione di avvio rapido. Se si desidera toodo in un linguaggio diverso da .NET, ad esempio Java o Python, selezionare solo la lingua preferita dopo aver toohello sito.

## <a name="next-steps"></a>Passaggi successivi

[Database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50)

[Informazioni sul database SQL](../sql-database/sql-database-technical-overview.md)

[SQL Database Query Editor available in Azure portal] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Che cos'è Azure Information Protection?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Che cos'è Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/) (Azure Information Protection: Una soluzione immediata per la protezione)
