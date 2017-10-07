---
title: aaaI utilizzare servizi mobili, come servizio App consente?
description: Informazioni su quali vantaggi servizio App garantisce tooyour progetti di servizi mobili esistenti.
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>In che modo può essere utile il servizio app per gli utenti di Servizi mobili?
## <a name="overview"></a>Panoramica
Il servizio mobile esistente è al sicuro e continuerà ad essere supportato. Tuttavia sono presenti numeri di hello vantaggi *Azure App Service* piattaforma sono disponibili per app per dispositivi mobili che non sono attualmente disponibili con i servizi mobili:

* Offerte semplificate e più economiche per app che includono client sia Web che mobili.
* Nuove funzionalità host che includono processi Web, CName personalizzati e monitoraggio migliorato.
* Integrazione chiavi in mano con Gestione traffico.
* Connettività tooyour alle risorse locali e l'utilizzo di rete virtuale in tooHybrid inoltre le connessioni VPN
* Monitoraggio, avvisi e risoluzione dei problemi delle app con NewRelic o AppInsights
* Più dettagliato gamma di risorse di calcolo sottostante hello e prezzi
* Scalabilità automatica predefinita, bilanciamento del carico e monitoraggio delle prestazioni.
* Funzionalità predefinite di gestione temporanea, backup, rollback e test in ambiente di produzione.

## <a name="new-hosting-features"></a>Nuove funzionalità di hosting
In *Azure App Service* hello *App Mobile* esegue codice di back-end in hello stesso contenitore di App Web e App per le API. Di conseguenza è possibile sfruttare tutte le funzionalità di hello in questo contenitore, inclusi alcuni di quelli che non sono attualmente presenti nei servizi mobili:

* Aggiunta di logica back-end in continua esecuzione tramite processi Web
* Garanzia che il codice back-end sia sempre in esecuzione
* Utilizzare descrittivo personalizzato tooprovide di record CNAME e stabile nomi tooyour gli endpoint di back-end mobile
* Scalabilità geografica dell'app con Gestione traffico
* Inserimento di tutte le librerie e i pacchetti desiderati.
* (Per .NET) Uso delle funzionalità di ASP.NET, tra cui MVC
* (Per Node. js) Utilizzare qualsiasi libreria JavaScript pura dell'ecosistema di nodo hello, incluse le librerie comuni di MVC.

## <a name="access-on-premises-data-using-vnet"></a>Accesso ai dati locali tramite reti virtuali
Con i servizi mobili è già possibile usare le connessioni ibride tooaccess risorse locali. Vi sono tuttavia alcune situazioni in cui una soluzione VPN è preferibile. Con il *servizio app di Azure* , è possibile usare la rete virtuale di Azure per il codice back-end delle app per dispositivi mobili.

## <a name="use-your-favorite-backend-language"></a>Uso del linguaggio back-end preferito
*Servizio App di Azure* offerte più ampie e supporto avanzato per le piattaforme ASP.NET e Node.js, tra cui accesso toohello di runtime più recente.

## <a name="set-up-automatic-scale"></a>Impostazione della scalabilità automatica
Con Servizi mobili, tutte le istanze del codice back-end vengono eseguite in macchine virtuali del tipo Piccola. *Servizio App di Azure* consente dimensioni hello tooselect delle macchine virtuali da un set di opzioni molto più dettagliato. È possibile inoltre possibile scalare orizzontalmente o verticalmente toohandle qualsiasi carico di clienti in ingresso, in base alle diverse metriche delle prestazioni.

## <a name="be-in-hello-know"></a>Essere in hello "sa"
Tooissues di rispondere in tempo reale con monitoraggio e gli avvisi tooautomatically notificare e al team. Integrazione analitica app avanzate e le funzionalità di monitoraggio da New Relic e AppInsights tooget arricchire comprensione delle prestazioni di app per dispositivi mobili. Con *Azure App Service* è ora possibile configurare avvisi basati su vasta gamma di metriche delle prestazioni a livello di codice e tramite hello portale di Azure.

## <a name="keep-your-assets-safe"></a>Asset sempre al sicuro
Backup automatico del back-end e del database. Il codice e dati è protetta da emergenza e facilmente ripristinati, consentendo toorun azienda con confidenza.

## <a name="ready-stage-go"></a>Sviluppo, test, produzione
Con il *servizio app di Azure* è ora possibile creare più ambienti privati di test e staging per le app per dispositivi mobili. Utilizzare tooperform test prima di distribuire. Scambiare tooproduction senza tempi di inattività. Le app Web sono precaricate, garantendo una migliore esperienza di hello.

È possibile iniziare a usare il *servizio app* sperimentando i vantaggi per il servizio mobile esistente seguendo questa [esercitazione](app-service-mobile-migrating-from-mobile-services.md).
