---
title: chiamare aaaDeploy e l'autenticazione web API e le API REST per le app di logica di Azure | Documenti Microsoft
description: Distribuire, autenticare e chiamare API Web e API REST nei flussi di lavoro per le integrazioni di sistema con le app per la logica di Azure
keywords: API Web, API REST, connettori, flussi di lavoro, integrazioni di sistema, autenticazione
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Distribuire, chiamare e autenticare le API personalizzate come connettori per le app per la logica

Dopo aver [creare API personalizzate](./logic-apps-create-api-app.md) toouse azioni o i trigger nella logica che forniscono i flussi di lavoro di applicazioni, è necessario distribuire le API prima di poter chiamare. Sebbene sia possibile chiamare qualsiasi API da un'app, la logica per un'esperienza ottimale di hello, aggiungere [metadati Swagger](http://swagger.io/specification/) che descrive le operazioni dell'API e parametri. Il file Swagger consente all'API di funzionare meglio e di integrarsi più facilmente con le app per la logica.

È possibile distribuire le API come [le app web](../app-service-web/app-service-web-overview.md), ma è consigliabile distribuire le API come [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md), che può semplificare il lavoro quando si compila, host e utilizzare le API nel cloud hello e in locale. Non si dispone toochange qualsiasi codice nelle API--è sufficiente distribuire l'app per le API tooan di codice. È possibile ospitare le API in [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) offerta che fornisce uno dei modi di hello migliori, più semplici e più scalabili per l'API di hosting.

tooauthenticate chiamate da logica App tooyour API, è possibile impostare Azure Active Directory in hello portale di Azure in modo non si dispone di codice tooupdate. Oppure, è possibile richiedere e applicare l'autenticazione attraverso il codice dell'API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Distribuire l'API come app Web o app per le API

Prima di poter chiamare l'API personalizzata da un'app di logica, è possibile distribuire l'API come un'app web o l'API app tooAzure servizio App. Inoltre, toomake documento Swagger leggibile da hello logica progettazione applicazione, impostare le proprietà di definizione API hello e attivare [risorse multiorigine (CORS) di condivisione](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) per le app web o API.

1. Nel portale di Azure hello, selezionare le app web o API.

2. Nel pannello hello visualizzata nell'area **API**, scegliere **di definizione dell'API**. Set hello **percorso definizione API** toohello URL per il file swagger.

   URL hello in genere, viene visualizzato nel formato seguente:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![File di collegamento tooSwagger dell'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Scegliere **CORS** nell'area **API**. Impostare il criterio CORS hello per **le origini consentite** troppo**'*'** (Consenti tutti).

   Questa impostazione consente le richieste da Progettazione app per la logica.

   ![Consentire richieste dall'API di progettazione applicazione logica tooyour personalizzato](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Per altre informazioni, vedere questi articoli:

* [Aggiungere metadati Swagger per le API Web ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Distribuzione di ASP.NET web API tooAzure servizio App](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Chiamare l'API personalizzata dai flussi di lavoro delle app per la logica

Dopo aver impostato le proprietà di definizione API hello e CORS, trigger e le azioni dell'API personalizzata dovrebbero diventare disponibile per tooinclude nel flusso di lavoro logica app. 

*  tooview hello siti Web con l'URL di Swagger, è possibile esplorare i siti Web di sottoscrizione nella logica di progettazione di App hello.

*  azioni disponibili tooview e degli input che punta a un documento di Swagger, utilizzare hello [HTTP + Swagger azione](../connectors/connectors-native-http-swagger.md).

*  toocall qualsiasi API, incluse le API che non hanno o esporre un documento di Swagger, è sempre possibile creare una richiesta con hello [azione HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Autenticare le chiamate API personalizzata di tooyour

È possibile proteggere le chiamate API personalizzata di tooyour nei modi seguenti:

* [Nessuna modifica di codice](#no-code): proteggere le API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) tramite hello portale di Azure, pertanto non disporre di tooupdate codice oppure ridistribuire l'API.

  > [!NOTE]
  > Per impostazione predefinita, l'autenticazione di Azure AD hello che attivare in hello portale di Azure non fornisce un'autorizzazione. Ad esempio, questa autenticazione Blocca toojust l'API, un tenant specifico, non tooa utente o specifico dell'applicazione. 

* [Aggiornare il codice dell'API](#update-code): proteggere l'API applicando [l'autenticazione del certificato](#certificate), [l'autenticazione di base](#basic) o [autenticazione di Azure AD](#azure-ad-code) attraverso il codice.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Autenticare le chiamate API di tooyour senza modificare il codice

Ecco i passaggi generali hello per questo metodo:

1. Creare due [identità di applicazione di Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md), una per l'app per la logica e una per l'app Web (o l'app per le API).

2. tooauthenticate tooyour di chiamate API, utilizzare le credenziali di hello (ID client e segreto) per hello [dell'entità servizio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associato hello identità dell'applicazione Azure AD per l'app logica.

3. Includere un'applicazione hello ID nella definizione dell'app logica.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Parte 1: Creare un'identità di applicazione di Azure AD per l'app per la logica

Logica app Usa questa tooauthenticate identità di applicazione di Azure AD con Azure AD. È solo una volta per la directory tooset backup questa identità. Ad esempio, è possibile scegliere toouse hello identità stesso per tutte le app di logica, anche se è possibile creare le identità univoche per ogni app logica. È possibile impostare queste identità nel portale di Azure hello [portale di Azure classico](#app-identity-logic-classic), oppure utilizzare [PowerShell](#powershell).

**Creare l'identità dell'applicazione hello per le app per la logica in hello portale di Azure**

1. In hello [portale di Azure](https://portal.azure.com "https://portal.azure.com"), scegliere **Azure Active Directory**. 

2. Confermare che si è in hello stessa directory le app web o API.

   > [!TIP]
   > Directory tooswitch, scegliere il profilo e selezionare un'altra directory. In alternativa, scegliere **Panoramica** > **Cambia directory**.

3. Menu directory hello in **Gestisci**, scegliere **registrazioni di App** > **nuova registrazione applicazione**.

   > [!TIP]
   > Per impostazione predefinita, elenco di registrazioni app hello Mostra tutte le registrazioni di app nella directory. Selezionare solo le registrazioni di app, casella di ricerca toohello Avanti tooview **le mie app**. 

   ![Creare una nuova registrazione di app](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Assegnare un nome di identità applicazione, lasciare **tipo di applicazione** impostato troppo**app Web / API**, fornire un univoco stringa formattata come un dominio per **Sign-on URL**e scegliere  **Creare**.

   ![Specificare nome e URL di accesso per l'identità di applicazione](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   identità dell'applicazione Hello creato per l'app logica ora viene visualizzato nell'elenco di registrazioni app hello.

   ![Identità di applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Nell'elenco di registrazioni hello app, selezionare la nuova identità di applicazione. Copiare e salvare hello **ID applicazione** toouse come hello "ID client" per l'app logica nella parte 3.

   ![Copiare e salvare l'ID applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Se le impostazioni dell'identità di applicazione non sono visibili, scegliere **Impostazioni** o **Tutte le impostazioni**.

7. Scegliere **Chiavi** in **Accesso all'API**. In **Descrizione** specificare un nome per la chiave. Selezionare una **scadenza** per la durata della chiave.

   chiave Hello che si sta creando funge da dell'identità di applicazione hello "segreto" o la password per l'app logica.

   ![Creare una chiave per l'identità dell'app per la logica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Sulla barra degli strumenti hello, scegliere **salvare**. La chiave viene visualizzata in **Valore**. 
**Verificare che toocopy e salvare la chiave** per un utilizzo successivo perché è nascosta chiave hello se si lascia pannello chiave hello.

   Quando si configura l'app logica nella parte 3, specificare questa chiave come hello "segreto" o la password.

   ![Copiare e salvare la chiave per usarla in un momento successivo](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Creare l'identità dell'applicazione hello per le app per la logica nel portale di Azure classico hello**

1. Nel portale di Azure classico hello, scegliere [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Selezionare hello stessa directory in cui si utilizza per l'app web o app per le API.

3. In hello **applicazioni** scegliere **Aggiungi** nella parte inferiore di hello della pagina hello.

4. Assegnare un nome all'identità di applicazione e scegliere **Avanti** (freccia destra).

5. In **Proprietà dell'app** specificare una stringa univoca formattata come dominio per **URL accesso** e **URI ID app** e scegliere **Completa** (segno di spunta).

6. In hello **configura** scheda, copiare e salvare hello **ID Client** per il toouse app logica nella parte 3.

7. In **chiavi**aprire hello **Seleziona durata** elenco. Selezionare una durata per la chiave.

   chiave Hello che si sta creando funge da dell'identità di applicazione hello "segreto" o la password per l'app logica.

8. Nella parte inferiore di hello della pagina hello, scegliere **salvare**. Potrebbe essere toowait pochi secondi.

9. In **chiavi**, assicurarsi che toocopy e salvare chiave hello che viene visualizzato. 

   Quando si configura l'app logica nella parte 3, specificare questa chiave come hello "segreto" o la password.

Per ulteriori informazioni, vedere come troppo [configurare l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Creare l'identità dell'applicazione hello per le app per la logica in PowerShell**

È possibile eseguire questa attività usando Azure Resource Manager con PowerShell. In PowerShell eseguire questi comandi:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Verificare che hello toocopy **ID Tenant** hello (GUID per il tenant di Azure AD), **ID applicazione**e la password di hello utilizzato.

Per ulteriori informazioni, vedere come troppo [creare un'entità servizio con PowerShell tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Parte 2: Creare un'identità di applicazione di Azure AD per l'app Web o l'app per le API

Se è già stato distribuito l'app web o app per le API, è possibile attivare l'autenticazione e creare l'identità dell'applicazione hello in hello portale di Azure. In alternativa, è possibile [attivare l'autenticazione quando si effettua la distribuzione con un modello di Azure Resource Manager](#authen-deploy). 

**Creare l'identità dell'applicazione hello e attivare l'autenticazione nel portale di Azure per le app distribuite hello**

1. In hello [portale di Azure](https://portal.azure.com "https://portal.azure.com"), individuare e selezionare le app web o API. 

2. In **Impostazioni** scegliere **Autenticazione/Autorizzazione**. In **Autenticazione servizio app** **attivare** l'autenticazione. In **Provider di autenticazione** scegliere **Azure Active Directory**.

   ![Attivare l'autenticazione](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Creare un'identità di applicazione per l'app Web o l'app per le API come indicato di seguito. In hello **impostazioni di Azure Active Directory** pannello, impostare **modalità di gestione** troppo**Express**. Scegliere **Crea nuova App AD**. Assegnare un nome all'identità di applicazione e scegliere **OK**. 

   ![Creare un'identità di applicazione per l'app Web o l'app per le API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. In hello **autenticazione / pannello autorizzazione**, scegliere **salvare**.

A questo punto è necessario trovare l'ID client hello e ID tenant per l'identità di applicazione hello associata con l'app web o app per le API. Questi ID verranno usati nella Parte 3. Pertanto, continuare con la procedura per hello portale di Azure o [portale di Azure classico](#find-id-classic).

**Trovare l'ID client dell'identità di applicazione e l'ID tenant per l'app web o app per le API nel portale di Azure hello**

1. In **Provider di autenticazione** scegliere **Azure Active Directory**. 

   ![Scegliere "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. In hello **impostazioni di Azure Active Directory** pannello, impostare **modalità di gestione** troppo**avanzate**.

3. Hello copia **ID Client**e salvare tale GUID per l'utilizzo nella parte 3.

   > [!TIP] 
   > Se **ID Client** e **Url autorità di certificazione** non vengono visualizzati, provare ad aggiornare hello portale di Azure e ripetere il passaggio 1.

4. In **Url autorità di certificazione**, copiare e salvare solo hello GUID per la parte 3. È anche possibile usare questo GUID nel modello di distribuzione dell'app Web o app per le API, se necessario.

   Questo GUID è il GUID del tenant specifico ("ID tenant") e deve apparire in questo URL: `https://sts.windows.net/{GUID}`

5. Senza salvare le modifiche, chiudere hello **impostazioni di Azure Active Directory** blade.

<a name="find-id-classic"></a>

**Trovare l'ID client dell'identità di applicazione e l'ID tenant per l'app web o app per le API nel portale di Azure classico hello**

1. Nel portale di Azure classico hello, scegliere [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Selezionare la directory di hello utilizzato per le app web o API.

3. In hello **ricerca** , trovare e selezionare l'identità dell'applicazione hello per le app web o API.

4. In hello **configura** scheda, hello copia **ID Client**e salvare tale GUID per l'utilizzo nella parte 3.

5. Dopo avere ottenuto l'ID client hello, nella parte inferiore di hello di hello **configura** scegliere **visualizzare endpoint**.

6. Copia URL hello per **documento metadati federazione**e passare toothat URL.

7. Nel documento di metadati hello che si apre, trovare radice hello **EntityDescriptor ID** elemento, che ha un **entityID** attributo in questo formato:`https://sts.windows.net/{GUID}` 

      Hello GUID in questo attributo è il GUID del tenant specifica (ID tenant).

8. Copiare l'ID tenant hello e salvare tale ID per l'utilizzo nella parte 3 e toouse in app web o il modello di distribuzione dell'app dell'API, se necessario.

Per altre informazioni, vedere gli argomenti seguenti:

* [Autenticazione utente per le app per le API nel servizio app di Azure](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Attivare l'autenticazione quando si esegue la distribuzione con un modello di Azure Resource Manager**

È ancora necessario creare identità di un'applicazione Azure AD per l'app web o app per le API che differisce dall'identità dell'applicazione hello per le app per la logica. identità dell'applicazione hello toocreate, seguire hello precedente procedura nella parte 2 di hello portale di Azure. È anche possibile seguire i passaggi di hello nella parte 1, ma rendere toouse che l'app web o dell'app per le API effettivo `https://{URL}` per **Sign-on URL** e **URI ID App**. Da questi passaggi, è necessario toosave sia client hello ID e l'ID tenant per l'utilizzo nel modello di distribuzione dell'applicazione, nonché per la parte 3.

> [!NOTE]
> Quando si crea l'identità dell'applicazione hello Azure AD per le app web o API, è necessario utilizzare hello portale di Azure o portale di Azure classico, anziché PowerShell. cmdlet di PowerShell Hello non impostare le autorizzazioni di hello necessario toosign gli utenti in un sito Web.

Dopo avere ottenuto l'ID client hello e l'ID tenant, è possibile includere questi ID come un subresource dell'app web o app per le API del modello di distribuzione:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically distribuire un'app web vuota e una logica app con l'autenticazione di Azure Active Directory, [visualizzazione hello completo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), oppure fare clic su **distribuire tooAzure** qui:

[![Distribuire tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Parte 3: Popolare sezione Authorization hello nell'app logica

modello precedente di Hello ha già impostata in questa sezione di autorizzazione, ma se si modifica direttamente hello logica app, è necessario includere sezione autorizzazioni complete hello.

Aprire la definizione dell'app logica nella visualizzazione codice, passa toohello **HTTP** una sezione di azione di ricerca hello **autorizzazione** sezione e includere questa riga:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Elemento | Descrizione |
| ------- | ----------- |
| tenant |Hello GUID per il tenant hello Azure AD |
| audience |Obbligatorio. Hello GUID per la risorsa di destinazione hello che si desidera tooaccess - ID client hello dall'identità dell'applicazione hello per le app web o API |
| clientId |Hello GUID per il client di hello richiedendo l'accesso - ID client hello dall'identità dell'applicazione hello per le app per la logica |
| secret |Obbligatorio. Hello chiave o una password dall'identità dell'applicazione hello per client hello che richiede il token di accesso di hello |
| type |tipo di autenticazione Hello. Per l'autenticazione ActiveDirectoryOAuth, il valore di hello è `ActiveDirectoryOAuth`. |

ad esempio:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Chiamate API protette con codice

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Autenticazione del certificato

toovalidate hello le richieste in ingresso dal logica app tooyour web app o app per le API, è possibile utilizzare i certificati client. informazioni su tooset il codice, [come l'autenticazione reciproca TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

In hello **autorizzazione** sezione, includere questa riga: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Elemento | Descrizione |
| ------- | ----------- |
| type |Obbligatorio. tipo di autenticazione Hello. Per i certificati client SSL, deve essere il valore di hello `ClientCertificate`. |
| password |Obbligatorio. password di Hello per accedere al certificato del client hello (file. PFX) |
| pfx |Obbligatorio. Contenuto con codifica Base64 del certificato del client hello (file. PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Autenticazione di base

toovalidate richieste in ingresso dal logica app tooyour web app o app per le API, è possibile utilizzare l'autenticazione di base, ad esempio un nome utente e password. Autenticazione di base è un modello comune, e le app web o API, è possibile utilizzare l'autenticazione in qualsiasi toobuild linguaggio utilizzato.

In hello **autorizzazione** sezione, includere questa riga:

`{"type": "basic", "username": "username", "password": "password"}`.

| Elemento | Descrizione |
| --- | --- |
| type |Obbligatorio. tipo di autenticazione Hello. L'autenticazione di base, deve essere il valore di hello `Basic`. |
| username |Obbligatorio. nome utente di Hello per l'autenticazione |
| password |Obbligatorio. password Hello per l'autenticazione |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Autenticazione di Azure Active Directory usando il codice

Per impostazione predefinita, l'autenticazione di Azure AD hello che attivare in hello portale di Azure non fornisce un'autorizzazione. Ad esempio, questa autenticazione Blocca toojust l'API, un tenant specifico, non tooa utente o specifico dell'applicazione. 

API toorestrict accesso tooyour logica app tramite codice, estrarre l'intestazione hello che dispone di hello JSON web token (JWT). Verificare l'identità del chiamante hello e rifiutare le richieste che non corrispondono.

Continua, tooimplement questa autenticazione interamente nel proprio codice e non utilizzare hello portale di Azure, informazioni su come troppo [l'autenticazione con locale di Active Directory in Azure app](../app-service-web/web-sites-authentication-authorization.md).

identità di un'applicazione per l'app logica toocreate e utilizzare tale toocall identità dell'API, è necessario seguire i passaggi precedenti hello.

## <a name="next-steps"></a>Passaggi successivi

* [Controllare le prestazioni dell'app per la logica con avvisi e log di diagnostica](logic-apps-monitor-your-logic-apps.md)