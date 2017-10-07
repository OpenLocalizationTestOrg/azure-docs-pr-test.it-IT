---
title: origini dati di profilo tooData aaaHow
description: Come-tooarticle evidenziazione come dati a livello di tabella e di colonna tooinclude profili per la registrazione delle origini dati in Azure Data Catalog e come dati toouse profili toounderstand origini di dati.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Eseguire il profiling dati delle origini dati
## <a name="introduction"></a>Introduzione
**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. In altre parole, **Azure Data Catalog** è tutte sulle persone assistenza individuare, comprendere e utilizzare origini dati e aiutare le organizzazioni tooget più valore dai dati esistenti. Quando un'origine dati è registrata con **Azure Data Catalog**, i relativi metadati viene copiato e indicizzato dal servizio hello, ma storia hello non finisce qui.

Hello **Profiling dati** funzionalità di **Azure Data Catalog** esamina hello dati da origini dati supportate nel catalogo e raccoglie le statistiche e informazioni relativi a tali dati. È facile tooinclude un profilo di asset di dati. Quando si registra un asset di dati, scegliere **includono dati profilo** nello strumento di registrazione origine dati hello.

## <a name="what-is-data-profiling"></a>Informazioni sul profiling dati
Profiling dati esamina hello dati nell'origine dati hello in corso la registrazione e raccoglie le statistiche e informazioni relativi a tali dati. Durante l'individuazione di origine dati, queste statistiche consentono di determinare idoneità hello di hello dati toosolve il problema aziendale.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Hello origini dati seguenti supportano dati di profilatura:

* Viste e tabelle di SQL Server, inclusi database SQL di Azure e Azure SQL Data Warehouse.
* Viste e tabelle di Oracle
* Viste e tabelle di Teradata
* Tabelle Hive

Includendo i profili dati durante la registrazione degli asset di dati gli utenti possono rispondere a domande sulle origini dati, ad esempio:

* Può essere utilizzato toosolve il problema aziendale?
* Dati hello rispetta gli standard tooparticular o modelli?
* Quali sono alcune delle anomalie hello dell'origine dati hello?
* Quali sono i possibili problemi legati all'integrazione di questi dati nell'applicazione?

> [!NOTE]
> È anche possibile aggiungere documentazione tooan asset toodescribe come è possibile integrare i dati in un'applicazione. Vedere [come origini dati toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Come tooinclude un tipo di dati del profilo quando si registra un'origine dati
È facile tooinclude un profilo dell'origine dati. Quando si registra un'origine dati, in hello **toobe oggetti registrati** pannello della registrazione dell'origine dati hello strumento, scegliere **includono dati profilo**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

altre informazioni sulle toolearn tooregister le origini dati, vedere [come origini dati tooregister](data-catalog-how-to-register.md) e [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Applicazione di filtri su asset di dati che includono profili dati
toodiscover gli asset di dati che includono un profilo dati, è possibile includere `has:tableDataProfiles` o `has:columnsDataProfiles` come uno dei termini di ricerca.

> [!NOTE]
> Selezione **includono dati profilo** di hello dati strumento di registrazione di origine include sia la tabella informazioni sul profilo a livello di colonna. Tuttavia, hello API di catalogo dati consente dati asset toobe registrato con un solo set di informazioni sul profilo inclusi.
>
>

## <a name="viewing-data-profile-information"></a>Visualizzazione delle informazioni sul profilo dati
Dopo aver individuato l'origine dati appropriata con un profilo, è possibile visualizzare i dettagli del profilo dati hello. dati hello tooview del profilo, selezionare un asset di dati e scegliere **profilo dati** nella finestra del portale di hello catalogo dati.

![](media/data-catalog-data-profile/data-catalog-view.png)

Un profilo dati in **Azure Data Catalog** include informazioni sul profilo a livello di tabella e di colonna, ad esempio:

### <a name="object-data-profile"></a>Profilo dati dell'oggetto
* Numero di righe
* Dimensioni della tabella
* Ultimo aggiornamento dell'oggetto hello

### <a name="column-data-profile"></a>Profilo dati della colonna
* Tipo di dati della colonna
* Numero di valori distinct
* Numero di righe con valori NULL
* Deviazione minima, massima, media e standard per i valori di colonna

## <a name="summary"></a>Riepilogo
Profiling dati fornisce le statistiche e informazioni registrate toohelp asset di dati è determinare l'idoneità hello di problemi di hello dati toosolve aziendali. Oltre che annotare e documentare le origini dati, i profili dati permettono agli utenti di comprendere meglio i dati.

## <a name="see-also"></a>Vedere anche
* [Come origini dati tooregister](data-catalog-how-to-register.md)
* [Introduzione ad Azure Data Catalog](data-catalog-get-started.md)
