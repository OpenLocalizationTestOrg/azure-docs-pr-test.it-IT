---
title: aaaIntroduction tooData Factory, un servizio di integrazione dati | Documenti Microsoft
description: "Informazioni su Azure Data Factory: è un servizio di integrazione dei dati cloud che consente di orchestrare e automatizzare lo spostamento e la trasformazione dei dati."
keywords: "integrazione dei dati, integrazione dei dati cloud, che cos'è azure data factory"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Introduzione tooAzure Data Factory 
## <a name="what-is-azure-data-factory"></a>Che cos'è Azure Data Factory?
In HelloWorld dei big data, come viene dati esistenti usati in azienda? È possibile tooenrich dati generati nel cloud hello utilizzando dati di riferimento da origini dati locali o altre origini dati diverse? Ad esempio, una società di gioco raccoglie molti log di prodotti da giochi nel cloud hello. Desidera tooanalyze informazioni toogain questi registri toocustomer preferenze, i dati demografici, il comportamento di utilizzo opportunità di offerte speciali e cross-selling di tooidentify e così via, sviluppare nuove interessanti crescita toodrive delle funzionalità e fornire un'esperienza migliore toocustomers. 

tooanalyze questi registri, società hello necessita di dati di riferimento di hello toouse, ad esempio informazioni sui clienti, informazioni di gioco, informazioni in un archivio dati locale campagna di marketing. Pertanto, società di hello vuole tooingest dati del log dall'archivio dati di cloud hello e dati di riferimento da archivio dati locale di hello. Quindi, elaborare i dati hello con Hadoop in hello cloud (Azure HDInsight) e pubblicano i risultati di hello archivio dati in un data warehouse di cloud, ad esempio Azure SQL Data Warehouse o un dati locali, ad esempio SQL Server. Nell'esempio toorun questo flusso di lavoro settimanale di una volta. 

È necessario è una piattaforma che consente a un flusso di lavoro può inserire dati on-premise e archivi dati cloud e i dati di trasformazione o un processo mediante i servizi di calcolo esistente, ad esempio Hadoop e pubblicare hello risultati tooan locale hello aziendale toocreate o archivio dati cloud per tooconsume applicazioni di Business Intelligence. 

