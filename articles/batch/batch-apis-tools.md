---
title: soluzioni aaaUse strumenti e le API di Azure Batch toodevelop su larga scala l'elaborazione parallela | Documenti Microsoft
description: Informazioni sulle API hello e gli strumenti disponibili per lo sviluppo di soluzioni con il servizio di Azure Batch hello.
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Panoramica delle API e degli strumenti di Batch

L'elaborazione dei carichi di lavoro paralleli con Azure Batch è in genere eseguita a livello di programmazione utilizzando uno dei hello [API Batch](#batch-development-apis). L'applicazione client o il servizio è possibile utilizzare hello API Batch toocommunicate con hello servizio Batch. Con hello API Batch, è possibile creare e gestire i pool di nodi di calcolo, le macchine virtuali o i servizi cloud. È quindi possibile pianificare processi e attività toorun tali nodi. 

È possibile in modo efficiente di elaborare carichi di lavoro su larga scala per l'organizzazione, o fornire un front-end del servizio clienti tooyour in modo che possano eseguire processi e attività, su richiesta o in una pianificazione, in uno, centinaia o migliaia di nodi. È anche possibile usare il servizio Azure Batch nell'ambito di un flusso di lavoro più ampio, gestito da strumenti come [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Quando si è pronti toodig in toohello API Batch per una conoscenza più approfondita di hello caratteristiche disponibili, estrarre hello [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Account Azure per lo sviluppo Batch
Quando si sviluppano soluzioni di Batch, si userà hello seguendo gli account in Microsoft Azure.

* **Account e sottoscrizione di Azure**: se non si ha già una sottoscrizione di Azure, è possibile attivare i [vantaggi dell'abbonamento a MSDN][msdn_benefits] oppure iscriversi per ottenere un [account Azure gratuito][free_account]. Quando si crea un account, viene creata una sottoscrizione predefinita.
* **Account Batch**: le risorse di Azure Batch, inclusi pool, nodi di calcolo, processi e attività, sono associate a un account Azure Batch. Quando l'applicazione esegue una richiesta nel servizio Batch hello, consente l'autenticazione richiesta hello utilizzando nome dell'account Azure Batch hello, hello URL dell'account hello e una chiave di accesso. È possibile [creare l'account Batch](batch-account-create-portal.md) in hello portale di Azure.
* **Account di archiviazione**: Batch include il supporto predefinito per l'uso di file in [Archiviazione di Azure][azure_storage]. Quasi ogni scenario di Batch utilizza l'archiviazione Blob di Azure per dati di hello che elaborano e programmi hello che eseguono le attività di gestione temporanea e per l'archiviazione dei dati di output che generano hello. toocreate un account di archiviazione, vedere [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>API di servizio Batch

Le applicazioni e servizi possono rilasciare dirette chiamate all'API REST o utilizzare uno o più dei seguenti toorun librerie client hello e gestire i carichi di lavoro di Azure Batch.

| API | Informazioni di riferimento sulle API | Scaricare | Esercitazione | Esempi di codice | Altre informazioni |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |N/D |- |- | [Versioni supportate](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Esercitazione](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Note sulla versione](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Esercitazione](batch-python-tutorial.md)|[GitHub][api_sample_python] | [File Leggimi](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [File Leggimi](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[File Leggimi][api_sample_java] | [File Leggimi](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>API per la gestione di Batch

API di gestione risorse di Azure per Batch Hello forniscono l'accesso a livello di codice tooBatch account. Usando queste API, è possibile gestire a livello di codice gli account Batch, le quote e i pacchetti dell'applicazione.  

| API | Informazioni di riferimento sulle API | Scaricare | Esercitazione | Esempi di codice |
| --- | --- | --- | --- | --- |
| **REST di Resource Manager per Batch** |[docs.microsoft.com][api_rest_mgmt] |N/D |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **.NET di Resource Manager per Batch** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Esercitazione](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Strumenti da riga di comando di Batch

Questi strumenti da riga di comando offrono hello stessa funzionalità come hello API di gestione di Batch e il servizio Batch: 

* [I cmdlet di PowerShell batch][batch_ps]: hello cmdlet di Azure Batch in hello [Azure PowerShell](/powershell/azure/overview) modulo consentono risorse Batch toomanage con PowerShell.
* [CLI di Azure](/cli/azure/overview): hello interfaccia della riga di comando di Azure (Azure CLI) è un set di strumenti multipiattaforma che fornisce i comandi della shell per interagire con molti servizi di Azure, inclusi il servizio di Batch hello e servizio di gestione dei Batch. Vedere [risorse gestire Batch con Azure CLI](batch-cli-get-started.md) per ulteriori informazioni sull'utilizzo di hello CLI di Azure batch.

## <a name="other-tools-for-application-development"></a>Altri strumenti per lo sviluppo di applicazioni

Di seguito sono riportati alcuni strumenti aggiuntivi che possono risultare utili per la compilazione e il debug di applicazioni e servizi Batch:

* [Portale di Azure][portal]: si può creare, monitorare ed eliminare pool, processi e attività in hello Azure Batch pannelli Batch del portale. È possibile visualizzare le informazioni sullo stato di hello per queste e altre risorse mentre si eseguono i processi e anche scaricare i file dei nodi di calcolo hello nei pool. È ad esempio possibile scaricare il file `stderr.txt` di un'attività non riuscita durante la risoluzione dei problemi. È inoltre possibile scaricare i file Desktop remoto (RDP) che è possibile utilizzare toolog toocompute nodi.
* [Azure Batch Esplora][batch_explorer]: Esplora Batch offre funzionalità di gestione risorse di Batch simili come hello portale di Azure, ma in un'applicazione client Windows Presentation Foundation (WPF) autonoma. Una delle applicazioni di esempio .NET per Batch hello disponibile in [GitHub][github_samples], è possibile compilare con Visual Studio 2015 o versione successiva e usarlo toobrowse e gestire risorse hello nell'account di Batch durante lo sviluppo e debug delle soluzioni di Batch. Visualizza processo, i pool e i dettagli delle attività, scaricano file da nodi di calcolo e connettono in remoto toonodes utilizzando Esplora Batch è possibile scaricare i file di Desktop remoto (RDP).
* [Microsoft Azure Storage Explorer][storage_explorer]: sebbene non sia strettamente uno strumento di Azure Batch, hello Esplora archivi è un altro strumento prezioso toohave durante lo sviluppo e debug delle soluzioni di Batch.

## <a name="additional-resources"></a>Risorse aggiuntive

- toolearn sugli eventi di registrazione dall'applicazione di Batch, vedere [registrare gli eventi per una valutazione diagnostica e monitoraggio di soluzioni di Batch](batch-diagnostics.md). Per informazioni di riferimento sugli eventi generati dal servizio Batch hello, vedere [Analitica Batch](batch-analytics.md).
- Per informazioni sulle variabili di ambiente per i nodi di calcolo, vedere [Variabili di ambiente per i nodi di calcolo di Azure Batch](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Passaggi successivi

* Hello lettura [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md), informazioni essenziale per chiunque preparazione toouse Batch. articolo Hello contiene informazioni più dettagliate sulle risorse del servizio Batch come pool di nodi, processi e attività e hello molte funzionalità dell'API che è possibile utilizzare durante la compilazione dell'applicazione di Batch.
* [Introduzione alla libreria di Azure Batch hello per .NET](batch-dotnet-get-started.md) toolearn come toouse c# e hello tooexecute libreria .NET di Batch di un carico di lavoro semplice utilizzando un flusso di lavoro comune di Batch. In questo articolo deve essere il primo viene arrestata quando si impara come toouse hello servizio Batch. È inoltre disponibile un [versione di Python](batch-python-tutorial.md) di esercitazione hello.
* Scaricare hello [esempi su GitHub di codice] [ github_samples] toosee come c# e Python può interfacciarsi con Batch tooschedule e processo di esempio carichi di lavoro.
* Estrarre hello [il percorso di apprendimento Batch] [ learning_path] tooget un'idea di tooyou disponibili risorse di hello come è illustrato toowork con Batch.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
