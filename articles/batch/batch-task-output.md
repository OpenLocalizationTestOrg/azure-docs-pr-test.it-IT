---
title: "dati tooa processi e attività di completamento aaaPersist risultati o log da archivio - Azure Batch | Documenti Microsoft"
description: "Informazioni su diverse opzioni per rendere persistenti i dati di output da attività e processi di Batch. È possibile mantenere i dati di archiviazione tooAzure o tooanother archiviare."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Rendere persistente l'output di processi e attività

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Alcuni esempi comuni di output delle attività includono:

- File creati durante i processi di hello attività dati di input.
- File di log associati all'esecuzione dell'attività. 

In questo articolo vengono descritte varie opzioni per salvare in modo permanente attività output hello scenari e per il quale ogni opzione è più appropriato.   

## <a name="about-hello-batch-file-conventions-standard"></a>Informazioni sullo standard di hello convenzioni dei File Batch

Batch definisce un set facoltativo di convenzioni per la denominazione dei file di output delle attività in Archiviazione di Azure. Hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) descrive queste convenzioni. standard di convenzioni per i File Hello determina i nomi di hello hello destinazione blob e contenitore del percorso di archiviazione di Azure per un file di output specificata in base ai nomi di hello del processo di hello e attività.

È attivo tooyou se si decide di hello toouse convenzioni dei File standard per la denominazione dei file di dati di output. È anche possibile denominare i blob e contenitore di destinazione hello tuttavia desiderato. Se si utilizza hello convenzioni dei File standard per la denominazione dei file di output, quindi i file di output sono disponibili per la visualizzazione in hello [portale di Azure][portal].

Esistono alcuni modi diversi, che è possibile utilizzare standard di convenzioni per i File hello:

