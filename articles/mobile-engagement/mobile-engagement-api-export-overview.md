---
title: Panoramica dell'API esportare Engagement aaaMobile
description: Informazioni su hello nozioni fondamentali per l'esportazione dei dati non elaborati generato da tooleverage dispositivi dell'utente in strumenti personalizzati
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Panoramica dell'API di esportazione di Mobile Engagement
## <a name="introduction"></a>Introduzione
In questo documento, si apprenderà hello nozioni fondamentali per l'esportazione dei dati non elaborati generato da tooleverage dispositivi dell'utente in strumenti personalizzati.

## <a name="pre-requisites"></a>Prerequisiti
L'esportazione di dati non elaborati hello da Mobile Engagement richiede:

* Toobe toouse in grado di hello API di API autenticazione programma di installazione (vedere [installazione manuale di autenticazione](mobile-engagement-api-authentication-manual.md)),
* Utilizzare le API REST hello o hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Un account dell'Archiviazione di Azure.

> [!NOTE]
> È inoltre consigliabile hello eccellente [Microsoft Azure Storage Explorer](http://storageexplorer.com/), almeno durante la fase di sviluppo hello perché fornisce un semplice toouse dell'interfaccia utente per l'interazione con l'archiviazione di Azure.
> 
> 

## <a name="what-can-be-exported"></a>Cosa può essere esportato
Engagement mobile consente relativo toocollect utenti molti tipi di dati e pertanto dispongono di diversi tipi di esportazione adatto toothese diversi tipi di dati.
Esistono due tipi fondamentali di esportazione:

* Snapshot: in genere utilizzato tooexport dati che rappresenta uno stato e per cui Mobile Engagement non dispone di una cronologia. Tali dati includono tag (app-info), token o commenti e suggerimenti di campagne push. Di conseguenza questi tipi di esportazione non sono correlati tooa Data.
* Cronologica: questo tipo di esportazione viene usato per i dati che si accumulano nel tempo, ad esempio eventi o attività.

Hello tabla reputano tutte hello possibili le esportazioni:

| Export Type | Tipo di dati | Descrizione |
| --- | --- | --- |
| Snapshot |Push |Genera un'esportazione di commenti e suggerimenti di campagne push in base all'ID dispositivo o all'utente |
| Snapshot |Tag |Genera un'esportazione di hello tag (app-info) associati tooeach dispositivi |
| Snapshot |Dispositivo |Genera un'esportazione della maggior parte dei dati di hello sui dispositivi, ad esempio technicals hello (modello, delle impostazioni locali, fuso orario,...), il tag di hello, visto prima,... |
| Snapshot |token |Genera un'esportazione di tutti i token validi hello |
| Cronologica |Attività |Genera un'esportazione di tutte le attività di hello per ogni tipo di dispositivi in un determinato periodo di tempo |
| Cronologica |Evento |Genera un'esportazione di tutte le attività di hello per ogni tipo di dispositivi in un determinato periodo di tempo |
| Cronologica |Job |Genera un'esportazione di tutti i processi di hello per ogni tipo di dispositivi in un determinato periodo di tempo |
| Cronologica |Errore |Genera un'esportazione di tutti gli errori di hello per ogni tipo di dispositivi in un determinato periodo di tempo |

## <a name="how-does-it-work"></a>Come funziona?
Le esportazioni sono attività a esecuzione prolungata che potrebbero generare file di dati di grandi dimensioni. Per questo motivo, non possono essere richiamati tooreturn immediatamente un toodownload di file.
Ordinare i dati di tooexport da Mobile Engagement, sarà necessario toocreate un **processo di esportazione** tramite l'API in cui è in genere specificare:

* tipo di Hello di esportazione (snapshot o cronologia)
* tipo di dati Hello,
* Hello **contenitore di archiviazione Azure** (inclusa una firma di accesso condiviso valido con accesso in scrittura) in cui verrà scritto il risultato di hello dell'esportazione hello.
* Il parametro dell'URL del contenitore sarà ad esempio https://[NomeAccountArchiviazione].blob.core.windows.net/[NomeContenitore]?[TokenAutorizzazioniScritturaFirmaAccessoCondiviso]  

Ecco un esempio reale: https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

Si noti che potrebbe richiedere alcuni minuti per toobe il processo avviato e quindi, potrà essere eseguito da alcuni secondi per le ore tooseveral App leggera per applicazioni con numerosi utenti o attività.

Una volta creato il processo di hello, è possibile toocheck toosee il relativo stato, se è ancora in esecuzione o se è stata completata.

Dopo che ha avuto esito positivo processo hello, file di dati risultante hello è disponibile nel contenitore di archiviazione fornito hello.

