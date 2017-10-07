---
title: le applicazioni client native aaaPublish - Azure AD | Documenti Microsoft
description: Descrive come toocommunicate di App client nativa tooenable con Azure Active Directory Application Proxy Connector tooprovide accesso remoto sicuro tooyour locale delle app.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Come toointeract di App client nativa tooenable con proxy applicazioni

Nelle applicazioni tooweb aggiunta, il Proxy di applicazione Azure Active Directory può essere anche le applicazioni client native toopublish utilizzato. Le app client native si differenziano dalle app Web perché vengono installate su un dispositivo, mentre le app Web sono accessibili tramite un browser. 

Il proxy di applicazione supporta le app client native accettando token rilasciati da Azure AD e inviati in intestazioni HTTP Authorize standard.

![Relazione tra utenti finali, Azure Active Directory e applicazioni pubblicate](./media/active-directory-application-proxy-native-client/richclientflow.png)

Usare Azure AD Authentication Library, che si occupa di autenticazione e supporta molti ambienti client, le applicazioni native toopublish hello. Proxy dell'applicazione si integra con hello [uno scenario di applicazione nativa tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). In questo articolo illustra hello quattro passaggi toopublish un'applicazione nativa con Proxy dell'applicazione e hello Azure AD Authentication Library. 

## <a name="step-1-publish-your-application"></a>Passaggio 1: Pubblicare l'applicazione
Pubblicare l'applicazione proxy come qualsiasi altra applicazione e assegnare gli utenti tooaccess l'applicazione. Per altre informazioni, vedere [Pubblicare applicazioni mediante il proxy di applicazione](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Passaggio 2: Configurare l'applicazione
Configurare l'applicazione nativa come indicato di seguito:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare troppo**Azure Active Directory** > **registrazioni di App**.
3. Selezionare **Registrazione nuova applicazione**.
4. Specificare un nome per l'applicazione, seleziona **nativo** come tipo di applicazione, hello e fornire hello URI di reindirizzamento per l'applicazione. 

   ![Creare una nuova registrazione di app](./media/active-directory-application-proxy-native-client/create.png)
5. Selezionare **Crea**.

Per informazioni più dettagliate sulla creazione di una nuova registrazione di app, vedere [Integrazione di applicazioni con Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Passaggio 3: Applicazioni concedere accesso tooother
Abilitare hello applicazione nativa toobe esposti tooother applicazioni nella directory:

1. Ancora in **registrazioni di App**, selezionare hello nuova applicazione nativa appena creato.
2. Selezionare **Autorizzazioni necessarie**.
3. Selezionare **Aggiungi**.
4. Innanzitutto aprire hello **selezionare un'API**.
5. Usare hello ricerca barra toofind hello Proxy di applicazione app pubblicata nella prima sezione hello. Scegliere tale app e quindi fare clic su **Seleziona**. 

   ![Cercare hello proxy app](./media/active-directory-application-proxy-native-client/select_api.png)
6. Aprire hello secondo passaggio, ovvero **selezionare autorizzazioni**.
7. Utilizzare hello casella di controllo toogrant applicazione applicazione nativa access tooyour proxy, quindi fare clic su **selezionare**.

   ![Concedere accesso tooproxy app](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Selezionare **Operazione completata**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Passaggio 4: Modificare hello Active Directory Authentication Library
Modificare il codice di applicazione nativa hello in contesto di autenticazione hello di hello tooinclude di Active Directory Authentication Library (ADAL) hello seguente testo:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

le variabili di Hello nel codice di esempio hello devono essere sostituite come indicato di seguito:

* **ID tenant** è reperibile nel portale di Azure hello. Passare troppo**Azure Active Directory** > **proprietà** e hello copia ID di Directory. 
* **URL esterno** URL front-end di hello immesso nel Proxy applicazione hello. toofind questo valore, passare toohello **proxy dell'applicazione** sezione hello proxy app.
* **ID dell'app** di hello app nativa è reperibile in hello **proprietà** pagina dell'applicazione nativa hello.
* **URI di reindirizzamento dell'app nativa hello** possono trovarsi in hello **Redirect URIs** pagina dell'applicazione nativa hello.


## <a name="see-also"></a>Vedere anche

Per ulteriori informazioni sul flusso di hello applicazione nativa, vedere [tooweb applicazione nativa API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)