- Se si utilizza il file di output toopersist hello Batch servizio API, è possibile scegliere i contenitori di destinazione tooname e BLOB in base toohello convenzioni dei File standard. API del servizio Batch Hello consente toopersist i file di output dal codice client, senza modificare l'applicazione di attività.
- Se si sviluppa con .NET, è possibile utilizzare hello [libreria convenzioni File Batch di Azure per .NET][nuget_package]. Un vantaggio dell'utilizzo di questa libreria è che supporta l'esecuzione di query in base a ID tootheir o lo scopo dei file di output. funzionalità di query incorporate Hello rende facile tooaccess i file di output da un'applicazione client o da altre attività. Tuttavia, l'applicazione di attività deve essere modificato toocall libreria di convenzioni per i File. Per ulteriori informazioni, vedere il riferimento hello per hello [libreria convenzioni dei File per .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Se si sviluppa con un linguaggio diverso da .NET, è possibile implementare hello convenzioni dei File standard dell'applicazione.

## <a name="design-considerations-for-persisting-output"></a>Considerazioni sulla progettazione per la persistenza dell'output 

Quando si progetta la soluzione di Batch, prendere in considerazione seguente hello fattori correlati toojob e risultati delle attività.

* **Durata dei nodi di calcolo**: questi nodi sono spesso temporanei, in particolare nei pool abilitati per il ridimensionamento automatico. Output di un'attività che viene eseguito in un nodo è disponibile solo hello nodo esiste, ma solo entro il periodo di memorizzazione file hello sono stati impostati per l'attività hello. Se un'attività genera output che potrebbero essere necessari al termine dell'attività hello, attività hello necessario caricare il relativo archivio durevole tooa al file di output, ad esempio l'archiviazione di Azure.

* **Archiviazione dell'output**: Archiviazione di Azure è la soluzione consigliata come archivio dati per l'output delle attività, ma è possibile usare qualsiasi sistema di archiviazione permanente. Scrittura di attività output tooAzure archiviazione è integrata in hello API del servizio Batch. Se si utilizza un altro formato di archiviazione durevole, è necessario output dell'attività toopersist logica dell'applicazione hello toowrite manualmente.   

* **Il recupero di output**: È possibile recuperare l'output dell'attività direttamente dai nodi di calcolo hello del pool o da un altro archivio dati o di archiviazione di Azure se si è rese persistenti di output dell'attività. tooretrieve un'attività di output direttamente da un nodo di calcolo, è necessario il nome di file hello e il relativo percorso di output sul nodo hello. Se si utilizzano attività output tooAzure archiviazione, è necessario file toohello percorso completo di hello nei file di output di archiviazione di Azure toodownload hello con hello Azure Storage SDK.

* **Visualizzazione dell'output**: quando ci si sposta attività Batch tooa hello Azure portale e selezionare **file nodo**, viene visualizzata con tutti i file associati attività hello, hello non solo i file di output si è interessati. Nuovo file sui nodi di calcolo sono disponibili solo mentre hello nodo esiste solo nel periodo di conservazione file hello sono stati impostati per l'attività hello. output dell'attività di tooview che è stata resa persistente tooAzure archiviazione, è possibile utilizzare hello portale di Azure o un'applicazione client di archiviazione di Azure, ad esempio hello [Azure Storage Explorer][storage_explorer]. tooview output dei dati in archiviazione di Azure con il portale di hello o un altro strumento, è necessario conoscere il percorso del file hello e passare direttamente tooit.

## <a name="options-for-persisting-output"></a>Opzioni per la persistenza dell'output

A seconda dello scenario, sono disponibili due diversi approcci è possibile eseguire l'output dell'attività toopersist:

- Usare l'API del servizio Batch hello.  
- Usare libreria di hello convenzioni dei File Batch per .NET.  
- Implementare hello convenzioni dei File Batch standard dell'applicazione.
- Implementare una soluzione personalizzata per lo spostamento dei file.

Hello le sezioni seguenti vengono descritti più dettagliatamente ogni approccio.

### <a name="use-hello-batch-service-api"></a>Utilizzare l'API del servizio Batch hello

Aggiunge il supporto per specificare i file di output in archiviazione di Azure per i dati di attività con la versione 2017-05-01, hello servizio Batch quando si [aggiungere un processo tooa attività](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) o [aggiungere una raccolta di processi tooa attività](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Hello API del servizio Batch supporta persistenti attività dati tooan account di archiviazione di Azure dal pool creati con la configurazione della macchina virtuale hello. Con l'API del servizio Batch hello, è possibile mantenere i dati di attività senza modificare l'applicazione hello che esegue l'attività. È facoltativamente possibile rispettare toohello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) mantenere tooAzure archiviazione per la denominazione di file hello. 

Utilizzare quando l'output di hello API del servizio Batch toopersist attività:

- Si desidera toopersist dati dalle attività di Batch e attività di processo di gestione nel pool creati con la configurazione della macchina virtuale hello.
- Si desidera toopersist contenitore di archiviazione di Azure tooan di dati con un nome arbitrario.
- Si desidera toopersist contenitore di archiviazione di Azure tooan dati denominato in base toohello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Hello API del servizio Batch non consente di rendere persistenti i dati dall'attività in esecuzione nel pool creati con la configurazione del servizio cloud hello. Per informazioni sull'attività persistenti dal pool di eseguire la configurazione di servizi cloud hello di output, vedere [mantenere job e task tooAzure archiviazione dati con libreria di hello convenzioni dei File Batch per .NET toopersist](batch-task-output-file-conventions.md)
> 
> 

Per ulteriori informazioni sull'output dell'attività persistenti con hello API del servizio Batch, vedere [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md). Vedere anche hello [PersistOutputs] [github_persistoutputs] il progetto in GitHub, che illustra la modalità di output toodurable archiviazione libreria client di toouse hello Batch per attività toopersist .NET di esempio.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Utilizzare libreria di hello convenzioni dei File Batch per .NET

Gli sviluppatori la creazione di soluzioni di Batch con c# e .NET possono utilizzare hello [libreria convenzioni dei File per .NET] [ nuget_package] toopersist attività dati tooan account di archiviazione di Azure, in base toohello [File Batch Le convenzioni standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). libreria di convenzioni per i File Hello gestisce tooAzure i file di output mobile archiviazione e denominazione dei BLOB e contenitori di destinazione in modo ben noto.

essi senza la necessità di hello Hello convenzioni File libreria supporta i file di output per l'ID o a scopo di una query, rendendo semplice toolocate completare file URI. 

Utilizzo della libreria di convenzioni per i File Batch hello per attività toopersist .NET quando l'output:

- Si desidera toostream dati tooAzure archiviazione mentre l'attività hello è ancora in esecuzione.
- Si desidera toopersist dati dal pool creati con la configurazione di macchina virtuale hello o della configurazione del servizio cloud hello.
- L'applicazione client o altre attività in hello processi toolocate esigenze e scaricare i file di output di attività per ID o in base allo scopo. 
- Si desidera tooperform controllo verso il basso o anticipata il caricamento dei risultati iniziali.
- Desideri che l'output dell'attività tooview in hello portale di Azure.

Per ulteriori informazioni sul salvataggio in modo permanente l'output dell'attività con libreria convenzioni File hello per .NET, vedere [mantenere job e task tooAzure archiviazione dati con libreria di hello convenzioni dei File Batch per .NET toopersist ](batch-task-output-file-conventions.md). Vedere anche hello [PersistOutputs] [github_persistoutputs] il progetto in GitHub, che illustra come libreria di convenzioni per i File hello toouse per attività toopersist .NET output archiviazione toodurable di esempio.

Hello progetto di esempio [PersistOutputs] [github_persistoutputs] su GitHub riportato viene illustrato come libreria client di toouse hello Batch per attività toopersist .NET toodurable archiviazione.

### <a name="implement-hello-batch-file-conventions-standard"></a>Implementare hello convenzioni dei File Batch standard

Se si utilizza un linguaggio diverso da .NET, è possibile implementare hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) nella propria applicazione. 

È consigliabile tooimplement hello standard di denominazione File convenzioni manualmente quando si desidera che uno schema di denominazione si basa sulla collaudata o quando si desidera che l'output dell'attività tooview in hello portale di Azure.

### <a name="implement-a-custom-file-movement-solution"></a>Implementare una soluzione personalizzata per lo spostamento dei file

È anche possibile implementare una soluzione completa propria per lo spostamento dei file. Usare questo approccio nei casi seguenti:

- Si desidera toopersist attività dati tooa archivio di dati diverso da archiviazione di Azure. dati tooa tooupload file archivio come SQL Azure o Azure Lake, è possibile creare uno script personalizzato o un percorso toothat tooupload eseguibile. È quindi possibile chiamarlo nella riga di comando hello dopo l'esecuzione del file eseguibile principale. In un nodo di Windows, ad esempio, si potrebbero chiamare questi due comandi:`doMyWork.exe && uploadMyFilesToSql.exe`
- Si desidera tooperform controllo verso il basso o anticipata il caricamento dei risultati iniziali.
- Si desidera un controllo granulare toomaintain sulla gestione degli errori. Ad esempio, è consigliabile tooimplement soluzione se si desidera toouse attività dipendenza azioni tootake determinati caricare azioni in base ai codici di uscita di attività specifica. Per ulteriori informazioni sulle azioni di dipendenze di attività, vedere [creare relazioni tra attività attività toorun che dipendono da altre attività](batch-task-dependencies.md). 

## <a name="next-steps"></a>Passaggi successivi

- Esplorare l'utilizzo delle nuove funzionalità di hello nei dati di attività hello API del servizio Batch toopersist in [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md).
- Informazioni sull'uso della libreria di hello convenzioni dei File Batch per .NET in [mantenere job e task tooAzure archiviazione dati con libreria di hello convenzioni dei File Batch per .NET toopersist ](batch-task-output-file-conventions.md).
- Vedere hello [PersistOutputs] [github_persistoutputs] toodurable archiviazione output del progetto di esempio in GitHub, che illustra come toouse entrambi hello libreria client di Batch per .NET e libreria convenzioni File hello per attività toopersist .NET.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
