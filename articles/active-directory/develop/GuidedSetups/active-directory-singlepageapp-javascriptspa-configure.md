---
title: 'aaaAzure AD v2 JS SPA interattiva del programma di installazione: configurare | Documenti Microsoft'
description: Come le applicazioni SPA di Javascript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Registrare l'applicazione

Esistono più modi toocreate un'applicazione, selezionare uno di essi:

### <a name="option-1-register-your-application-express-mode"></a>Opzione 1: Registrare l'applicazione (modalità Rapida)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:

1.  Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Assicurarsi che opzione hello *impostazione guidata* è selezionata
4.  Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice

### <a name="option-2-register-your-application-advanced-mode"></a>Opzione 2: Registrare l'applicazione (modalità avanzata)

1. Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione
2. Immettere un nome per l'applicazione e l'indirizzo di posta elettronica 
3. Assicurarsi che opzione hello *impostazione guidata* è deselezionata
4.  Fare clic su `Add Platform`, quindi selezionare `Web`
5. Aggiungere hello `Redirect URL` che corrispondono l'URL dell'applicazione toohello basato sul server web. Vedere sezioni hello per le istruzioni su come tooset / ottenere l'URL di reindirizzamento hello in Visual Studio e Python.
6. Fare clic su *Save*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Istruzioni di Visual Studio per ottenere l'URL di reindirizzamento
> Seguire hello istruzioni tooobtain l'URL di reindirizzamento:
> 1.    In *Esplora*, selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzato una finestra delle proprietà, premere `F4`)
> 2.    Copiare il valore di hello da `URL` toohello Appunti:<br/> ![Proprietà del progetto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Passa indietro toohello *portale di registrazione applicazione* e incollare il valore di hello come un `Redirect URL` e fare clic su "Salva"

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configurazione dell'URL di reindirizzamento per Python
> Per Python, è possibile impostare una porta del server web hello tramite riga di comando. Il programma di installazione guidata utilizza hello la porta 8080 per riferimento, ma è gratuita toouse qualsiasi porta disponibile. In ogni caso, attenersi alle istruzioni di hello seguenti tooset un URL di reindirizzamento nelle informazioni di registrazione applicazione hello:<br/>
> - Passa indietro toohello *portale di registrazione applicazione* e impostare `http://localhost:8080/` come un `Redirect URL`, oppure utilizzare `http://localhost:[port]/` se si utilizza una porta TCP personalizzata (dove *[porta]* è la porta TCP personalizzata hello numero) e fare clic su "Salva"


#### <a name="configure-your-javascript-spa"></a>Configurare JavaScript SPA

1.  Creare un file denominato `msalconfig.js` contenente le informazioni di registrazione applicazione hello. Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), mouse e scegliere: `Add`  >  `New Item`  >  `JavaScript File`. Assegnare il nome `msalconfig.js`
2.  Aggiungere i seguenti tooyour codice hello `msalconfig.js` file:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Sostituire <code>Enter_the_Application_Id_here</code> con hello Id applicazione appena registrato
</li>
</ol>
