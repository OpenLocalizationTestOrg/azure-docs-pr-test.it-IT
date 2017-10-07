---
title: applicazione Proxy di applicazione aaaAn accetta tooload troppo lungo | Documenti Microsoft
description: Risolvere i problemi di prestazioni di caricamento pagina con hello Proxy dell'applicazione Azure Active
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Un'applicazione di Proxy applicazione impiega troppo tempo tooload

Questo articolo è utile toounderstand perché un'applicazione Proxy dell'applicazione Azure Active Directory potrebbe richiedere un tooload molto tempo e cosa è possibile eseguire tooresolve questo problema.

## <a name="overview"></a>Panoramica
Se le applicazioni funzionino ma vedrai una latenza prolungata, è possibile alcune modifiche di lieve entità nella topologia di rete che è possibile prendere in considerazione velocità hello tooimprove. Per una versione di valutazione di diverse topologie, vedere hello [documento considerazioni sulla rete](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Se queste considerazioni non sono utili, purtroppo al momento non abbiamo altri consigli per ottimizzare le prestazioni. Come servizio Proxy applicazione hello espande toomore data Center che possono essere tooyou più vicino, è possibile avviare direttamente latenza toosee migliorata. Centra elenco completo di hello toosee dei dati di Azure, è possibile visualizzare hello [pagina di prova di latenza](http://www.azurespeed.com/Azure/Latency). 

Hello data center con il servizio Proxy di applicazione hello è disponibile con hello [connettore porte Test strumento](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Commenti sulle posizioni dei data center del proxy di applicazione 
È possibile data center di Azure che non include ancora Proxy dell'applicazione ma potrebbe causare miglioramento latenza grande tooa automaticamente. posizione in Hello del data center < aadapfeedback@microsoft.com > per poterlo utilizzare tooplan i commenti e suggerimenti quando si espande.

Si stanno lavorando alcune funzionalità aggiuntive che consentono di migliorare latenza hello per i tenant che attualmente vedere latenze lungo e che documentazione tooshare una volta disponibile.

## <a name="next-steps"></a>Passaggi successivi
[Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md)
