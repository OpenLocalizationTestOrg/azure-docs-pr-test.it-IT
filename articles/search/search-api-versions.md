---
title: versioni di aaaAPI di ricerca di Azure | Documenti Microsoft
description: Criteri di versione per le API REST di ricerca di Azure e hello libreria client .NET SDK hello.
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Versioni API in Ricerca di Azure
Il servizio Ricerca di Azure Search distribuisce regolarmente aggiornamenti delle funzionalità. A volte, ma non sempre, questi aggiornamenti richiedono la toopublish una nuova versione di compatibilità con le versioni precedenti di toopreserve l'API. Una nuova versione di pubblicazione consente toocontrol quando e come si integrano gli aggiornamenti del servizio di ricerca nel codice.

Come regola, si tenta toopublish nuove versioni solo quando necessario, poiché può comportare alcuni tooupgrade sforzo la versione di toouse una nuova API di codice. Una nuova versione verranno pubblicate solo se è necessario toochange alcuni aspetti di hello API in modo che interrompe la compatibilità con le versioni precedenti. Questa situazione può verificarsi a causa di correzioni tooexisting funzionalità o a causa di nuove funzionalità che modificano una superficie API esistente.

Si seguirà hello stessa regola per gli aggiornamenti SDK. Ricerca di Azure SDK Hello segue hello [controllo delle versioni semantico](http://semver.org/) regole, che significa che la versione è costituito da tre parti: principale, secondario e build numero (ad esempio, 1.1.0). Si rilascerà una nuova versione principale di hello SDK solo in caso di modifiche che interrompono la compatibilità con le versioni precedenti. Per aggiornamenti delle funzionalità non è importante, si incrementa la versione secondaria hello e per le correzioni di bug si aumenterà solo versione di build hello.

> [!NOTE]
> L'istanza del servizio di ricerca di Azure supporta più versioni API REST, tra cui hello più recente. È possibile continuare toouse una versione quando non è più hello più recente, ma è consigliabile eseguire la migrazione la versione più recente del codice toouse hello. Quando si utilizza l'API REST di hello, è necessario specificare una versione dell'API hello in ogni richiesta tramite il parametro api-version hello. Quando si utilizza hello .NET SDK, versione di hello di hello SDK in uso determina versione corrispondente di hello di hello API REST. Se si utilizza un SDK precedente, è possibile continuare toorun che il codice senza apportare modifiche anche se il servizio di hello è la versione aggiornata toosupport un'API più recente.

## <a name="snapshot-of-current-versions"></a>Panoramica delle versioni correnti
Di seguito è uno snapshot di hello versioni correnti di tooAzure interfacce di programmazione tutti ricerca.

| Interfacce | Versione principale più recente | Stato |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |Disponibile a livello generale, rilasciata a novembre 2016 |
| [Anteprima di .NET SDK](https://aka.ms/search-sdk-preview) |2.0-preview |anteprima, rilasciata ad agosto 2016 |
| [API REST del servizio](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Disponibile a livello generale |
| [Anteprima API REST del servizio](search-api-2015-02-28-preview.md) |2015-02-28-Preview |Preview |
| [.NET Management SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Disponibile a livello generale |
| [API REST di gestione](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Disponibile a livello generale |

Per le API REST, tra cui hello hello `api-version` è necessaria per ogni chiamata. Questo rende facile tootarget una versione specifica, ad esempio un'API di anteprima. Hello seguente viene illustrato come hello `api-version` parametro specificato:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Benché ogni richiesta abbia un `api-version`, è consigliabile usare hello stessa versione per tutte le richieste API. Ciò vale soprattutto nel caso in cui nuove versioni API introducano attributi oppure operazioni non riconosciuti dalle versioni precedenti. La combinazione di diverse versioni API può avere conseguenze impreviste e deve essere evitata.
>
> Hello API REST del servizio e l'API REST di gestione dispongono di versioni indipendentemente uno da altro. L'eventuale somiglianza del numero di versione è causale.

In genere disponibile (o GA) API può essere utilizzate nell'ambiente di produzione e sono soggetto tooAzure contratti di servizio. Versioni di anteprima hanno funzionalità sperimentali che non sono sempre versione tooa migrati GA. **È consigliabile evitare l'utilizzo delle API di anteprima in applicazioni di produzione.**

## <a name="about-preview-and-generally-available-versions"></a>Informazioni sull'anteprima e sulle versioni disponibili a livello generale
Ricerca di Azure sempre pre-rilascia funzionalità sperimentali tramite API REST hello in primo luogo, quindi tramite le versioni non definitive di hello .NET SDK.

Le funzionalità di anteprima non sono garantite toobe versione GA tooa migrati. Mentre le funzionalità in una versione GA vengono considerate stabili e non scontato toochange con eccezione hello piccole correzioni di compatibilità e miglioramenti, le funzionalità di anteprima sono disponibili per il test e la sperimentazione, con l'obiettivo di hello di raccogliere commenti e suggerimenti su fase di progettazione e implementazione.

Tuttavia, poiché le funzionalità di anteprima sono toochange soggetto, è consigliabile evitare la scrittura di codice di produzione che assume una dipendenza su versioni di anteprima. Se si utilizza una versione di anteprima precedente, si consiglia di eseguire la migrazione versione di toohello disponibile a livello generale (GA).

Per .NET SDK hello: linee guida per la migrazione di codice è reperibile in [hello aggiornamento .NET SDK](search-dotnet-sdk-migration.md).

Disponibilità generale si intende che ricerca di Azure si trova sotto hello contratto di servizio (SLA). Hello contratto di servizio è reperibile in [contratti del servizio di ricerca di Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
