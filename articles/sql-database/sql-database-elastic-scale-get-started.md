---
title: aaaGet visivo con strumenti di database elastico | Documenti Microsoft
description: "Descrizione di base della funzionalità di Database SQL di Azure, tra cui un'app di esempio semplice per eseguire strumenti di database elastico hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Iniziare a utilizzare gli strumenti di database elastici
Questo documento introduce esperienza dello sviluppatore toohello grazie alla possibilità di app di esempio hello toorun. esempio Hello crea una semplice applicazione partizionata ed Esplora le funzionalità principali di strumenti di database elastico. esempio Hello illustra le funzioni di hello [libreria client di database elastico](sql-database-elastic-database-client-library.md).

libreria di hello tooinstall, andare troppo[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). libreria di Hello viene installata con app di esempio hello descritto nella seguente sezione hello.

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2012 o versione successiva con C#. Scaricare una versione gratuita dalla pagina [Download di Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 o versione successiva. versione più recente di hello tooget, vedere [installazione di NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Scaricare ed eseguire app di esempio hello
Hello **elastico strumenti DB per SQL Azure - Introduzione** applicazione di esempio vengono descritti gli aspetti più importanti di hello dell'esperienza di sviluppo hello per le applicazioni partizionate che utilizzano gli strumenti di database elastico. L'applicazione è incentrata sui principali casi d'uso per la [gestione delle mappe delle partizioni](sql-database-elastic-scale-shard-map-management.md), il [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) e l'[esecuzione di query su più partizioni](sql-database-elastic-scale-multishard-querying.md). toodownload e: esempio hello esecuzione, seguire questi passaggi: 

1. Scaricare hello [elastico strumenti DB per SQL Azure - esempio della Guida introduttiva](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) da MSDN. Decomprimere percorso tooa di esempio hello prescelto.

2. toocreate un progetto, aprire hello **ElasticScaleStarterKit.sln** soluzione da hello **c#** directory.

3. Nella soluzione hello per il progetto di esempio hello aprire hello **app** file. Il nome del server di Database SQL di Azure e le informazioni di accesso (nome utente e password), quindi seguire le istruzioni di hello di tooadd file hello.

4. Compilare ed eseguire un'applicazione hello. Quando richiesto, attivare i pacchetti NuGet di Visual Studio toorestore hello della soluzione hello. Versione più recente di hello della libreria client di database elastico hello vengono scaricati da NuGet.

5. Sperimentare hello diverse opzioni toolearn più sulle funzionalità di libreria del client hello. Si noti passaggi hello hello accetta applicazione nell'output di console hello e si ritiene che il codice hello tooexplore libero background hello.
   
    ![Avanzamento][4]

È stata creata ed eseguita la prima applicazione partizionata usando gli strumenti di database elastici nel database SQL. Usare il database SQL tooyour tooconnect Visual Studio o SQL Server Management Studio e un rapido controllo di partizioni hello che hello esempio creato. Si noterà nuovi database di partizione di esempio e un database di gestione di partizioni della mappa: esempio hello che ha creato.

> [!IMPORTANT]
> È consigliabile utilizzare sempre hello la versione più recente di Management Studio in modo da restare sincronizzato con gli aggiornamenti tooAzure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Parti principali dell'esempio di codice hello
* **Esegue il mapping di gestione di partizioni e partizioni**: hello di codice viene illustrato come toowork con partizioni, intervalli e i mapping nel file hello **ShardManagementUtils.cs**. Per ulteriori informazioni, vedere [scalabilità orizzontale di database con gestore mappe partizioni di hello](http://go.microsoft.com/?linkid=9862595).  

* **Routing dipendente dai dati**: Routing di partizioni di transazioni toohello destra viene visualizzato **DataDependentRoutingSample.cs**. Per altre informazioni, vedere [Routing dipendente dai dati](http://go.microsoft.com/?linkid=9862596). 

* **Esecuzione di query su più partizioni**: l'esecuzione di query tra partizioni è illustrato nel file hello **MultiShardQuerySample.cs**. Per altre informazioni, vedere [Esecuzione di query su più partizioni](http://go.microsoft.com/?linkid=9862597).

* **Aggiunta di partizioni vuote**: hello iterativo aggiunta di nuove partizioni vuote viene eseguita dal codice hello nel file hello **CreateShardSample.cs**. Per ulteriori informazioni, vedere [scalabilità orizzontale di database con gestore mappe partizioni di hello](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Altre operazioni di scalabilità elastica
* **Suddividere una partizione esistente**: le partizioni toosplit funzionalità hello viene fornito da hello **strumento di merge di divisione**. Per altre informazioni, vedere [Spostamento di dati tra database cloud con scalabilità orizzontale](sql-database-elastic-scale-overview-split-and-merge.md).

* **L'unione delle partizioni esistenti**: unione di partizioni vengono eseguite anche utilizzando hello **strumento di merge di divisione**. Per altre informazioni, vedere [Spostamento di dati tra database cloud con scalabilità orizzontale](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Costi
strumenti di database elastico Hello sono gratuiti. Quando si usano strumenti di database elastici, non si ricevono eventuali addebiti aggiuntivi nella parte superiore di costo hello relativa all'utilizzo di Azure. 

Ad esempio, l'applicazione di esempio hello crea nuovi database. costo Hello per questo dipende dall'edizione del Database SQL hello che prescelto e hello Azure-utilizzo dell'applicazione.

Per informazioni sui prezzi, vedere [Prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sugli strumenti di database elastici, vedere hello seguenti pagine:

* Esempi di codice: 
  * [Elastic DB Tools for Azure SQL - Getting Started](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE) (Strumenti di database elastici per SQL di Azure - Introduzione)
  * [Elastic DB Tools for Azure SQL - Entity Framework Integration](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE) (Strumenti di database elastici per SQL di Azure - Integrazione con Entity Framework)
  * [Elasticità di partizionamento in Script Center](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog: [Elastic Scale announcement](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/) (Annuncio della scalabilità elastica)
* Microsoft Virtual Academy: [implementazione scalabilità orizzontale con partizionamento orizzontale con hello elastico Video libreria Client di Database](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Channel 9: [video di panoramica della scalabilità elastica](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Forum di discussione: [forum sul database SQL di Azure](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* prestazioni toomeasure: [contatori delle prestazioni per gestore mappe partizioni](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

