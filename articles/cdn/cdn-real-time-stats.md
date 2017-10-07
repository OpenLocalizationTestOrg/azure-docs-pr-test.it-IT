---
title: fase aaaReal statistiche nella rete CDN di Azure | Documenti Microsoft
description: Statistiche in tempo reale fornisce in tempo reale dati sulle prestazioni di hello della rete CDN di Azure per il recapito di contenuto tooyour client.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Statistiche in tempo reale nella rete CDN di Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overview
Questo documento illustra le statistiche in tempo reale nella rete CDN di Microsoft Azure.  Questa funzionalità fornisce i dati in tempo reale, ad esempio larghezza di banda, gli stati di cache e connessioni simultanee tooyour CDN profilo per il recapito di contenuto tooyour client. In questo modo, il monitoraggio continuo dell'integrità di hello del servizio in qualsiasi momento, inclusi gli eventi di pubblicazione.

sono disponibile i seguenti grafici Hello:

* [Larghezza di banda](#bandwidth)
* [Codici di stato](#status-codes)
* [Stati della cache](#cache-statuses)
* [Connessioni](#connections)

## <a name="accessing-real-time-stats"></a>Accesso alle statistiche in tempo reale
1. In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
3. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **statistiche in tempo reale** riquadro a comparsa.  Fare clic su **Oggetto di grandi dimensioni HTTP**.
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    vengono visualizzati i grafici di Hello statistiche in tempo reale.

Ognuno dei grafici hello Visualizza statistiche in tempo reale per l'intervallo di tempo selezionato hello, avvio durante il caricamento pagina hello.  grafici di Hello aggiornati automaticamente ogni pochi secondi.  Hello **aggiornare grafico** pulsante, se presente, verrà cancellato grafico hello, dopo il quale verranno visualizzate solo dati hello selezionato.

## <a name="bandwidth"></a>Larghezza di banda
![Grafico Larghezza di banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

Hello **della larghezza di banda** grafico consente di visualizzare la quantità hello di larghezza di banda utilizzata per la piattaforma corrente hello tramite l'intervallo di tempo selezionato hello. Hello ombreggiata parte grafico hello indica l'utilizzo della larghezza di banda. quantità esatta di Hello di larghezza di banda attualmente in uso viene visualizzato sotto un grafico a linee hello.

## <a name="status-codes"></a>Codici di stato
![Grafico Codici di stato](./media/cdn-real-time-stats/cdn-status-codes.png)

Hello **codici di stato** grafico indica la frequenza con cui si verificano alcuni codici di risposta HTTP su intervallo di tempo hello selezionato.

> [!TIP]
> Per una descrizione di ogni opzione relativa ai codici di stato HTTP, vedere [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codici di stato HTTP della rete CDN di Azure).
> 
> 

Direttamente sopra il grafico di hello viene visualizzato un elenco di codici di stato HTTP. Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee hello e numero corrente di hello di occorrenze al secondo per il codice di stato. Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico hello. Tuttavia, è possibile scegliere tooonly i codici di stato hello monitor che hanno un significato speciale per la configurazione della rete CDN. toodo, controllare i codici di stato hello desiderato e deselezionare tutte le altre opzioni, quindi fare clic su **aggiornare grafico**. 

È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.  Legenda hello direttamente sotto il grafico di hello, selezionare il codice di stato hello desiderato toohide. codice di stato Hello verrà nascoste dal grafico hello immediatamente. Fare nuovamente clic su quel codice di stato causerà toobe tale opzione visualizzato di nuovo.

## <a name="cache-statuses"></a>Stati della cache
![Grafico Stati della cache](./media/cdn-real-time-stats/cdn-cache-status.png)

Hello **Cache stati** grafico indica la frequenza con cui si verificano determinati tipi di stato della cache su intervallo di tempo selezionato hello. 

> [!TIP]
> Per una descrizione di ogni opzione relativa agli stati della cache, vedere [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codici di stato della cache della rete CDN di Azure).
> 
> 

Direttamente sopra il grafico di hello viene visualizzato un elenco dei codici di stato della cache. Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee hello e numero corrente di hello di occorrenze al secondo per il codice di stato. Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico hello. Tuttavia, è possibile scegliere tooonly i codici di stato hello monitor che hanno un significato speciale per la configurazione della rete CDN. toodo, controllare i codici di stato hello desiderato e deselezionare tutte le altre opzioni, quindi fare clic su **aggiornare grafico**. 

È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.  Legenda hello direttamente sotto il grafico di hello, selezionare il codice di stato hello desiderato toohide. codice di stato Hello verrà nascoste dal grafico hello immediatamente. Fare nuovamente clic su quel codice di stato causerà toobe tale opzione visualizzato di nuovo.

## <a name="connections"></a>Connessioni
![Grafico Connessioni](./media/cdn-real-time-stats/cdn-connections.png)

Questo grafico indica il numero di connessioni sono state stabilite tooyour edge server. Ogni richiesta per un asset che passa attraverso la rete CDN costituisce una connessione.

## <a name="next-steps"></a>Passaggi successivi
* Per impostare la ricezione di notifiche, vedere [Avvisi in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-alerts.md)
* Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)
* Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)