![Panoramica di Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory è hello piattaforma per questo tipo di scenari. Si tratta di un **servizio di integrazione di dati basato su cloud che consente di toocreate basati sui dati dei flussi di lavoro nel cloud hello per gestire e automatizzare lo spostamento dei dati e la trasformazione dei dati**. Utilizza Data Factory di Azure, è possibile creare e pianificare basati sui dati dei flussi di lavoro (denominati pipeline) che possono caricare dati da archivi dati diversi, processo/trasformare dati hello utilizzando i servizi di calcolo, ad esempio Azure HDInsight Hadoop, Spark, Azure Data Lake Analitica e Azure Machine Learning e pubblicare dati toodata Archivia, ad esempio Azure SQL Data Warehouse per tooconsume applicazioni di business intelligence (BI) di output.  

È più una piattaforma di estrazione e caricamento (Extract-and-Load, EL) e quindi di trasformazione e caricamento (Transform-and-Load, TL) che una piattaforma di estrazione, trasformazione e caricamento (Extract-Transform-and-Load, ETL) tradizionale. trasformazioni di Hello che vengono eseguite vengono tootransform/elaborare i dati utilizzando i servizi di calcolo, anziché derivato di trasformazioni tooperform come hello quelli per l'aggiunta di colonne, il conteggio del numero di righe, l'ordinamento dei dati e così via. 

Attualmente, in Data Factory di Azure, dati hello che vengano utilizzati e prodotti dai flussi di lavoro sono **sezionati ora dati** (oraria, giornaliera, settimanale, ecc.). Una pipeline può ad esempio leggere i dati di input, elaborare i dati e generare dati di output una volta al giorno. È anche possibile eseguire un flusso di lavoro solo una volta.  
  

## <a name="how-does-it-work"></a>Come funziona? 
le pipeline Hello (flussi di lavoro basati su dati) in Azure Data Factory in genere eseguono hello tre passaggi:

![Le tre fasi di Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Connettersi e raccogliere
Le aziende hanno dati di tipi diversi in origini differenti. primo passaggio nella creazione di un sistema di produzione informazioni Hello è tooconnect tooall hello necessarie origini dati e l'elaborazione, ad esempio servizi SaaS, servizi web FTP, condivisioni di file e spostare hello dati tooa esigenze centralizzata per successive l'elaborazione.

Senza Data Factory, le aziende devono compilare componenti lo spostamento dei dati personalizzati o scrivere servizi personalizzati toointegrate queste origini dati e l'elaborazione. È toointegrate costosa e hardware e gestire tali sistemi, e spesso manca il livello aziendale hello di monitoraggio e avviso e i controlli di hello che offerta un servizio completamente gestito.

Con Data Factory, è possibile utilizzare hello attività di copia in una pipeline di dati toomove dati da sia in locale e cloud di origine dati archivi tooa centralizzazione come archivio dati cloud hello per un'ulteriore analisi. Ad esempio, è possibile raccogliere dati in un archivio Azure Data Lake e trasformare i dati di hello in un secondo momento utilizzando un servizio di calcolo di Azure Data Lake Analitica. oppure raccogliere i dati in un archivio BLOB di Azure e quindi trasformarli usando un cluster Hadoop Azure HDInsight.

### <a name="transform-and-enrich"></a>Trasformare e arricchire
Una volta dati sono presenti in un archivio dati centralizzata nel cloud hello, si desidera hello raccolti dati toobe elaborato o trasformati utilizzando i servizi di calcolo, ad esempio HDInsight Hadoop, Spark, Data Lake Analitica e Machine Learning. Tooreliably trasformata produrre dati desiderata in ambienti di produzione toofeed una pianificazione controllata e gestibile con dati attendibili. 

### <a name="publish"></a>Pubblica 
Fornire i dati trasformati dal cloud hello origini tooon locali come SQL Server oppure mantenerla in cloud di origini di archiviazione per l'utilizzo con la business intelligence (BI) e gli strumenti di analitica e altre applicazioni.

## <a name="key-components"></a>Componenti chiave
Una sottoscrizione di Azure può includere una o più istanze di Azure Data Factory (o data factory). Data Factory di Azure è composto da quattro componenti principali che interagiscono tra di loro piattaforma hello tooprovide in cui è possibile comporre i flussi di lavoro con passaggi toomove e trasformare i dati basati sui dati. 

### <a name="pipeline"></a>Pipeline
Una data factory può comprendere una o più pipeline. Una pipeline è un gruppo di attività, Insieme, le attività di hello in una pipeline di eseguono un'attività. Ad esempio, una pipeline potrebbe contenere un gruppo di attività che inserisce i dati da un blob di Azure e quindi eseguire una query Hive su una data di hello toopartition cluster HDInsight. Hello questo modo che pipeline hello consente attività hello toomanage come set anziché ognuna singolarmente. Ad esempio, è possibile distribuire e pianificare le pipeline di hello, anziché le attività di hello in modo indipendente. 

### <a name="activity"></a>Attività
Una pipeline può comprendere una o più attività. Attività definiscono hello azioni tooperform sui dati. Ad esempio, si potrebbero utilizzare un copia attività toocopy dati da un archivio tooanother dati archivio dati. Analogamente, è possibile utilizzare un'attività Hive, che viene eseguita una query Hive in un tootransform cluster HDInsight di Azure o analizzare i dati. Data Factory supporta due tipi di attività: attività di spostamento dei dati e attività di trasformazione dei dati.

### <a name="data-movement-activities"></a>Attività di spostamento dei dati
Attività di copia in Data Factory copia dati da un archivio dati di origine dati archivio tooa sink. Data Factory supporta hello seguenti archivi dati. È possibile scrivere dati da qualsiasi origine tooany sink. Fare clic su un toolearn archivio dati come toocopy tooand di dati dall'archivio.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Per altre informazioni, vedere l'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Attività di trasformazione dei dati
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Per altre informazioni, vedere l'articolo [Attività di trasformazione dei dati](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Attività .NET personalizzate
Se sono necessari dati toomove a/da un archivio dati di attività di copia non supporta, o trasformare i dati usando la logica personalizzata, creare un **attività .NET personalizzata**. Per i dettagli sulla creazione e l'uso di un'attività personalizzata, vedere l'articolo [Usare attività personalizzate in una pipeline di Azure Data Factory](data-factory-use-custom-activities.md).

### <a name="datasets"></a>Set di dati
Un'attività accetta zero o più set di dati come input e uno o più set di dati come output. Set di dati rappresentano strutture dei dati in archivi dati hello, che è sufficiente scegliere o fare riferimento a dati hello da toouse nelle attività come input o output. Ad esempio, un set di dati Blob di Azure specifica contenitore blob hello e cartelle nell'archiviazione Blob di Azure hello dal quale hello pipeline deve leggere i dati di hello. In alternativa, un set di dati di tabelle di SQL Azure consente di specificare dati di output di hello tabella toowhich hello sono scritto da attività hello. 

### <a name="linked-services"></a>Servizi collegati
Servizi collegati sono molto simili a stringhe di connessione, che definiscono le informazioni di connessione hello necessarie per le risorse di tooexternal tooconnect Data Factory. Pensare in questo modo, un servizio collegato definisce l'origine dati di hello connessione toohello e un set di dati rappresenta struttura hello dei dati di hello. Ad esempio, un servizio collegato di archiviazione di Azure specifica connessione stringa tooconnect toohello account di archiviazione Azure. E un set di dati Blob di Azure specifica contenitore blob hello e la cartella di hello che contiene dati hello.   

In Data factory i servizi collegati vengono usati per i due scopi seguenti:

* toorepresent un **archivio dati** inclusi via esemplificativa, un Server SQL locale, i database Oracle, condivisione file o un account di archiviazione Blob di Azure. Vedere hello [attività lo spostamento dei dati](#data-movement-activities) sezione per un elenco degli archivi di dati supportati.
* toorepresent un **risorse di calcolo** che può ospitare esecuzione hello di un'attività. Ad esempio, hello HDInsightHive attività viene eseguito in un cluster HDInsight Hadoop. Vedere la sezione [Attività di spostamento dei dati](#data-transformation-activities) per un elenco di ambienti di calcolo supportati.

### <a name="relationship-between-data-factory-entities"></a>Relazioni tra le entità di Data Factory
![Diagramma: Data Factory, servizio di integrazione dei dati cloud - Concetti chiave](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Figura 2.** Relazioni tra set di dati, attività, pipeline e servizio collegato

## <a name="supported-regions"></a>Aree supportate
Attualmente, è possibile creare data factory in hello **Stati Uniti occidentali**, **Stati Uniti orientali**, e **Europa settentrionale** aree. Tuttavia, una data factory può accedere ad archivi dati e altri dati toomove aree di Azure tra archivi dati servizi di calcolo o dati di processo tramite servizi di calcolo.

Azure Data Factory stesso non archivia alcun dato. Consente di creare flussi di lavoro basati su dati tooorchestrate spostamento dei dati tra [supportati archivi dati](#data-movement-activities) e l'elaborazione dei dati mediante [servizi di calcolo](#data-transformation-activities) in altre aree o in un locale ambiente. Consente inoltre troppo[monitorare e gestire i flussi di lavoro](data-factory-monitor-manage-pipelines.md) utilizzando sia a livello di codice e i meccanismi di interfaccia utente.

Anche se Data Factory è disponibile solo in **Stati Uniti occidentali**, **Stati Uniti orientali**, e **Europa settentrionale** aree, il servizio di hello accensione lo spostamento dei dati di hello in Data Factory è disponibile [globale](data-factory-data-movement-activities.md#global) in aree diverse. Se un archivio dati si trova dietro un firewall, quindi un [Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) installato invece dei dati di hello passa ambiente locale.

Si supponga ad esempio che gli ambienti di calcolo, come un cluster Azure HDInsight e Azure Machine Learning, siano in esecuzione nell'area Europa occidentale. È possibile creare e utilizzare un'istanza di Azure Data Factory in Europa settentrionale e usarlo processi tooschedule negli ambienti di calcolo in Europa occidentale. Occorrono pochi millisecondi per il processo di Data Factory tootrigger hello nell'ambiente di calcolo, ma ora hello per l'esecuzione processo hello in ambiente di elaborazione non cambia.

## <a name="get-started-with-creating-a-pipeline"></a>Introduzione alla creazione di una pipeline
È possibile utilizzare uno di questi strumenti o una pipeline di dati toocreate API in Azure Data Factory: 

- Portale di Azure
- Visual Studio
- PowerShell
- API .NET
- API REST
- Modello di Azure Resource Manager. 

toolearn come pipeline toobuild data factory con i dati, seguire le istruzioni dettagliate in hello seguenti esercitazioni:

| Esercitazione | Descrizione |
| --- | --- |
| [Spostare dati tra due archivi dati cloud](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |In questa esercitazione, si crea una factory di dati con una pipeline che **sposta dati** dal database tooSQL di archiviazione Blob. |
| [Trasformare i dati usando cluster Hadoop](data-factory-build-your-first-pipeline.md) |Questa esercitazione mostra come compilare la prima istanza di Azure Data Factory con una pipeline di dati che **elabora i dati** eseguendo uno script Hive in un cluster Azure HDInsight (Hadoop). |
| [Spostare dati tra un archivio dati locale e un archivio dati cloud usando il gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) |In questa esercitazione si compila una data factory con una pipeline che **sposta dati** da un **locale** tooan di database di SQL Server blob di Azure. Come parte della procedura dettagliata di hello, installare e configurare hello Gateway di gestione dati nel computer. |
