---
title: aaaPurge un endpoint rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toopurge tutti memorizzato nella cache contenuto da un endpoint rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Ripulire un endpoint della rete CDN di Azure
## <a name="overview"></a>Panoramica
Nodi di bordo della rete CDN Azure vengono memorizzati nella cache di asset fino alla scadenza time-to-live (TTL) dell'asset hello.  Alla scadenza durata (TTL) dell'asset hello, quando un client richiede asset hello dal nodo edge hello, nodo edge hello recupererà una nuova copia aggiornata della richiesta client di hello asset tooserve hello e archiviare l'aggiornamento della cache di hello.

Hello best practice toomake che gli utenti ottengono sempre una copia più recente di hello delle risorse è tooversion le risorse per ogni aggiornamento e pubblicano come nuovi URL.  Rete CDN recupera immediatamente nuove risorse di hello per le richieste client successive hello.  In alcuni casi è preferibile toopurge memorizzati nella cache il contenuto di tutti i nodi del bordo e forzarne tutte le risorse aggiornate nuovo tooretrieve.  Potrebbe trattarsi di scadenza dell'applicazione web di tooupdates tooyour o tooquickly aggiornamento asset che contenga informazioni non corrette.

> [!TIP]
> Si noti che solo eliminazione Cancella hello memorizzati nella cache contenuto nel server perimetrale della rete CDN di hello.  Tutte le cache downstream, ad esempio i server proxy e cache locale del browser, possono comunque contenere una copia memorizzata nella cache del file hello.  È importante tooremember questo quando si imposta un file time-to-live.  È possibile forzare una versione più recente di hello toorequest client downstream del file, assegnargli un nome univoco che ogni volta che si aggiornarlo o sfruttando [la memorizzazione nella cache di stringa di query](cdn-query-string.md).  
> 
> 

Questa esercitazione illustra l'eliminazione dagli asset di tutti i nodi periodici di un endpoint.

## <a name="walkthrough"></a>Procedura dettagliata
1. In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN toohello contenente hello endpoint desiderato toopurge.
2. Dal Pannello di profilo CDN hello, fare clic sul pulsante di eliminazione hello di seguito.
   
    ![Pannello del profilo di rete CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    verrà visualizzata la finestra di blade Purge Hello.
   
    ![Pannello di eliminazione della rete CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. In hello ripulire pannello, selezionare l'indirizzo del servizio hello desiderato toopurge dall'elenco a discesa URL hello.
   
    ![Maschera di eliminazione](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > È inoltre possibile ottenere toohello eliminazione pannello facendo hello **ripulire** pulsante sul pannello endpoint rete CDN di hello.  In tal caso, hello **URL** campo sarà già popolato con l'indirizzo del servizio hello di quell'endpoint specifico.
   > 
   > 
4. Selezionare le risorse desiderate toopurge da hello nodi periferici.  Se si desiderano tooclear tutte le risorse, fare clic su hello **Ripulisci** casella di controllo.  In caso contrario, tipo hello percorso di ogni asset da cui toopurge in hello **percorso** casella di testo. Formati di seguito sono supportate nel percorso di hello.
    1. **Eliminazione di URL singolo**: Elimina una singola risorsa specificando l'URL completo di hello, con o senza estensione file hello, ad esempio,`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Wildcard purge**: (Eliminazione dei caratteri jolly) l'asterisco (\*) può essere usato come carattere jolly. Eliminare tutte le cartelle, sottocartelle e file in un endpoint con `/*` hello percorso oppure eliminare tutte le sottocartelle e file in una cartella specifica specificando cartella hello seguita da `/*`, ad esempio,`/pictures/*`.  Si noti che l'eliminazione dei caratteri jolly non è attualmente supportata dalla rete CDN di Azure fornita da Akamai. 
    3. **Eliminazione di dominio radice**: radice hello di eliminazione dell'endpoint hello con "/" nel percorso di hello.
   
   > [!TIP]
   > I percorsi devono essere specificati per l'eliminazione e deve essere un URL relativo che rientrano seguente hello [espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx). Le funzioni **Elimina tutti** e **Wildcard purge** (Eliminazione dei caratteri jolly) non sono attualmente supportate con la **rete CDN di Azure fornita da Akamai**.
   > > Single URL purge (Eliminazione di un URL singolo) `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Stringa di query `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Wildcard purge (Eliminazione dei caratteri jolly) `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Ulteriori **percorso** nelle caselle di testo verrà visualizzato dopo l'immissione di testo tooallow si toobuild un elenco di più risorse.  È possibile eliminare l'asset dall'elenco hello facendo clic sul pulsante con puntini di sospensione (…) hello.
   > 
5. Fare clic su hello **ripulire** pulsante.
   
    ![Pulsante di eliminazione](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Eliminare le richieste richiedere circa 2-3 minuti tooprocess con **rete CDN di Azure da Verizon** (Standard e Premium) e circa 7 minuti con **rete CDN di Azure da Akamai**.  La rete CDN di Azure ha un limite di 50 richieste di eliminazione simultanee in qualsiasi momento. 
> 
> 

## <a name="see-also"></a>Vedere anche
* [Precaricamento di risorse in un endpoint della rete CDN di Azure](cdn-preload-endpoint.md)
* [Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint](https://msdn.microsoft.com/library/mt634451.aspx)

