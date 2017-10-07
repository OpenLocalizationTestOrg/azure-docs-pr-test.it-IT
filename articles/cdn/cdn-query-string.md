---
title: comportamento di memorizzazione nella cache della rete CDN di Azure con le stringhe di query aaaControl | Documenti Microsoft
description: Stringa di query della rete CDN Azure controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe di memorizzazione nella cache.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Rete CDN Premium di Azure fornita da Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Panoramica
La memorizzazione nella cache i controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe stringa di query.

> [!IMPORTANT]
> prodotti Standard e Premium CDN Hello forniscono hello stessa funzionalità di memorizzazione nella cache di stringhe di query, ma l'interfaccia utente di hello diversa.  Questo documento descrive l'interfaccia di hello per **Azure CDN Standard da Akamai** e **Azure CDN Standard da Verizon**.  Per informazioni sulla memorizzazione nella cache di stringhe di query con la **rete CDN Premium di Azure fornita da Verizon**, vedere l'articolo [Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query - Premium](cdn-query-string-premium.md).
> 
> 

Sono disponibili tre modalità:

* **Ignorare le stringhe di query**: si tratta di modalità predefinita di hello.  nodo perimetrale della rete CDN di Hello passa la stringa di query hello dall'origine toohello richiedente di hello nella prima richiesta hello e asset hello cache.  Tutte le richieste successive per tale asset resi disponibili dal nodo edge hello ignorerà la stringa di query hello fino alla scadenza di asset memorizzati nella cache di hello.
* **Ignorare la memorizzazione nella cache per URL con stringhe di query**: In questa modalità, le richieste con stringhe di query non vengono memorizzate nel nodo perimetrale della rete CDN di hello.  nodo edge Hello recupera asset hello direttamente dall'origine hello e passa il richiedente toohello con ogni richiesta.
* **Memorizzare nella cache tutti gli URL univoci**: questa modalità considera ogni richiesta con una stringa di query come un asset univoco con una propria memorizzazione nella cache.  Ad esempio, hello risposta dall'origine hello per una richiesta di *foo.ashx?q=bar* vengono memorizzati nella cache al nodo del bordo hello e restituiti per le successive cache con la stessa stringa di query.  Una richiesta per *foo.ashx?q=somethingelse* verrà memorizzata nella cache come una risorsa con il proprio tempo toolive separata.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Modifica delle impostazioni di memorizzazione nella cache della stringa di query per i profili standard della rete CDN
1. Dal Pannello di profilo CDN hello, fare clic su endpoint rete CDN hello desiderato toomanage.
   
    ![Endpoint del pannello del profilo di rete CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    verrà visualizzata la finestra di blade endpoint rete CDN di Hello.
2. Fare clic su hello **configura** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    Apre il pannello di configurazione della rete CDN Hello.
3. Selezionare un'impostazione da hello **stringa di Query, il comportamento di memorizzazione nella cache** elenco a discesa.
   
    ![Opzioni della memorizzazione nella cache della stringa di query della rete CDN](./media/cdn-query-string/cdn-query-string.png)
4. Dopo aver effettuato la selezione, fare clic su hello **salvare** pulsante.

> [!IMPORTANT]
> modifiche alle impostazioni di Hello potrebbe non essere immediatamente visibile, come il tempo per hello registrazione toopropagate tramite hello CDN.  Per <b>Rete CDN di Azure da Akamai</b> la propagazione in genere viene completata entro un minuto.  Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.
> 
> 

