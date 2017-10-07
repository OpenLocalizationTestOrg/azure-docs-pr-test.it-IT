---
title: aaaAzure AD v2 JS SPA impostazione guidata - configurare ARP () | Documenti Microsoft
description: Illustra in che modo le applicazioni SPA di JavaScript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2 (ARP)
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Aggiungere tooyour informazioni di registrazione dell'applicazione hello App

In questo passaggio, è necessario l'URL di reindirizzamento hello tooconfigure delle informazioni di registrazione dell'applicazione e quindi aggiungere un'applicazione hello Id applicazione tooyour SPA JavaScript.

### <a name="configure-redirect-url"></a>Configurare l'URL di reindirizzamento

Configurare hello `Redirect URL` campo sopra con hello URL della pagina index basato sul server web, quindi fare clic su *aggiornamento*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Istruzioni di Visual Studio per ottenere l'URL di reindirizzamento
> tooobtain l'URL di reindirizzamento, seguire le istruzioni di hello riportato di seguito:
> 1.    In *Esplora*, selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzato una finestra delle proprietà, premere `F4`)
> 2.    Copiare il valore di hello da `URL` toohello Appunti:<br/> ![Proprietà del progetto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Incollare il valore di hello come un `Redirect URL` nella parte superiore di hello di questa pagina, quindi fare clic su`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configurazione dell'URL di reindirizzamento per Python
> Per Python, è possibile impostare una porta del server web hello tramite riga di comando. Il programma di installazione guidata utilizza hello la porta 8080 per riferimento, ma è gratuita toouse qualsiasi porta disponibile. In ogni caso, attenersi alle istruzioni di hello seguenti tooset un URL di reindirizzamento nelle informazioni di registrazione applicazione hello:<br/>
> Impostare `http://localhost:8080/` come un `Redirect URL` hello inizio di questa pagina, o utilizzare `http://localhost:[port]/` se si utilizza una porta TCP personalizzata (dove *[porta]* numero di porta TCP personalizzata hello) e quindi fare clic su 'Aggiorna'

### <a name="configure-your-javascript-spa-application"></a>Configurare l'applicazione JavaScript SPA

1.  Creare un file denominato `msalconfig.js` contenente le informazioni di registrazione applicazione hello. Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), mouse e scegliere: `Add`  >  `New Item`  >  `JavaScript File`. Assegnare il nome `msalconfig.js`
2.  Aggiungere i seguenti tooyour codice hello `msalconfig.js` file:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
