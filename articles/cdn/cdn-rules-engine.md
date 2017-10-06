---
title: il comportamento di aaaOverride HTTP mediante motore regole di hello rete CDN di Azure | Documenti Microsoft
description: motore regole di Hello consente toocustomize come richieste HTTP vengono gestite dalla rete CDN di Azure, ad esempio il blocco di recapito hello di determinati tipi di contenuto, definire un criterio di memorizzazione nella cache e modificare le intestazioni HTTP.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Override del comportamento HTTP utilizzando motore regole di hello rete CDN di Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Panoramica
il motore regole di Hello consente toocustomize come vengono gestite le richieste HTTP, ad esempio il blocco di recapito hello di determinati tipi di contenuto, definizione di criteri di memorizzazione nella cache e la modifica delle intestazioni HTTP.  In questa esercitazione verrà illustrato la creazione di una regola che verrà modificato il comportamento delle risorse di rete CDN di memorizzazione nella cache di hello.  È inoltre contenuto video disponibili in hello "[vedere anche](#see-also)" sezione.

   > [!TIP] 
   > Per un riferimento toohello in modo dettagliato, vedere [riferimento motore regole](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Esercitazione
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Fare clic su hello **HTTP grandi** scheda, seguita da **motore regole di business**.
   
    Vengono visualizzate le opzioni per una nuova regola.
   
    ![Opzioni delle regole della nuova rete CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > ordine di Hello in cui sono elencate più regole influisce sulla modalità di gestione. Una regola successive può eseguire l'override di azioni hello specificate da una regola precedente.
   > 
   > 
3. Immettere un nome in hello **nome / descrizione** casella di testo.
4. Identificare il tipo di hello di hello regola verrà applicata alle richieste.  Per impostazione predefinita, hello **sempre** condizione di corrispondenza è selezionata.  Si utilizzerà **Sempre** per questa esercitazione, quindi lasciarla selezionata.
   
   ![Condizione di corrispondenza della rete CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Esistono molti tipi di corrispondenza condizioni disponibili nell'elenco a discesa hello.  Facendo clic su toohello icona informativa blu hello sinistra della condizione di corrispondenza hello illustrerà condizione hello attualmente selezionato in modo dettagliato.
   > 
   >  Per hello l'elenco completo delle espressioni condizionali in modo dettagliato, vedere [espressioni condizionali di motore regole](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Per hello l'elenco completo delle condizioni di corrispondenza in modo dettagliato, vedere [le condizioni corrispondono del motore regole](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Fare clic su hello  **+**  accanto troppo**funzionalità** tooadd una nuova funzionalità.  Nell'elenco a discesa hello hello sinistra, selezionare **Force interno Max-Age**.  Nella casella di testo hello che viene visualizzata, immettere **300**.  Lasciare hello rimanenti valori predefiniti.
   
   ![Funzionalità della rete CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Come con le condizioni di corrispondenza, fare clic su toohello icona informativa blu hello a sinistra della hello nuove funzionalità saranno visualizzati i dettagli su questa funzionalità.  Nel caso di hello di **Force interno Max-Age**, è stato eseguito l'override dell'asset hello **Cache-Control** e **Expires** toocontrol intestazioni quando il nodo del bordo della rete CDN di hello aggiornerà hello Asset dall'origine hello.  Esempio di 300 secondi significa nodo del bordo di hello CDN verrà memorizzati nella cache di asset hello per 5 minuti prima di aggiornare asset hello dall'origine.
   > 
   > Per hello l'elenco completo di funzionalità in modo dettagliato, vedere [dettagli delle funzionalità del motore regole](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Fare clic su hello **Aggiungi** nuova regola di pulsante toosave hello.  nuova regola Hello ora è in attesa di approvazione. Quando è stata approvata, hello stato cambia da **XML in sospeso** troppo**XML Active**.
   
   > [!IMPORTANT]
   > Le modifiche delle regole potrebbero richiedere too90 minuti toopropagate tramite hello CDN.
   > 
   > 

## <a name="see-also"></a>Vedere anche
* [Panoramica della rete CDN di Azure](cdn-overview.md)
* [Informazioni di riferimento sul motore regole](cdn-rules-engine-reference.md)
* [Condizioni di corrispondenza del motore regole](cdn-rules-engine-reference-match-conditions.md)
* [Espressioni condizionali del motore regole](cdn-rules-engine-reference-conditional-expressions.md)
* [Funzionalità del motore regole](cdn-rules-engine-reference-features.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
* [Vedere il video relativo alle nuove potenti funzionalità Premium della rete CDN di Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)