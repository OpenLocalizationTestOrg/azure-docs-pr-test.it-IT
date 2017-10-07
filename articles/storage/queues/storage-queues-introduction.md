---
title: aaaIntroduction tooAzure l'archiviazione delle code | Documenti Microsoft
description: Introduzione tooAzure l'archiviazione delle code
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Introduzione tooQueues

Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.

## <a name="common-uses"></a>Utilizzi comuni

Di seguito sono riportati gli utilizzi più comuni per il servizio di archiviazione di accodamento.

* Creazione di un backlog di lavoro tooprocess in modo asincrono
* Passaggio di messaggi da un ruolo di lavoro di Azure tooan ruolo web di Azure

## <a name="queue-service-concepts"></a>Concetti del servizio di accodamento

servizio di Accodamento Hello contiene hello seguenti componenti:

![Concetti delle code](./media/storage-queues-introduction/queue1.png)

* **Formato URL:** le code sono indirizzabili mediante hello seguendo il formato di URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    una coda nel diagramma hello è concepito Hello URL seguente:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Per informazioni sulla capacità dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .

* **Coda:** una coda contiene un set di messaggi. Tutti i messaggi devono essere inclusi in una coda. Il che nome della coda hello debba essere tutti in lettere minuscole. Per altre informazioni, vedere [Denominazione di code e metadati](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **Messaggio:** un messaggio, in qualsiasi formato, di too64 KB. tempo massimo di Hello che un messaggio può rimanere nella coda di hello è sette giorni.

## <a name="next-steps"></a>Passaggi successivi

* [Creare un account di archiviazione](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Introduzione alle code con .NET](storage-dotnet-how-to-use-queues.md)
