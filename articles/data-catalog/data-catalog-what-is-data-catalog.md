---
title: aaaIntroduction tooAzure catalogo dati | Documenti Microsoft
description: "In questo articolo viene fornita una panoramica di Microsoft Azure Data Catalog, incluse le funzionalità e consente di risolvere i problemi di hello. Catalogo dati consente a qualsiasi tooregister utente, individuare, comprendere e utilizzare le origini dati."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 82144c440b5692d3608af08208f36ee8e6dfdc93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-data-catalog"></a>Che cos'è il Catalogo dei dati di Azure?
Azure Data Catalog è un servizio cloud completamente gestito con gli utenti possono individuare le origini dati hello necessari e comprendere le origini dati hello individuati. In hello stesso tempo get di organizzazioni Data Catalog consente più valore gli investimenti esistenti. 

Con Data Catalog qualsiasi utente, dagli analisti ai data scientist fino agli sviluppatori, può individuare, comprendere e utilizzare le origini dati. Data Catalog include un modello crowdsourcing di metadati e annotazioni. È una posizione centrale per tutti i toocontribute gli utenti dell'organizzazione le proprie conoscenze e compilare una community e lingua dei dati.

## <a name="discovery-challenges-for-data-consumers"></a>Difficoltà di individuazione per i consumer di dati
Tradizionalmente, l'individuazione di origini dati aziendali è stato un processo organico basato su conoscenze specifiche. Per le aziende che desiderano tooget hello compreso la maggior parte delle risorse di informazioni, questo approccio presenta numerosi problemi:

* Gli utenti potrebbero non sapere dell'esistenza di un'origine dati, a meno che non la individuino nel corso di un altro processo. Non c'è una posizione centrale in cui le origini dati vengono registrate.
* A meno che gli utenti sanno percorso hello di un'origine dati, non possono quindi connettersi toohello dati tramite un'applicazione client. Esperienze di utilizzo di dati richiedono una stringa di connessione di utenti tooknow hello o il percorso.
* A meno che gli utenti sanno percorso hello della documentazione relativa a un'origine dati, che non comprendono hello destinato utilizza dati hello. Documentazione e origini dati possono trovarsi in varie posizioni e ed essere utilizzate in diversi modi.
* Se gli utenti eventuali domande su una risorsa di informazioni, gli utenti devono individuare esperto hello o un team responsabile dei dati di hello e coinvolgere le offline. Non c'è alcuna connessione esplicita tra dati e persone esperte del loro uso.
* A meno che gli utenti comprendono il processo di hello per la richiesta di origine dati di access toohello, individuare l'origine dati hello e la relativa documentazione ancora non aiutarlo accedere ai dati hello.

## <a name="discovery-challenges-for-data-producers"></a>Difficoltà di individuazione per i produttori di dati
Anche se in precedenza sfide hello faccia consumer di dati, gli utenti che sono responsabili per la produzione e Gestione risorse informative affrontano problematiche di propri:

* L'annotazione delle origini dati con metadati descrittivi è spesso una fatica inutile. Le applicazioni client ignorano in genere le descrizioni che vengono archiviate nell'origine dati hello.
* La creazione di documentazione per le origini dati è spesso una fatica inutile. La sincronizzazione della documentazione con le origini dati è un lavoro continuativo e gli utenti potrebbero non fidarsi della documentazione, ritenuta obsoleta.
* La creazione e la manutenzione della documentazione per le origini dati sono operazioni lunghe e complesse. Eseguendo tale tooeveryone immediatamente disponibile la documentazione che utilizza l'origine dati hello può essere una quantità ancora maggiore.
* Limitare l'accesso toodata origini e assicurare che i consumer di dati è noto come accesso toorequest è una richiesta in corso.

Quando tali problemi vengono combinati, che presentano un ostacolo significativo per le società che desidera tooencourage e alzare di livello utilizzare hello e comprensione dei dati aziendali.

## <a name="azure-data-catalog-can-help"></a>Utilità di Azure Data Catalog
Catalogo dati è progettato tooaddress questi problemi e toohelp aziende get hello più valore dalle risorse di informazioni esistenti. Catalogo dati rende origini dati facilmente individuabili e comprensibile agli utenti di hello che gestiscono i dati hello.

Data Catalog fornisce un servizio basato sul cloud in cui le origini dati possono essere registrate. Hello dati restano nel relativo percorso esistente, ma una copia dei metadati viene aggiunto tooData catalogo, insieme a un percorso di origine dati di riferimento toohello. Hello metadati è indicizzata toomake facilmente individuabili tramite ricerca e gli utenti toohello comprensibile individuato da ogni origine dei dati.

Dopo la registrazione di un'origine dati, i metadati possono quindi arricchire, da utente hello registrato o da altri utenti nell'organizzazione hello. Tutti gli utenti possono annotare un'origine dati, fornendo descrizioni, tag o altri metadati, come ad esempio la documentazione e i processi per richiedere l’accesso all’origine dati. Questi metadati descrittivi integrano hello strutturale dei metadati (ad esempio i tipi di dati e i nomi di colonna) registrato dall'origine dati hello.

Individuazione e informazioni sulle origini dati e il relativo utilizzo è scopo principale di hello di registrazione di origini di hello. Gli utenti dell'organizzazione potrebbero essere necessari dati per la business intelligence, lo sviluppo di applicazioni, analisi scientifica dei dati o qualsiasi altra attività in cui i dati di destra hello sono richiesto. È possibile utilizzare hello catalogo dati di individuazione esperienza tooquickly trovare i dati che corrisponda alle proprie esigenze, comprendere hello dati tooevaluate relativa idoneità a scopo di hello e utilizzare i dati di hello aprendo l'origine dati hello nello strumento di loro scelta. 

AT hello stesso tempo, gli utenti possono contribuire a catalogo toohello dall'assegnazione di tag, la documentazione e annotazione delle origini dati che sono già state registrate. È anche possibile registrare nuove origini dati, che quindi possono essere individuate, compreso e utilizzate dalla community di hello di utenti del catalogo.

![Funzionalità di Data Catalog](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a>Altre informazioni su Data Catalog
toolearn ulteriori informazioni su funzionalità hello del catalogo dati, vedere:

* [Come origini dati tooregister](data-catalog-how-to-register.md)
* [Come origini dati toodiscover](data-catalog-how-to-discover.md)
* [Come origini dati tooannotate](data-catalog-how-to-annotate.md)
* [Come origini dati toodocument](data-catalog-how-to-documentation.md)
* [Come origini toodata tooconnect](data-catalog-how-to-connect.md)
* [Come toowork dati di grandi dimensioni](data-catalog-how-to-big-data.md)
* [Come asset di dati toomanage](data-catalog-how-to-manage.md)
* [Come tooset backup hello glossario aziendale](data-catalog-how-to-business-glossary.md)
* [Domande frequenti](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a>Passaggi successivi
tooget avviato con il catalogo dati, vedere:
* [Microsoft Azure Data Catalog](https://www.azuredatacatalog.com)
* [Introduzione al Catalogo dati di Azure](data-catalog-get-started.md)
