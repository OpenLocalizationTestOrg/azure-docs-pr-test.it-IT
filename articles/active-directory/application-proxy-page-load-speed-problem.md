---
title: Il caricamento dell'applicazione del proxy di applicazione impiega troppo tempo | Microsoft Docs
description: Risoluzione dei problemi delle prestazioni di caricamento della pagina con il proxy di applicazione di Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a>Il caricamento dell'applicazione del proxy di applicazione impiega troppo tempo

Questo articolo aiuta a comprendere perché il caricamento di un'applicazione del proxy di applicazione di Azure AD potrebbe impiegare troppo tempo e illustra cosa è possibile fare per risolvere tale problema.

## <a name="overview"></a>Panoramica
Se le applicazioni funzionano ma si riscontra una lunga latenza, per migliorare la velocità potrebbero essere prese in considerazione piccole modifiche da applicare alla topologia di rete. Per una valutazione delle diverse topologie, consultare il [documento relativo alle considerazioni sulla rete](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Se queste considerazioni non sono utili, purtroppo al momento non abbiamo altri consigli per ottimizzare le prestazioni. Quando il servizio proxy di applicazione si espande a più data center in prossimità dell'utente, potrebbe essere possibile iniziare a vedere direttamente un miglioramento della latenza. Per un l'elenco completo dei data center di Azure, è possibile visualizzare la [pagina di prova della latenza](http://www.azurespeed.com/Azure/Latency). 

I data center con il servizio proxy di applicazione sono disponibili con lo [strumento per il test delle porte del connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Commenti sulle posizioni dei data center del proxy di applicazione 
Potrebbero essere presenti data center di Azure che non includono ancora il proxy di applicazione e, di conseguenza, potrebbero migliorare di tanto la latenza. È possibile inviare un feedback sulla posizione dei data center all'indirizzo <aadapfeedback@microsoft.com>, che potremo utilizzare per i futuri piani di espansione.

Stiamo inoltre lavorando per aggiungere funzionalità in grado di migliorare la latenza per i tenant che attualmente riscontrano tempi di latenza troppo lunghi. Condivideremo tutta la documentazione non appena disponibile.

## <a name="next-steps"></a>Passaggi successivi
[Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md)
