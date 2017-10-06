---
title: gruppo di connettori lavoro aaaNo trovato per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Risolvere i problemi riscontrati quando è presente alcun lavoro connettore in un gruppo di connettori per l'applicazione con hello Proxy dell'applicazione Azure Active"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Nessun gruppo di connettori funzionante trovato per un'applicazione Proxy di applicazione

La Guida di questo articolo è tooresolve hello comuni problemi quando non vi è un connettore per un'applicazione Proxy di applicazione integrata con Azure Active Directory.

## <a name="overview-of-steps"></a>Panoramica dei passaggi
Se è presente alcun lavoro connettore in un gruppo di connettori per l'applicazione, esistono alcuni problemi di hello tooresolve modi:

-   Se non si dispone di alcun connettori nel gruppo di hello, è possibile:

    -   Scaricare un nuovo connettore nel server locale destra hello e assegnare a questo gruppo toothis

    -   Spostare un connettore attivo nel gruppo di hello

-   Se non si dispone di alcun connettore attivo nel gruppo di hello, è possibile:

    -   Identificare il motivo di hello che il connettore è inattivo e risolvere

    -   Spostare un connettore attivo nel gruppo di hello

tooknow quale di questi problemi hello, aprire il menu di "Proxy dell'applicazione" hello nell'applicazione, confrontando il messaggio di avviso gruppo di connettori hello. Può specificare entrambi i gruppi che hello è necessario almeno un connettore (si dispone di nessuna gruppo hello) o che non dispone di alcun connettore attivo (anche se probabilmente si dispone di connettori inattivi).

   ![Selezione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Per informazioni dettagliate su ognuna di queste opzioni, sezione hello corrispondente riportato di seguito. Ognuna di queste si presuppone che si inizi dalla pagina di gestione di hello connettore. Se si sta esaminando i messaggio di errore hello sopra riportato, è possibile passare toothis pagina facendo clic sul messaggio di avviso hello. In caso contrario disponibile selezionando troppo**Azure Active Directory**, fare clic su **applicazioni aziendali**, quindi **Proxy dell'applicazione.**

   ![Gestione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Scaricare un nuovo connettore

toodownload un nuovo connettore, utilizzare pulsante "Scarica connettore" hello nella parte superiore di hello della pagina hello.

esigenze del connettore hello nota toobe installato in un computer con l'applicazione di back-end toohello of di visibilità diretto e si trova in genere hello applicazione hello nello stesso server. Dopo aver scaricato, hello connettore dovrebbe essere visualizzato in questo menu. Fare clic su hello connettore e utilizzare hello "Gruppo di connettori" elenco a discesa toomake che appartiene a gruppo corretto toohello. Salvare modifiche hello.

   ![Scaricare il connettore hello da hello portale di Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Spostare un connettore attivo

Se si dispone di un connettore attivo che deve appartenere toohello gruppo e che dispone di visibilità toohello l'applicazione back-end di destinazione, è possibile spostare hello connettore nel gruppo hello assegnato. toodo questa operazione, scegliere hello connettore. Nel campo "Gruppo di connettori" hello, utilizzare il gruppo corretto hello tooselect elenco a discesa hello e fare clic su Salva.

## <a name="resolve-an-inactive-connector"></a>Risolvere un connettore inattivo

Se hello solo connettori hello del gruppo sono inattivi, sono probabilmente su un computer che non sono stati sbloccati tutte le porte necessarie hello.

Vedere porte hello documento di risoluzione dei problemi per informazioni dettagliate su questo problema in corso.

## <a name="next-steps"></a>Passaggi successivi
[Comprendere i connettori del proxy applicazione Azure AD](application-proxy-understand-connectors.md)


