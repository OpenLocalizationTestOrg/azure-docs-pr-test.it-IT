---
title: supporto aaaHTTP/2 nella rete CDN di Azure | Documenti Microsoft
description: Informazioni sul supporto HTTP/2 e la rete CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Supporto HTTP/2 nella rete CDN di Azure

HTTP/2 è tooHTTP/1.1\ una revisione principale. Fornisce più velocemente esperienza utente migliorata, tempo di risposta ridotto e delle prestazioni web, mantenendo i metodi HTTP familiarità hello, codici di stato e semantica. HTTP/2, anche se toowork progettato con HTTP e HTTPS, molti browser web client supportano solo HTTP/2 tramite TLS.

###<a name="http2-benefits"></a>Vantaggi di HTTP/2

Hello HTTP/2 seguenti vantaggi:

*   **Multiplexing e concorrenza**

    Usando HTTP 1.1, se si eseguono più richieste di risorse multiple sono necessarie più connessioni TCP e a ogni connessione è associato un overhead delle prestazioni. HTTP/2 consente più toobe risorse richiesto in una singola connessione TCP.

*   **Compressione delle intestazioni**

    Comprimendo le intestazioni HTTP hello per le risorse fornite, tempo durante la trasmissione hello viene ridotto in modo significativo.

*   **Dipendenze del flusso**

    Dipendenze di flusso consentono ai client hello tooindicate toohello server quali risorse hanno la priorità.


##<a name="http2-browser-support"></a>Supporto browser HTTP/2

Tutti i browser principali hello stato implementato il supporto HTTP/2 le versioni correnti. Browser non supportati verranno automaticamente il fallback tooHTTP/1.1.

|Browser|Versione minima|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Abilitazione del supporto HTTP/2 nella rete CDN di Azure

Attualmente il supporto HTTP/2 è attivo per i profili di **rete CDN di Azure di Akamai** e di **rete CDN di Azure di Verizon**. Non è necessaria alcuna azione da parte dei clienti.

##<a name="next-steps"></a>Passaggi successivi

vantaggi di hello toosee HTTP/2 in azione, vedere [questa demo da Akamai](https://http2.akamai.com/demo).

toolearn ulteriori informazioni su HTTP/2, visitare hello seguenti risorse:

*   [Home page delle specifiche HTTP/2](https://http2.github.io/)
*   [Domande frequenti su HTTP/2](https://http2.github.io/faq/)
*   [Informazioni su HTTP/2 di Akamai](https://http2.akamai.com/)

toolearn sulle funzionalità disponibili della rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).
