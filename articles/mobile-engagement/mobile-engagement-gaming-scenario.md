---
title: implementazione di Mobile Engagement aaaAzure per App di gioco
description: "Modalità di gioco app scenario tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Implementare Mobile Engagement con app di gioco
## <a name="overview"></a>Overview
Una startup del settore gaming ha lanciato una nuova app di gioco di ruolo e strategia ispirata al mondo della pesca. gioco di Hello è stato installato e in esecuzione per 6 mesi. Il gioco è enorme esito positivo, include milioni di download e memorizzazione hello è molto elevato tooother confrontati avvio gioco app. Riunione di revisione trimestrale hello, le parti interessate accettano che devono tooincrease Ricavi medi per utente (ARPU). All'interno del gioco sono disponibili pacchetti Premium come offerte speciali. Questi pacchetti di giochi consentono aspetto hello tooupgrade di utenti e le prestazioni delle loro righe pesca e ami da o tackles nel gioco hello. Le vendite di pacchetti, però, sono molto basse. Pertanto si decide prima tooanalyze hello analisi con uno strumento di analitica e quindi toodevelop un coinvolgimento programma tooincrease delle vendite tramite avanzate segmentazione.

In base a hello [Azure Mobile Engagement - Guida introduttiva alle procedure consigliate](mobile-engagement-getting-started-best-practices.md) la compilazione di una strategia di assunzione.

## <a name="objectives-and-kpis"></a>Obiettivi e indicatori KPI
Principali parti interessate per gioco hello soddisfano. Tutti concordano un obiettivo principale - vendite di pacchetto premium tooincrease del 15%. Vengono creati unità e toomeasure Business indicatori di prestazioni chiave (KPI), questo obiettivo

* Il livello di gioco hello vengono acquistati questi pacchetti
* Che cos'è ricavi hello per ogni utente, sessione, settimana e mese?
* Quali sono i tipi di acquisto Preferiti hello?

Parte 1 di hello [Guida introduttiva](mobile-engagement-getting-started-best-practices.md) spiega come toodefine hello obiettivi e indicatori KPI. 

Con hello che KPI aziendali ora definiti, hello Mobile prodotto Manager crea tendenze di indicatori KPI di Engagement toodetermine nuovo utente e di memorizzazione.

* Memorizzazione di monitoraggio e l'uso in hello seguenti intervalli: ogni giorno, ogni 2 giorni, ogni settimana, mese e ogni 3 mesi
* Conteggio degli utenti attivi
* classificazione app Hello in hello archiviare

In base alle raccomandazioni del team IT hello, hello seguenti tecnici indicatori KPI sono state aggiunte hello tooanswer seguenti domande:

* Percorso utente (pagina visitata e tempo dedicato alla pagina dall'utente)
* Numero di arresti anomali o bug rilevati per sessione
* Versione del sistema operativo degli utenti
* Che cos'è di dimensioni medie di hello dello schermo per gli utenti?
* Tipo di connessione Internet degli utenti

Per ogni indicatore KPI hello Mobile prodotto Manager specifica dati hello ha bisogno e in cui si trova nel proprio playbook.

## <a name="engagement-program-and-integration"></a>Programma di engagement e integrazione
Prima di compilare un programma engagement avanzate, hello Mobile progetto Director responsabile di progetto hello deve avere una conoscenza approfondita di come e quando i prodotti vengono utilizzati dagli utenti di hello.

Dopo 3 mesi, hello Director progetto Mobile è state raccolte sufficiente tooenhance dati le proprie vendite di notifica push all'interno dell'applicazione. Informazioni raccolte:

* primo acquisto Hello in genere si verifica a livello di hello 14. Per 90% di questi casi, acquisto hello è nuove armi erede per $3.
* 80% di questi casi, gli utenti che hanno effettuato un acquisto, continuare con il prodotto hello e rendere più acquisti.
* Gli utenti che hanno superato il livello di hello 20, avviare toospend maggiore di $10/ settimana.
* Gli utenti tendono a pacchetti premium toobuy livello 16, 24 e 32.

Ringrazia analysis toothis hello Mobile progetto Director decide toocreate push specifici notifica sequenze tooincrease nella vendita di app. Crea tre sequenze push denominate: programma di benvenuto, programma di vendita e programma utenti inattivi. Per ulteriori informazioni consultare toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
