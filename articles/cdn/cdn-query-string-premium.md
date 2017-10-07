---
title: comportamento di memorizzazione nella cache della rete CDN di Azure con le stringhe di query - Premium aaaControl | Documenti Microsoft
description: Stringa di query della rete CDN Azure controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe di memorizzazione nella cache.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query: Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Rete CDN Premium di Azure fornita da Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Panoramica
La memorizzazione nella cache i controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe stringa di query.

> [!IMPORTANT]
> prodotti Standard e Premium CDN Hello forniscono hello stessa funzionalità di memorizzazione nella cache di stringhe di query, ma l'interfaccia utente di hello diversa.  Questo documento descrive l'interfaccia di hello per **Premium rete CDN di Azure da Verizon**.  Per informazioni sulla memorizzazione nella cache di stringhe di query con la **rete CDN Standard di Azure fornita da Akamai** e la **rete CDN Standard di Azure fornita da Verizon**, vedere l'articolo [Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query](cdn-query-string.md).
> 
> 

Sono disponibili tre modalità:

* **standard cache**: si tratta di modalità predefinita di hello.  nodo perimetrale della rete CDN di Hello passa la stringa di query hello dall'origine toohello richiedente di hello nella prima richiesta hello e asset hello cache.  Tutte le richieste successive per tale asset resi disponibili dal nodo edge hello ignorerà la stringa di query hello fino alla scadenza di asset memorizzati nella cache di hello.
* **no-cache**: In questa modalità, le richieste con stringhe di query non vengono memorizzate nel nodo perimetrale della rete CDN di hello.  nodo edge Hello recupera asset hello direttamente dall'origine hello e passa il richiedente toohello con ogni richiesta.
* **unique-cache**: questa modalità considera ogni richiesta con una stringa di query come un asset univoco con la propria memorizzazione nella cache.  Ad esempio, hello risposta dall'origine hello per una richiesta di *foo.ashx?q=bar* vengono memorizzati nella cache al nodo del bordo hello e restituiti per le successive cache con la stessa stringa di query.  Una richiesta per *foo.ashx?q=somethingelse* verrà memorizzata nella cache come una risorsa con il proprio tempo toolive separata.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Modifica delle impostazioni di memorizzazione nella cache della stringa di query per i profili premium della rete CDN
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.  Fare clic su **Memorizzazione nella cache della stringa di Query**.
   
    Vengono visualizzate le opzioni di memorizzazione nella cache della stringa di query.
   
    ![Opzioni della memorizzazione nella cache della stringa di query della rete CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. Dopo aver effettuato la selezione, fare clic su hello **aggiornamento** pulsante.

> [!IMPORTANT]
> modifiche alle impostazioni di Hello potrebbe non essere immediatamente visibile, come il tempo per hello registrazione toopropagate tramite hello CDN.  Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.
> 
> 

