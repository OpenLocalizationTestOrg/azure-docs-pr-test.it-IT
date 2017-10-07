---
title: aaaAzure Engagement Mobile iOS note sulla versione di SDK | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Note sulla versione di Azure Mobile Engagement iOS SDK

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Risolto il problema delle notifiche cancellate in background.
* Risolto il problema degli avvisi in XCode 9 sulle API non chiamate nella coda principale.
* Risolto un problema di memoria nei poll di copertura.
* Eliminazione del supporto per iOS 6.X. A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 7.

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* Recapito del log migliorato in background.

## <a name="400-09122016"></a>4.0.0 (12/09/2016)
* Risolto il problema delle notifiche non prese in considerazione sui dispositivi iOS 10.
* Deprecare XCode 7.

## <a name="324-06302016"></a>3.2.4 (30/06/2016)
* Aggregazione fissa tra log tecnici e altri log.

## <a name="323-06072016"></a>3.2.3 (07/06/2016)
* Commenti e suggerimenti di recapito in cui non viene segnalato quando l'app è in background hello bug di hello fisso.
* Hello ottimizzato l'invio dei log tecniche.

## <a name="322-04072016"></a>3.2.2 (07/04/2016)
* Annullamento di richiesta HTTP con un conseguente talvolta toocrash correzione del bug.

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* Ritardo hello predefinito quando viene attivata una nuova istanza di applicazione da una notifica con collegamenti diretti

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Abilitato Bitcode in hello SDK toomake funziona con **Xcode 7**.
* Bug risolti correlati notifiche tooin-app.
* Apportate le notifiche in-app hello più affidabile in caso di batteria in esaurimento e altri scenari di questo tipo.
* Rimossi i registri aggiuntivi della console generati dalla libreria di terze parti 3.

## <a name="310-08262015"></a>3.1.0 (08/26/2015)
* Correzione del bug di compatibilità di iOS 9 con una libreria di terze parti. Provocava arresti anomali durante l'invio del polling dei risultati, di informazioni sull'applicazione o di dati aggiuntivi.

## <a name="300-06192015"></a>3.0.0 (19/06/2015)
* Mobile Enagement usa le notifiche push Silent.
* Eliminazione del supporto per iOS 4.X. A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 6.

## <a name="220-05212015"></a>2.2.0 (21/05/2015)
* id del dispositivo Mobile Engagement Hello per i dispositivi < iOS 6 è basata su un GUID generato in fase di installazione.

## <a name="210-04242015"></a>2.1.0 (24/04/2015)
* È stata aggiunta la compatibilità per Swift.
* Quando si fa clic su una notifica, l'azione hello che URL viene ora eseguita destra dopo l'apertura di un'applicazione hello.
* È stato aggiunto il file di intestazione mancante nel pacchetto dell'SDK.
* Risolto un problema quando reporter di arresto anomalo di Mobile Engagement hello è stato disabilitato.

## <a name="200-02172015"></a>2.0.0 (17/02/2015)
* Versione iniziale di Azure Mobile Engagement
* La configurazione di appId/sdkKey viene sostituita da una configurazione della stringa di connessione.
* Rimosso toosend API e ricevere messaggi XMPP arbitrari da entità XMPP arbitraria.
* Rimosso toosend API e ricevere messaggi tra i dispositivi.
* Sono stati introdotti miglioramenti per la sicurezza.
* È stato eliminato il rilevamento di SmartAd.
