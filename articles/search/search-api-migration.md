---
title: aaaUpgrading toohello Azure API REST di ricerca versione 2016-09-01 | Documenti Microsoft
description: L'aggiornamento toohello Azure API REST di ricerca versione 2016-09-01
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>L'aggiornamento toohello Azure API REST di ricerca versione 2016-09-01
Se si utilizza la versione 2015-02-28 o 2015-02-28-Preview di hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx), in questo articolo consentirà di aggiornare l'applicazione toouse hello in genere disponibili API versione successiva, 01 / 09 / 2016.

Versione 2016-09-01 di hello API REST include alcune modifiche apportate da versioni precedenti. Le versioni sono abbastanza compatibili tra loro, pertanto la modifica del codice richiede un impegno minimo, a seconda della versione in uso prima. Vedere [tooupgrade passaggi](#UpgradeSteps) per istruzioni su come toochange il codice toouse hello nuova versione dell'API.

> [!NOTE]
> L'istanza del servizio di ricerca di Azure supporta più versioni API REST, tra cui hello più recente. È possibile continuare toouse una versione quando non è più hello più recente, ma è consigliabile eseguire la migrazione la versione più recente del codice toouse hello.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Novità della versione 2016-09-01
Versione 2016-09-01 è secondo rilascio generalmente disponibili hello di hello API REST del servizio ricerca di Azure. Le nuove funzionalità in questa versione dell'API includono:

* [Gli analizzatori personalizzati](https://aka.ms/customanalyzers), che consentono di controllo tootake hello del processo di conversione di testo in token indicizzabili e disponibile per la ricerca.
* [Archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md) e [archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md) indicizzatori, che consentono di tooeasily importare dati dall'archiviazione di Azure in ricerca di Azure in una pianificazione o su richiesta.
* [Campo di mapping](search-indexer-field-mappings.md), che consentono di toocustomize come importano dati di indicizzatori in ricerca di Azure.
* ETag, che consentono di definizioni di hello tooupdate degli indici, gli indicizzatori e origini dati in modo indipendente dalla concorrenza. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Passaggi tooupgrade
Se esegue l'aggiornamento dalla versione 2015-02-28, probabilmente sarà possibile toomake qualsiasi codice tooyour modifiche, diverso dal numero di versione di hello toochange. situazioni di Hello solo in cui potrebbe essere necessario codice toochange sono quando:

* Il codice ha esito negativo quando vengono restituite proprietà sconosciute in una risposta API. Per impostazione predefinita, l'applicazione deve ignorare le proprietà che non riconosce.
* Il codice rende persistenti le richieste API e tenta tooresend li toohello nuova versione dell'API. Ad esempio, questa situazione può verificarsi se l'applicazione mantiene i token di continuazione restituiti dall'API di ricerca hello (per ulteriori informazioni, cercare `@search.nextPageParameters` in hello [riferimento all'API di ricerca](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Se una delle situazioni seguenti si applicano tooyou, potrebbe essere toochange il codice di conseguenza. In caso contrario, non devono essere necessarie modifiche a meno che non si desidera toostart utilizzando hello [nuove funzionalità](#WhatsNew) della versione 2016-09-01.

Se esegue l'aggiornamento dalla versione 2015-02-28-Preview, si applica anche hello precedente, ma è inoltre necessario tenere presente che alcune funzionalità di anteprima non sono disponibili nella versione 2016-09-01:

* Supporto per gli indicizzatori di Archiviazione BLOB di Azure per i file e i BLOB con estensione csv contenenti matrici JSON.
* Sinonimi
* Query "Altri elementi simili"

Se il codice utilizza queste funzionalità, non sarà in grado di tooupgrade too2016-09-01, senza rimuovere l'utilizzo di essi.

> [!IMPORTANT]
> Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione.
> 
> 

## <a name="conclusion"></a>Conclusioni
Per ulteriori informazioni sull'utilizzo di hello API REST del servizio ricerca di Azure, vedere hello aggiornato di recente [riferimento all'API](https://msdn.microsoft.com/library/azure/dn798935.aspx) su MSDN.

I commenti degli utenti su Ricerca di Azure sono molto apprezzati. Se si verificano problemi, è disponibile tooask ci per informazioni su hello [forum MSDN di ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o [StackOverflow](http://stackoverflow.com/). Se si desidera che una domanda su Azure ricerca StackOverflow, assicurarsi che tootag con `azure-search`.

Grazie per avere usato Ricerca di Azure.

