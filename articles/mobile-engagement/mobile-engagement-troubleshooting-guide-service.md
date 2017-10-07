---
title: aaaAzure Mobile Engagement Troubleshooting Guide - servizio
description: Guide alla risoluzione dei problemi di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Guida alla risoluzione dei problemi relativi al servizio
di seguito Hello sono possibili problemi che possono verificarsi con la modalità di esecuzione di Azure Mobile Engagement.

## <a name="service-outages"></a>Interruzioni di servizio
### <a name="issue"></a>Problema
* Problemi causati da interruzioni del servizio di Azure Mobile Engagement toobe visualizzati.

### <a name="causes"></a>Cause
* I problemi causati da interruzioni del servizio di Azure Mobile Engagement toobe alle possono essere causati da diversi fattori:
  * Problemi isolati apparentemente originariamente tooall sistemica di Azure Mobile Engagement
  * Problemi noti causati da interruzioni del server (non sempre visualizzati nello stato del server).
  * Pianificazione ritardi, gli errori di assegnazione, problemi di aggiornamento di Badge, arresto statistiche raccolgono, Push smette di funzionare, API smettono di funzionare, nuove app o gli utenti Impossibile creare, errori DNS e gli errori di Timeout in hello dell'interfaccia utente, l'API o App in un dispositivo.
  * Interruzioni di dipendenza cloud [Stato del servizio Azure](http://status.azure.com/)
  * Interruzione di dipendenza servizi di notifica push (PNS, Push Notification Services)
  * Interruzioni di App Store

1) tootest toosee se il problema di hello dipende sistemico è possibile testare hello stessa funzione da un altro

* Applicazione integrata di Azure Mobile Engagement
* Dispositivo di test
* Versione del sistema operativo del dispositivo di test
* Campagna
* Account utente dell'amministratore
* Browser (Internet Explorer, Firefox, Chrome, ecc.)
* Computer

2) tootest se hello problema solo hello dell'interfaccia utente o hello dell'API:

* Test hello stessa funzione dell'interfaccia utente di Azure Mobile Engagement entrambi hello e hello dell'API di Azure Mobile Engagement.

3) tootest se hello problema con la rete cellulare:

* Eseguire test durante toohello connesso Internet tramite Wi-Fi e durante la connessione tramite la rete cellulare 3G.
* Verificare che il firewall non blocchi le porte o indirizzi IP di hello Azure Mobile Engagement.

4) tootest se hello problema con il dispositivo:

* Verificare se il dispositivo è in grado di tooconnect tooAzure Mobile Engagement con un'altra app integrata di Azure Mobile Engagement.
* Verificare che è possibile generare eventi, i processi e arresti anomali del sistema dal telefono che può essere visualizzato nell'interfaccia utente di Azure Mobile Engagement hello. 
* Verificare se è possibile inviare notifiche push dal dispositivo di tooyour dell'interfaccia utente di Azure Mobile Engagement hello in base all'ID la periferica. 

5) tootest se hello problema con l'App:

* Installare e testare l'applicazione da un emulatore anziché da un dispositivo fisico:

6) tootest se il problema di hello è un sistema operativo viene aggiornato tooend utente, dispositivi, che richiedono un tooresolve aggiornamento SDK:

* Testare l'applicazione in dispositivi diversi con versioni diverse di hello del sistema operativo.
* Confermare che si utilizza hello la versione più recente di hello SDK.

## <a name="connectivity-and-incorrect-information-issues"></a>Problemi di connettività e di informazioni non corrette
### <a name="issue"></a>Problema
* Problemi di accesso in hello dell'interfaccia utente di Azure Mobile Engagement.
* Errori di connessione con l'API di Azure Mobile Engagement hello.
* Problemi di caricamento dei tag Info App tramite hello Device API.
* Problemi relativi al download di registri o di dati esportati da Azure Mobile Engagement.
* Informazioni non corrette nell'interfaccia utente di Azure Mobile Engagement hello.
* Informazioni non corrette visualizzate nei registri di Azure Mobile Engagement.

### <a name="causes"></a>Cause
* Confermare che l'account utente disponga di sufficienti attività hello tooperform di autorizzazioni.
* Verificare che il problema di hello non è isolato tooone computer o la rete locale.
* Verificare che il servizio di Azure Mobile Engagement hello non ha le interruzioni segnalate.
* Confermare che i file relativi al tag di informazioni sull'app seguono tutte le regole seguenti:
  * Utilizzare hello solo set di caratteri UTF8 (set di caratteri ANSI hello non supportato).
  * Utilizzare la virgola "," come carattere separatore hello (è possibile aprire un carattere di separatore di servizio richiesta toorequest toochange hello CSV da una virgola carattere tooanother ",", ad esempio un punto e virgola ";").
  * Usare tutte le lettere minuscole per i valori Boolean "true" e "false".
  * Utilizzare un file di dimensioni inferiori a quelle delle dimensioni massime del file hello di 35MB.

