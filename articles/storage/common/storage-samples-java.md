---
title: esempi di archiviazione aaaAzure Usa Java | Documenti Microsoft
description: Visualizzare, scaricare ed eseguire codici di esempio e applicazioni per l'Archiviazione di Azure. Individuare introduzione esempi per BLOB, code, tabelle e file, utilizzando le librerie client di archiviazione di hello Java.
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a>Esempi di Archiviazione di Azure che usano Java

## <a name="java-sample-index"></a>Indice degli esempi Java

Hello nella tabella seguente viene fornita una panoramica di esempi del repository e hello scenari analizzate in ogni esempio. Fare clic su hello collegamenti tooview hello corrispondente codice di esempio in GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Endpoint</th><th style="font-size:110%">Scenario</th><th style="font-size:110%">Codice di esempio</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>BLOB</b></td>
<td>Append Blob</td> 
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td> 
</tr> 
<tr> 
<td>BLOB in blocchi</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Crittografia lato client</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a> (Introduzione alla crittografia lato client di Azure in Java)</td>
</tr> 
<tr> 
<td>Copia di BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Creazione contenitore</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Eliminazione BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Eliminazione contenitore</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Metadati/proprietà/statistiche BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>ACL/metadati/proprietà contenitore</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Ottenere intervalli di pagine</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Esempio di test di BLOB di pagine</a></td>
</tr> 
<tr> 
<td>BLOB/contenitore di lease</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>Elenco BLOB/contenitore</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td>BLOB di pagine</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Esempio di test di firma di accesso condiviso (SAS)</a></td>
</tr>   
<tr> 
<td>Proprietà del servizio</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr>           
<tr> 
<td>Snapshot di BLOB</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introduzione al servizio BLOB di Azure in Java)</td>
</tr> 
<tr> 
<td rowspan="9"><b>File</b></td>
<td>Creazione condivisioni/directory/file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr>
<tr> 
<td>Eliminazione condivisioni/directory/file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr> 
<tr> 
<td>Proprietà/metadati di directory</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr> 
<tr> 
<td>Download di file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr> 
<tr> 
<td>Proprietà/metadati/metriche di file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr> 
<tr> 
<td>Proprietà del servizio file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr> 
<tr> 
<td>Elenco di directory e file</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr>
<tr> 
<td>Elenco di condivisioni</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr>
<tr> 
<td>Condivisione di proprietà/metadati/statistiche</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introduzione al servizio File di Azure in Java)</td> 
</tr>
<tr> 
<td rowspan="8"><b>Coda</b></td>
<td>Aggiunta di un messaggio</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Esempi di libreria client di archiviazione Java</a></td> 
</tr> 
<tr> 
<td>Crittografia lato client</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Esempi di libreria client di archiviazione Java</a></td> 
</tr> 
<tr> 
<td>Creazione di code</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td>Eliminazione di messaggio/coda</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td>Visualizzazione di messaggio</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td>ACL/metadati/statistiche di coda</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td>Proprietà del servizio di accodamento</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td>Aggiornamento messaggio</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Introduzione al servizio di accodamento di Azure in Java)</td> 
</tr> 
<tr> 
<td rowspan="7"><b>Tabella</b></td>
<td>Creazione di tabella</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Introduzione al servizio tabelle di Azure in Java)</td> 
</tr> 
<tr> 
<td>Eliminazione entità/tabella</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Introduzione al servizio tabelle di Azure in Java)</td> 
</tr> 
<tr> 
<td>Inserimento/unione/sostituzione di entità</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Esempi di libreria client di archiviazione Java</a></td> 
</tr> 
<tr> 
<td>Query su entità</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Introduzione al servizio tabelle di Azure in Java)</td> 
</tr> 
<tr> 
<td>Query su tabelle</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Introduzione al servizio tabelle di Azure in Java)</td> 
</tr> 
<tr> 
<td>ACL/proprietà di tabella</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a> (Introduzione al servizio tabelle di Azure in Java)</td> 
</tr> 
<tr> 
<td>Aggiornamento di entità</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Esempi di libreria client di archiviazione Java</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Libreria di esempi di codice per Azure

libreria di esempio completo di hello tooview, andare toohello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=storage) libreria che sono inclusi esempi per l'archiviazione di Azure che è possibile scaricare ed eseguire in locale. Libreria di esempio di codice Hello fornisce il codice di esempio in formato zip. In alternativa, è possibile esplorare e clonare il repository GitHub hello per ogni esempio.

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>Guide introduttive

Estrarre hello seguenti guide se si sta cercando di istruzioni su come tooinstall e iniziare a utilizzare hello le librerie Client di archiviazione di Azure.

* [Getting Started with Azure Blob Service in Java](../blobs/storage-java-how-to-use-blob-storage.md) (Introduzione al servizio BLOB di Azure in Java)
* [Getting Started with Azure Queue Service in Java](../storage-java-how-to-use-queue-storage.md) (Introduzione al servizio di accodamento di Azure in Java)
* [Getting Started with Azure Table Service in Java](../../cosmos-db/table-storage-how-to-use-java.md) (Introduzione al servizio tabelle di Azure in Java)
* [Getting Started with Azure File Service in Java](../storage-java-how-to-use-file-storage.md) (Introduzione al servizio File di Azure in Java)

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su esempi con altri linguaggi:

* .NET: [Esempi di Archiviazione di Azure che usano .NET](../storage-samples-dotnet.md)
* Tutti gli altri linguaggi: [Esempi di archiviazione di Azure](../storage-samples.md)
