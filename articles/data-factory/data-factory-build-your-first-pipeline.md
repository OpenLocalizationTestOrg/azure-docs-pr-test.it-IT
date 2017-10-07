---
title: 'Esercitazione su Data Factory: prima pipeline di dati | Documentazione Microsoft'
description: In questa esercitazione di Data Factory di Azure viene illustrato come toocreate e la pianificazione di una data factory che elabora i dati utilizzando Hive eseguito uno script in un cluster Hadoop.
services: data-factory
keywords: esercitazione di azure data factory, cluster hadoop, hive di hadoop
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Esercitazione: Creare i primi dati tootransform pipeline utilizzando cluster Hadoop
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

In questa esercitazione si compila la prima data factory di Azure con una pipeline di dati. Hello pipeline Trasforma i dati di input tramite l'esecuzione di script Hive in un cluster di Azure HDInsight (Hadoop) tooproduce output dati.  

Questo articolo fornisce una panoramica e prerequisiti per l'esercitazione hello. Dopo aver completato i prerequisiti di hello, è possibile eseguire esercitazione hello utilizzando uno dei seguenti SDK di strumenti/hello: portale di Azure, Visual Studio, PowerShell, Gestione risorse modello API REST. Selezionare una delle opzioni di hello nell'elenco a discesa hello hello inizio (o) i collegamenti alla fine di hello di questa esercitazione di hello toodo articolo utilizzando una di queste opzioni.    

## <a name="tutorial-overview"></a>Panoramica dell'esercitazione
In questa esercitazione è eseguire hello alla procedura seguente:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline di dati che spostano e trasformano i dati. 

    In questa esercitazione è creare una pipeline in data factory di hello. 
2. Creare una **pipeline**. Una pipeline può comprendere una o più attività (esempi: attività di copia, attività Hive HDInsight). Questo esempio utilizza hello attività Hive di HDInsight che esegue uno script Hive in un cluster HDInsight Hadoop. script di Hello crea innanzitutto una tabella in cui i riferimenti hello dati di log web non elaborato archiviati nell'archiviazione blob di Azure e quindi partizioni hello dati non elaborati per anno e mese.

    In questa esercitazione, pipeline di hello utilizza dati tootransform attività Hive di hello eseguendo una query Hive in un cluster Azure HDInsight Hadoop. 
3. Creare **servizi collegati**. Per creare un servizio collegato di toolink un archivio dati o una data factory toohello servizio di calcolo. Un archivio dati, ad esempio l'archiviazione di Azure contiene i dati di input/output delle attività nella pipeline hello. Un servizio di calcolo come un cluster Hadoop di HDInsight elabora/trasforma i dati.

    In questa esercitazione guidata si creano due servizi collegati : **Archiviazione di Azure** e **Azure HDInsight**. Archiviazione di Azure Hello collegato collegamenti al servizio un Account di archiviazione di Azure che contiene una data factory toohello dati di input/output di hello. Azure HDInsight collegato collegamenti al servizio di un cluster HDInsight di Azure che è usato tootransform dati toohello data factory. 
3. Creare **set di dati**di input e di output. Un set di dati di input rappresenta hello l'input per un'attività nella pipeline hello e un set di dati di output rappresenta l'output di hello per attività hello.

    In questa esercitazione, hello di input e output del set di dati specificare i percorsi di input e output di dati in hello archiviazione Blob di Azure. servizio collegato di archiviazione Azure Hello specifica quale Account di archiviazione Azure usato. Consente di specificare un set di dati di input in cui si trovano i file di input hello e specifica di un set di dati di output in cui vengono collocati i file di output di hello. 


Vedere [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo per una panoramica dettagliata della Data Factory di Azure.
  
Ecco hello **vista diagramma** della factory di dati di esempio hello è compilare in questa esercitazione. **MyFirstPipeline** ha un'attività di tipo Hive che usa i set di dati **AzureBlobInput** come input e produce set di dati **AzureBlobOutput** come output. 

![Vista diagramma nell'esercitazione su Data Factory](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


In questa esercitazione, **inputdata** cartella di hello **adfgetstarted** contenitore blob di Azure contiene un file denominato input.log. Questo file di log contiene voci relative ai tre mesi di gennaio, febbraio e marzo 2016. Di seguito sono le righe di esempio hello per ogni mese nel file di input hello. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Quando il file hello venga elaborato dalla pipeline di hello con attività Hive di HDInsight, attività hello esegue uno script Hive nel cluster HDInsight hello che partizioni di dati di input per anno e mese. script di Hello crea tre cartelle di output che contengono un file con le voci di ogni mese.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Dalle righe di esempio hello illustrate in precedenza, hello innanzitutto una (con 2016-01-01) viene scritto toohello 000000_0 file mese hello = 1 cartella. Allo stesso modo, hello secondo viene scritto il file toohello nel mese di hello = 2 cartella e hello terzo uno viene scritto il file toohello nel mese di hello = 3 cartella.  

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti prerequisiti:

1. **Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un account di valutazione gratuito in pochi minuti. Vedere hello [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) articolo su come ottenere un account di prova.
2. **Archiviazione di Azure** : si utilizza un account di archiviazione di Azure standard generica per l'archiviazione dei dati hello in questa esercitazione. Se non si dispone di un account di archiviazione di Azure standard generici, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo. Dopo aver creato l'account di archiviazione hello, prendere nota delle hello **nome account** e **tasto**. Vedere [Visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Scaricare ed esaminare i file di query Hive hello (**HQL**) disponibile all'indirizzo: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Questa query Trasforma i dati di output tooproduce di dati di input. 
4. Scaricare ed esaminare i file di input di esempio hello (**input.log**) disponibile all'indirizzo: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Creare un contenitore BLOB denominato **adfgetstarted** nell'Archiviazione BLOB di Azure. 
6. Caricare **partitionweblogs.hql** file toohello **script** cartella hello **adfgetstarted** contenitore. Usare strumenti come [Esplora archivi di Microsoft Azure](http://storageexplorer.com/). 
7. Caricare **input.log** file toohello **inputdata** cartella hello **adfgetstarted** contenitore. 

Dopo aver completato i prerequisiti di hello, selezionare uno dei hello segue/SDK di strumenti toodo hello esercitazione: 

- [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Il portale di Azure e Visual Studio forniscono l'interfaccia utente grafica per la creazione di data factory. Le opzioni PowerShell, il modello di Resource Manager e l'API REST forniscono una modalità di programmazione/script per la creazione di data factory.

> [!NOTE]
> pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input. Non copia dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md). 





  
