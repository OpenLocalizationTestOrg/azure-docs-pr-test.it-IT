---
title: lo strumento di valutazione soluzioni di Business Intelligence aaaCortana | Documenti Microsoft
description: "I Partner Microsoft di seguito sono tutti i passaggi di hello toofollow toopublish è necessario il tooAppSource soluzioni di Business Intelligence di Cortana."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Strumento di valutazione delle soluzioni Cortana Intelligence
## <a name="overview"></a>Panoramica
È possibile utilizzare nelle soluzioni avanzate analitica hello Intelligence Cortana soluzione valutazione strumento tooassess per la conformità alle procedure consigliate consigliate da Microsoft. Microsoft è entusiasti toowork con i partner (ISV o SIs) tooprovide soluzioni di alta qualità per i clienti, rivenditori e l'implementazione. Questa Guida verrà illustrata processo hello dell'utilizzo dello strumento di valutazione di hello soluzione con la soluzione e descrivono hello specifiche consigliate nei controlli per.

## <a name="getting-started"></a>introduttiva
. [Scaricare](https://aka.ms/aa-evaluation-tool-download) e installare lo strumento di valutazione di hello Intelligence Cortana soluzione.

Prerequisiti:
- Windows 10: [Sito ufficiale di Windows 10](https://www.microsoft.com/en-us/windows)
- Azure Powershell: [Installare e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).

## <a name="identifying-your-app"></a>Identificazione dell'app
Al termine dell'installazione, aprire lo strumento hello e per iniziare la prima valutazione.

![Aprire lo strumento di valutazione](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Specificare le informazioni di identificazione della soluzione.

![Connettersi alla sottoscrizione di Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Connettersi tooyour sottoscrizione di Azure e fornire il gruppo di risorse contenente l'applicazione hello.

![Selezionare le risorse](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Una volta caricato il gruppo di risorse hello, selezionare le risorse di hello che vengono inclusi nella soluzione e identificano l'accessibilità di hello di tutte le risorse di dati come:
- Ingestion
- Consumo
- Interno

Queste informazioni vengono utilizzate toobetter comprendere come la soluzione utilizza vari componenti e componenti rivolta all'utente tooensure siano coerenti con le procedure consigliate.

### <a name="ingestion"></a>Ingestion
Inserimento significa in questo caso tutte le origini dati che sono toopull utilizzati nei dati di soluzione hello esterno o che tutti i servizi all'esterno di soluzione hello utilizzano toopush al suo interno.

### <a name="consumption"></a>Consumo
In questo caso, il consumo, set di dati sono utilizzati toopush dati tooend, direttamente o indirettamente. ad esempio:
- Set di dati usati in query dirette da Power BI.
- Set di dati sottoposti a query in un'app Web.

>[!NOTE]
Se una risorsa specifica viene usata sia per l'inserimento che per il consumo, scegliere **Consumo**.

### <a name="internal"></a>Interno
Usare Interno per le risorse di dati usate solo nell'elaborazione interna delle applicazioni.

Successivamente, sarà richiesta tooprovide credenziali valide per tutti i database specificati nel passaggio precedente hello:

![Prerequisiti set di test](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Test case per la soluzione
Hello soluzione verrà eseguita una raccolta di test automatizzati nella soluzione.

![Esecuzione set di test](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Al termine dei test di hello, sarà richiesto tooprovide una spiegazione o giustificazione per il motivo per cui la soluzione non è conforme ai requisiti di hello.

![Offrire la giustificazione operativa](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Ad esempio, se la soluzione pubblica tooAzure SQL DW, valutazione hello test richiesto è tooalso pubblicare tooAzure Analysis Services. 

È possibile che la soluzione usi macchine virtuali IaaS che eseguono SQL Server Analysis Services anziché Azure Analysis Services. Questo potrebbe essere un motivo dell'errore del test di hello accettabile.
## <a name="packaging-your-evaluation-results"></a>Gestione dei risultati della valutazione
Dopo aver completato hello test case, il pacchetto di valutazione sarà esportato tooa file con estensione zip e verrà richiesto tooprovide feedback sullo strumento di valutazione di hello. 

È necessario tooshare file zip con Microsoft per toobe la soluzione valutata prima di ottenere l'approvazione toobe aggiunto dei risultati dei test tooAppSource

![Commenti sullo strumento di valutazione](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Sopra la sezione di questo articolo vengono illustrate diverse funzionalità dello strumento hello, ora segnalare il problema, esaminare i tipi di procedure consigliate che restituisce questo strumento.

## <a name="security-evaluation-considerations"></a>Considerazioni sulla valutazione della protezione
### <a name="databases-should-use-azure-active-directory-authentication"></a>I database devono usare l'autenticazione di Azure Active Directory
Alle risorse di SQL Azure o Azure SQL DW hello sloution devono essere abilitate con l'autenticazione di Azure Active Directory (AAD). Azure ad fornisce toomanage un'unica posizione tutti i ruoli e le identità.

| Per altre informazioni su | Vedere questo articolo |
| --- | --- |
| AAD con SQL Database e SQL Data Warehouse | [Usare l'autenticazione di Azure Active Directory per l'autenticazione di un database SQL o di SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Configurare e gestire AAD | [Configurare e gestire l'autenticazione di Azure Active Directory con il database SQL oppure con SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Autenticazione delle app Web di Azure | [Autenticazione e autorizzazione nel servizio app di Azure](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Configurare le app Web con AAD | [Come tooconfigure l'account di accesso Active Directory di Azure di toouse applicazione di servizio App](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Set di dati accessibili tooend gli utenti devono supportare il controllo di accesso basato sui ruoli
Durante l'esecuzione dello strumento di valutazione di hello, sarà richiesto toospecify qualsiasi report o la pubblicazione di risorse. Si presuppone che queste risorse siano destinate all'accesso degli utenti finali e non degli sviluppatori. Queste risorse devono essere consentono il controllo di accesso basato sui ruoli (RBAC) in ordine tooensure che gli utenti finali sono solo in grado di tooaccess autorizzato i dati.

In particolare, una delle seguenti risorse di Azure hello può essere configurata con RBAC e sono considerata accettabile:
- HDInsight protette, vedere [una sicurezza tooHadoop introduzione con una dominio cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- SQL Azure, vedere [AAD authentication with Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) (Autenticazione AAD con SQL Azure)
- Azure Analysis Services, vedere la sezione corrispondente in [Manage database roles and users](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) (Gestire ruoli e utenti di database)
- Azure SQL Data Warehouse (ricordare che SQL DW non è consigliabile per l'accesso diretto degli utenti finali perché supporta RBAC).

Se si utilizza un tipo di risorsa diverso che supporta RBAC, indicare che la giustificazione hello test case.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store deve usare la crittografia dei dati inattivi
Azure Data Lake Store (ADLS) supporta la crittografia dei dati inattivi per impostazione predefinita mediante chiavi di crittografia gestite internamente. È anche possibile configurare la crittografia con Azure Key Vault.

Per informazioni su come specificare le impostazioni di crittografia di ADLS, vedere [Creare un account di Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL e Azure SQL Data Warehouse devono usare la crittografia
Sia Azure SQL che Azure SQL DW supportano Transparent Data Encryption (TDE), che offre la crittografia e la decrittografia in tempo reale di file di dati e file di log.

| Per altre informazioni su | Vedere questo articolo |
| --- | --- |
| Transparent data encryption (TDE) | [Transparent Data Encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL Data Warehouse con TDE | [Introduzione a Transparent Data Encryption (TDE)](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Configurare Azure SQL con TDE | [Transparent Data Encryption con il database SQL di Azure](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Configurare Azure SQL con Always Encrypted | [Always Encrypted: proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia in Azure Key Vault](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Inoltre tooTDE, SQL Azure supporta anche crittografia sempre attiva, una nuova tecnologia di crittografia di dati che assicura che i dati vengono crittografati non solo a riposo e durante lo spostamento tra client e server, ma anche durante i dati non è in uso durante l'esecuzione di comandi nel server di hello.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Tutte le macchine virtuali devono essere distribuiti da hello Azure Marketplace
In ordine tooprovide un livello di sicurezza tra AppSource coerente, è necessario che tutte le macchine virtuali distribuite come parte di una soluzione di Business Intelligence di Cortana essere certificate e pubblicate su hello Azure Marketplace.

elenco corrente di hello toosearch di immagini di Azure Marketplace, vedere [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Per informazioni su come toopublish immagine di una macchina virtuale per Azure Marketplace, vedere [toocreate Guida un'immagine di macchina virtuale per hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Considerazioni per la valutazione della scalabilità
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Le soluzioni Cortana Intelligence devono includere una piattaforma Big Data scalabile
Soluzioni di Business Intelligence di Cortana dovrebbero essere scalato toovery formati di dati di grandi dimensioni. In Azure, ciò significa che deve includere una delle due piattaforme di dati su scala Petabyte hello:
- Archivio Azure Data Lake
- Azure SQL Data Warehouse

Se la soluzione non richiedono il supporto per le dimensioni dei dati o se si utilizza una piattaforma di dati alternativi, illustrata in giustificazione di hello test case.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Le soluzioni Cortana Intelligence devono includere ambienti di dati dedicati per l'inserimento
In genere è consigliabile evitare che le soluzioni Cortana Intelligence inseriscano direttamente dati in origini dati relazionali. I dati non elaborati dovranno essere archiviati in un ambiente non strutturato, con inserimenti/aggiornamenti idempotent in qualsiasi archivio relazionale mediante Azure Data Factory.

Per altre informazioni sulla copia di dati con Azure Data Factory, vedere [Esercitazione: Creare una pipeline con l’attività Copia usando Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Azure SQL Data Warehouse deve usare PolyBase per l'inserimento di dati
Azure SQL Data Warehouse supporta PolyBase, che dispone di modalità di inserimento dati altamente scalabili e in parallelo. PolyBase consente toouse Azure SQL DW tooissue query set di dati esterni archiviati in archiviazione Blob di Azure o archivio Azure Data Lake. Questo offre prestazioni superiori tooalternative metodi di aggiornamenti in blocco.

Per un'introduzione all'uso di PolyBase con Azure SQL Data Warehouse, vedere [Caricare dati con PolyBase in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Per informazioni sulle procedure consigliate con PolyBase e Azure SQL Data Warehouse, vedere [Guida per l'uso di PolyBase in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Considerazioni per la valutazione della disponibilità

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Gli utenti tooend accessibile di set di dati devono supportare un volume elevato di utenti simultanei
Durante l'esecuzione dello strumento di valutazione di hello, sarà richiesto toospecify qualsiasi report o la pubblicazione di risorse. Si presuppone che queste risorse siano destinate all'accesso degli utenti finali e non degli sviluppatori. Queste risorse devono supportare un numero medio/grande di utenti simultanei.

In particolare, Azure SQL Data Warehouse non deve essere agli utenti di hello dati unica origine tooend disponibili. Se il data Warehouse di SQL Azure viene fornito come risorsa per Power Users, Azure Analysis Services devono essere apportate agli utenti di tootypical disponibili.

Per altre informazioni sui limiti di concorrenza di Azure SQL DW, vedere [Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Per altre informazioni su Azure Analysis Services, vedere [Informazioni su Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Le risorse Azure SQL devono avere una replica di sola lettura per il failover
Database SQL di Azure supportano le istanze secondarie tooa replica geografica. Questa istanza può quindi essere utilizzata come applicazioni a disponibilità elevata un failover istanza tooprovide.

Per altre informazioni sulla replica geografica per i database SQL di Azure, vedere [Panoramica: gruppi di failover e replica geografica attiva](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Per istruzioni sulla replica geografica tooconfigure per SQL Azure, vedere [configurare la replica geografica attiva per il Database di SQL Azure con Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Azure SQL Data Warehouse deve avere i backup con ridondanza geografica attivati
Data Warehouse di SQL Azure supporta l'archiviazione con ridondanza toogeo backup giornaliero. Questa replica geografica modo che è possibile ripristinare data warehouse di hello anche in situazioni in cui non è possibile accedere snapshot archiviati nell'area primaria. Questa funzionalità è attivata per impostazione predefinita e non deve essere disattivata per le soluzioni Cortana Intelligence.

Per altre informazioni su backup e ripristino in Azure SQL DW, vedere [Backup di SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Le macchine virtuali devono essere configurate in set di disponibilità
Macchine virtuali di Azure deve essere configurate in set di disponibilità in impatto hello toominimize di ordine di eventi di manutenzione pianificate e non pianificate.

Per ulteriori informazioni sulla disponibilità delle macchine virtuali di Azure, vedere [gestione hello disponibilità delle macchine virtuali di Windows in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Altre considerazioni per la valutazione
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Le applicazioni Cortana Intelligence devono usare uno strumento centralizzato per l'orchestrazione dei dati
L'uso di un unico strumento per la gestione e la pianificazione dello spostamento e della trasformazione dei dati garantisce la coerenza per i dati di importanza critica. Questo approccio garantisce logica chiara intorno alla logica di retry, gestione delle dipendenze, avvisi/registrazione e così via. È consigliabile utilizzare hello di [Data Factory di Azure](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) per l'orchestrazione di dati in Azure.

Se si usa uno strumento diverso da Azure Data Factory per l'orchestrazione di dati, descrivere lo strumento o gli strumenti in uso.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>È necessario ripetere il training dei modelli di Azure Machine Learning con Azure Data Factory
Azure Machine Learning (Azure ml) fornisce strumenti di facile toouse per hello creazione e la distribuzione di modellazione predittiva e machine learning pipeline. Tuttavia, è importante che le distribuzioni di produzione di questi modelli di Azure ml non è basato su un singolo set di dati predefinito, ma invece adatta toohello spostando dynamics di fenomeni del mondo reale.

Per informazioni sulla creazione di servizi Web per la ripetizione del training in AzureML, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Per ulteriori informazioni sull'automazione di processo di training del modello hello usando Azure Data Factory, vedere [modelli di aggiornamento di Azure Machine Learning utilizzando l'attività della risorsa di aggiornamento](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Documentazione esistente
[Microsoft Azure Certified toogrow azienda cloud](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Certified per Cortana Intelligence](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

