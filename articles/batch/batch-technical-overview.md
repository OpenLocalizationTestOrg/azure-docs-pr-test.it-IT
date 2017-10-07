---
title: aaaAzure Batch viene eseguito soluzioni di elaborazione parallele su larga scala nel cloud hello | Documenti Microsoft
description: Informazioni sull'utilizzo del servizio Azure Batch hello per carichi di lavoro HPC e paralleli su larga scala
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Eseguire carichi di lavoro intrinsecamente paralleli con Batch

Azure Batch è un servizio di piattaforma per l'esecuzione di applicazioni su larga scala parallele e ad alte prestazioni (HPC computing) in modo efficiente nel cloud hello. Azure Batch pianifica toorun di lavoro a utilizzo intensivo di calcolo su una raccolta di macchine virtuali gestita e possa automaticamente la scala di calcolo esigenze hello toomeet di risorse dei processi.

Con Azure Batch, è possibile facilmente definire tooexecute risorse di calcolo di Azure le applicazioni in parallelo e su larga scala. Non è toomanually è necessario creare, configurare e gestire un cluster HPC, singole macchine virtuali, reti virtuali o un processo complesso e infrastruttura di pianificazione di attività. Azure Batch automatizza o semplifica queste attività.

## <a name="use-cases-for-batch"></a>Casi d'uso di Batch
Batch è un servizio gestito di Azure usato per l'*elaborazione batch* o *batch computing*, ovvero l'esecuzione di un volume elevato di attività simili per un risultato previsto. Il batch computing viene in genere usato dalle aziende che devono elaborare, trasformare e analizzare regolarmente volumi di dati di grandi dimensioni.

Batch funziona bene con applicazioni e carichi di lavoro intrinsecamente paralleli, a volte definiti "imbarazzantemente paralleli", che possono essere suddivisi facilmente in più attività ed eseguiti contemporaneamente in più computer.

![Attività parallele][1]<br/>

Di seguito sono riportati alcuni esempi di carichi di lavoro in genere elaborati con questa tecnica:

* Modellazione dei rischi finanziari
* Analisi dei dati climatici e idrologici
* Rendering, analisi ed elaborazione di immagini
* Codifica e transcodifica multimediale
* Analisi delle sequenze genetiche
* Analisi delle sollecitazioni in fase di progettazione
* Test di software

Batch può inoltre eseguire i calcoli paralleli con un passaggio di ridurre al fine di hello ed eseguire carichi di lavoro HPC più complessi, ad esempio [interfaccia MPI (Message Passing)](batch-mpi.md) applicazioni.

Per un confronto tra Batch e altre soluzioni HPC in Azure, vedere [Soluzioni Batch e HPC nel cloud di Azure](batch-hpc-solutions.md).

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Scenario: scalabilità orizzontale di un carico di lavoro parallelo
Una soluzione comune che usa hello API Batch toointeract con il servizio Batch hello implica la scalabilità orizzontale lavoro intrinsecamente parallelo, ad esempio per il rendering hello di immagini per le scene 3D, in un pool di nodi di calcolo. Questo pool di nodi di calcolo può essere "rendering farm" che fornisce decine, centinaia o migliaia di processo di rendering tooyour core, ad esempio.

Hello diagramma seguente viene illustrato un Batch flusso di lavoro comune, con un'applicazione client o un servizio ospitato utilizzando Batch toorun un carico di lavoro parallelo.

![Flusso di lavoro della soluzione Batch][2]

In questo scenario comune, l'applicazione o servizio elabora un carico di lavoro di elaborazione in Batch di Azure eseguendo hello alla procedura seguente:

1. Caricare hello **file di input** hello e **applicazione** che elaborerà i tooyour file account di archiviazione di Azure. file di input Hello possono essere qualsiasi dato che l'applicazione elaborerà, ad esempio dati di modellazione finanziaria o file video toobe transcodificato. i file dell'applicazione Hello possono essere qualsiasi applicazione che viene utilizzato per l'elaborazione dati hello, ad esempio un transcodificatore media o un'applicazione per il rendering 3D.
2. Creare un Batch **pool** dei nodi di calcolo nell'account di Batch, questi nodi sono macchine virtuali hello che eseguirà le attività. Specificare le proprietà, ad esempio hello [dimensioni nodo](../cloud-services/cloud-services-sizes-specs.md)relativo sistema operativo e la posizione di hello in archiviazione di Azure di hello applicazione tooinstall quando i nodi di hello join pool hello (applicazione hello caricato nel passaggio &#1;). È inoltre possibile configurare il pool di hello troppo[automaticamente scalati](batch-automatic-scaling.md) risposta toohello del carico di lavoro che generano le attività. La scalabilità automatica in modo dinamico modifica il numero di hello dei nodi di calcolo nel pool di hello.
3. Creare un Batch **processo** toorun hello carico di lavoro del pool di hello di nodi di calcolo. Quando si crea un processo, lo si associa a un pool di Batch.
4. Aggiungere **attività** toohello processo. Quando si aggiunge il processo di tooa attività, il servizio Batch hello automaticamente hello le attività vengono programmate per l'esecuzione in nodi di calcolo hello nel pool di hello. Ogni attività utilizza un'applicazione hello caricato i file di input hello tooprocess.
   
   * 4a. Prima di un'attività viene eseguita, è possibile scaricare i dati hello (file di input di hello) che si tratta del nodo di calcolo toohello tooprocess a che viene assegnato. Se un'applicazione hello non è già installata nel nodo hello (vedere il passaggio &#2;), può essere scaricato qui invece. Dopo aver completato i download hello, hello eseguite ai relativi nodi assegnati.
5. Come eseguire attività di hello, è possibile eseguire una query Batch toomonitor hello lo stato di avanzamento del processo di hello e le relative attività. L'applicazione client o il servizio comunica con il servizio Batch hello tramite HTTPS. Dal momento che può essere monitoraggio migliaia di attività in esecuzione in migliaia di nodi di calcolo, troppo[query in modo efficiente servizio Batch hello](batch-efficient-list-queries.md).
6. Come completare attività hello, è possibile caricare tooAzure di dati archiviazione i relativi risultati. È inoltre possibile recuperare i file direttamente dal file system di hello in un nodo di calcolo.
7. Quando il monitoraggio rileva di aver completato le attività nel processo di hello, l'applicazione client o il servizio è possibile scaricare dati di output di hello per un'ulteriore elaborazione o evaluation.

Tenere presente questo è solo una delle modalità toouse Batch e questo scenario descrive solo alcune delle funzionalità disponibili. Ad esempio, è possibile eseguire [più attività in parallelo](batch-parallel-node-tasks.md) in ogni nodo di calcolo e utilizzare [attività di preparazione e completamento del processo](batch-job-prep-release.md) tooprepare hello nodi per i processi, quindi pulire successivamente.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato una panoramica generale di hello servizio Batch, è ora toodig più approfondita toolearn come è possibile usarlo tooprocess i carichi di lavoro con utilizzo intensivo di calcolo paralleli.

* Hello lettura [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md), informazioni essenziale per chiunque preparazione toouse Batch. articolo Hello contiene informazioni più dettagliate sulle risorse del servizio Batch come pool di nodi, processi e attività e hello molte funzionalità dell'API che è possibile utilizzare durante la compilazione dell'applicazione di Batch.
* Informazioni su hello [Batch API e strumenti](batch-apis-tools.md) disponibili per la creazione di soluzioni di Batch.
* [Introduzione alla libreria di Azure Batch hello per .NET](batch-dotnet-get-started.md) toolearn come toouse c# e hello tooexecute libreria .NET di Batch di un carico di lavoro semplice utilizzando un flusso di lavoro comune di Batch. In questo articolo deve essere il primo viene arrestata quando si impara come toouse hello servizio Batch. È inoltre disponibile un [versione di Python](batch-python-tutorial.md) di esercitazione hello.
* Scaricare hello [esempi su GitHub di codice] [ github_samples] toosee come c# e Python può interfacciarsi con Batch tooschedule e processo di esempio carichi di lavoro.
* Estrarre hello [il percorso di apprendimento Batch] [ learning_path] tooget un'idea di tooyou disponibili risorse di hello come è illustrato toowork con Batch.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
