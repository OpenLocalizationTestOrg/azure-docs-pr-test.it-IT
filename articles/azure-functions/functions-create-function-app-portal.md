---
title: un'app di funzione dal portale di Azure hello aaaCreate | Documenti Microsoft
description: Creare una nuova funzione app in Azure App Service dal portale hello.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Creare un'app di funzione dal portale di Azure hello

Le app di Azure (funzione) utilizza l'infrastruttura di Azure App Service hello. In questo argomento illustra come un'app di funzione nel portale di Azure hello toocreate. Un'app di funzione è contenitore hello che ospita l'esecuzione di hello delle singole funzioni. Quando si crea un'app di funzione nel piano di hosting del servizio App hello, l'app di funzione può utilizzare tutte le funzionalità di hello di servizio App.

## <a name="create-a-function-app"></a>Creare un'app per le funzioni

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Quando si crea un'app per le funzioni, inserire un **nome dell'app** valido, che contenga solo lettere, numeri e trattini. Il carattere di sottolineatura (**_**) non è consentito.

I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole. Nome dell'account di archiviazione deve essere univoco all'interno di Azure. 

Dopo la creazione di app di funzione hello, è possibile creare le singole funzioni in uno o più lingue diverse. Creare funzioni [tramite il portale di hello](functions-create-first-azure-function.md#create-function), [distribuzione continua](functions-continuous-deployment.md), o da [caricamento con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Piani di servizio

Funzioni di Azure offre due piani di servizio diversi: piano a consumo e piano di servizio app. piano di consumo Hello alloca automaticamente potenza di calcolo quando viene eseguito il codice, scale-out come carico toohandle necessarie e quindi scale-in quando codice non è in esecuzione. piano di servizio App Hello offre la funzione funzionalità di app accesso tooall hello del servizio App. È necessario scegliere il piano di servizio quando viene creata l'app per le funzioni, che al momento non può essere modificato. Per altre informazioni, vedere [Scegliere un piano di hosting di Funzioni di Azure](functions-scale.md).

Se si intende toorun funzioni JavaScript in un piano di servizio App, è consigliabile scegliere un piano con un minor numero di core. Per ulteriori informazioni, vedere hello [riferimento JavaScript per le funzioni](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Requisiti dell'account di archiviazione

Quando si crea un'app di funzione nel servizio App, è necessario creare o collegare tooa generico account di archiviazione di Azure che supporta l'archiviazione Blob, coda e tabella. Le funzioni usano internamente l'archiviazione per operazioni come la gestione dei trigger e la registrazione dell'esecuzione delle funzioni. Alcuni account di archiviazione, come gli account di archiviazione solo BLOB, Archiviazione Premium di Azure e gli account di archiviazione di uso generico con replica ZRS, non supportano code e tabelle. Questi account vengono filtrati dal Pannello di Account di archiviazione hello durante la creazione di un'app di funzione.

>[!NOTE]
>Quando si utilizza piano di hosting hello consumo, i file di configurazione codice e l'associazione di funzione sono archiviati nell'archiviazione di File di Azure nell'account di archiviazione principale hello. Quando si elimina l'account di archiviazione principale hello, questo contenuto viene eliminato e non può essere recuperato.

toolearn ulteriori informazioni sui tipi di account di archiviazione, vedere [Introduzione a servizi di archiviazione di Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



