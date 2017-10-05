---
title: Distribuire, chiamare e autenticare API Web e API REST per le app per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Distribuire, chiamare e autenticare le API personalizzate come connettori per le app per la logica

Dopo aver [creato le API personalizzate](./logic-apps-create-api-app.md) che offrono le azioni o i trigger da usare nei flussi di lavoro delle app per la logica, è necessario implementare le API prima di eseguire la chiamata. Sebbene sia possibile chiamare qualsiasi API da un'app per la logica, per ottimizzare i risultati aggiungere [metadati Swagger](http://swagger.io/specification/) che descrivano le operazioni e i parametri dell'API. Il file Swagger consente all'API di funzionare meglio e di integrarsi più facilmente con le app per la logica.

È possibile implementare le API come [app Web](../app-service-web/app-service-web-overview.md), ma è consigliabile distribuirle come [app per le API](../app-service-api/app-service-api-apps-why-best-platform.md), in modo da semplificare il lavoro durante la compilazione, l'hosting e l'uso delle API nel cloud e in locale. Non è necessario modificare alcun codice nelle API, è sufficiente implementare il codice a un'app per le API. È possibile ospitare le API nel [servizio app di Azure](../app-service/app-service-value-prop-what-is.md), una soluzione PaaS (platform-as-a-service) che offre uno dei modi più efficaci, semplici e scalabili per ospitare l'API.

Per autenticare le chiamate dalle app per la logica all'API, è possibile configurare Azure Active Directory nel portale di Azure, in modo da non dover aggiornare il codice. Oppure, è possibile richiedere e applicare l'autenticazione attraverso il codice dell'API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Distribuire l'API come app Web o app per le API

Prima di chiamare l'API personalizzata da un'app per la logica, implementare l'API come app Web o app per le API al servizio app di Azure. Rendere inoltre leggibile il documento Swagger per Progettazione app per la logica, impostare le proprietà di definizione dell'API e attivare la [condivisione di risorse tra le origini](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) per l'app Web o l'app per le API.

1. Nel portale di Azure selezionare l'app Web o l'app per le API.

2. Nell'area **API** del pannello visualizzato scegliere **Definizione API**. Impostare la **posizione della definizione dell'API** sull'URL del file swagger.json.

   In genere, l'URL viene visualizzato in questo formato: `https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Collegamento al file Swagger per l'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Scegliere **CORS** nell'area **API**. Impostare i criteri CORS per le **origini consentite** su **'*'** (consenti tutto).

   Questa impostazione consente le richieste da Progettazione app per la logica.

   ![Consentire le richieste da Progettazione app per la logica all'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Per altre informazioni, vedere questi articoli:

* [Aggiungere metadati Swagger per le API Web ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Distribuire app Web ASP.NET al servizio app di Azure](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Chiamare l'API personalizzata dai flussi di lavoro delle app per la logica

Dopo aver impostato le proprietà di definizione API e CORS, i trigger e le azioni dell'API personalizzata devono essere disponibili per l'inserimento nel flusso di lavoro delle app per la logica. 

*  Per visualizzare i siti Web con URL di Swagger, è possibile sfogliare i siti Web di sottoscrizione in Progettazione app per la logica.

*  Per visualizzare le azioni e gli input disponibili puntando a un documento di Swagger, usare l'[azione HTTP + Swagger](../connectors/connectors-native-http-swagger.md).

*  Per chiamare qualsiasi API, incluse le API che non hanno o non espongono un documento Swagger, è sempre possibile creare una richiesta con l'[azione HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-to-your-custom-api"></a>Autenticare le chiamate all'API personalizzata

È possibile proteggere le chiamate all'API personalizzata nei modi seguenti:

* [Nessuna modifica del codice](#no-code): proteggere l'API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) dal portale di Azure, in modo che non sia necessario aggiornare il codice o implementare nuovamente l'API.

  > [!NOTE]
  > Per impostazione predefinita, l'autenticazione di Azure AD che si attiva nel portale di Azure non offre un'autorizzazione con granularità fine. Ad esempio, questa autenticazione blocca l'API a un tenant specifico, non a un determinato utente o app. 

* [Aggiornare il codice dell'API](#update-code): proteggere l'API applicando [l'autenticazione del certificato](#certificate), [l'autenticazione di base](#basic) o [autenticazione di Azure AD](#azure-ad-code) attraverso il codice.

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a>Autenticare le chiamate all'API senza modificare il codice

Questi sono i passaggi generali per questo metodo:

1. Creare due [identità di applicazione di Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md), una per l'app per la logica e una per l'app Web (o l'app per le API).

2. Per autenticare le chiamate all'API, usare le credenziali (ID client e segreto) per l'[entità servizio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associata all'identità di applicazione di Azure AD per l'app per la logica.

3. Includere gli ID applicazione nella definizione di app per la logica.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Parte 1: Creare un'identità di applicazione di Azure AD per l'app per la logica

L'app per la logica usa questa identità di applicazione di Azure AD per l'autenticazione con Azure AD. È sufficiente impostare l'identità una sola volta per la directory. Ad esempio, si può scegliere di usare la stessa identità per tutte le app per la logica, anche se è possibile creare identità univoche per ogni app per la logica. È possibile impostare queste identità nel portale di Azure, nel [portale di Azure classico](#app-identity-logic-classic) o usare [PowerShell](#powershell).

**Creare l'identità di applicazione per l'app per la logica nel portale di Azure**

1. Nel [portale di Azure](https://portal.azure.com "https://portal.azure.com") scegliere **Azure Active Directory**. 

2. Verificare di essere nella stessa directory dell'app Web o app per le API.

   > [!TIP]
   > Per passare da una directory all'altra, fare clic sul proprio profilo e selezionare un'altra directory. In alternativa, scegliere **Panoramica** > **Cambia directory**.

3. Nel menu delle directory scegliere da **Gestisci** **Registrazioni per l'app** > **Registrazione nuova applicazione**.

   > [!TIP]
   > Per impostazione predefinita, l'elenco delle registrazioni di app indica tutte le registrazioni di app presenti nella directory. Per visualizzare solo le registrazioni delle proprie app, selezionare **Le mie app** accanto alla casella di ricerca. 

   ![Creare una nuova registrazione di app](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Assegnare un nome all'identità di applicazione, lasciare il **tipo di applicazione** impostato su **App Web/API**, specificare una stringa univoca formattata come dominio per **URL accesso** e scegliere **Crea**.

   ![Specificare nome e URL di accesso per l'identità di applicazione](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   L'identità di applicazione creata per l'app per la logica ora appare nell'elenco delle registrazioni di app.

   ![Identità di applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Nell'elenco di registrazioni di app selezionare la nuova identità di applicazione. Copiare e salvare l'**ID applicazione** da usare come "ID client" per l'app per la logica nella Parte 3.

   ![Copiare e salvare l'ID applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Se le impostazioni dell'identità di applicazione non sono visibili, scegliere **Impostazioni** o **Tutte le impostazioni**.

7. Scegliere **Chiavi** in **Accesso all'API**. In **Descrizione** specificare un nome per la chiave. Selezionare una **scadenza** per la durata della chiave.

   La chiave che si sta creando agisce come "segreto" o password dell'identità di applicazione per l'app per la logica.

   ![Creare una chiave per l'identità dell'app per la logica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Scegliere **Salva** nella barra degli strumenti. La chiave viene visualizzata in **Valore**. 
Poiché la chiave viene nascosta quando si lascia il pannello, **assicurarsi di copiarla e salvarla** per usarla in un secondo tempo.

   Quando si configura l'app per la logica nella Parte 3, si specifica questa chiave come "segreto" o password.

   ![Copiare e salvare la chiave per usarla in un momento successivo](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Creare l'identità di applicazione per l'app per la logica nel portale di Azure classico**

1. Nel portale di Azure classico scegliere [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Selezionare la stessa directory che si usa per l'app Web o l'app per le API.

3. Nella scheda **Applicazioni** scegliere **Aggiungi** nella parte inferiore della pagina.

4. Assegnare un nome all'identità di applicazione e scegliere **Avanti** (freccia destra).

5. In **Proprietà dell'app** specificare una stringa univoca formattata come dominio per **URL accesso** e **URI ID app** e scegliere **Completa** (segno di spunta).

6. Nella scheda di **configurazione** copiare e salvare l'**ID client** per l'app per la logica da usare nella Parte 3.

7. In **Chiavi** aprire l'elenco **Seleziona durata**. Selezionare una durata per la chiave.

   La chiave che si sta creando agisce come "segreto" o password dell'identità di applicazione per l'app per la logica.

8. Fare clic su **Salva** nella parte inferiore della pagina. Potrebbe essere necessario attendere alcuni secondi.

9. In **Chiavi** assicurarsi di copiare e salvare la chiave che ora viene visualizzata. 

   Quando si configura l'app per la logica nella Parte 3, si specifica questa chiave come "segreto" o password.

Per altre informazioni, vedere la procedura di [configurazione di un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Creare l'identità di applicazione per l'app per la logica in PowerShell**

È possibile eseguire questa attività usando Azure Resource Manager con PowerShell. In PowerShell eseguire questi comandi:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Assicurarsi di copiare l'**ID tenant** (GUID per il tenant di Azure AD), l'**ID applicazione** e la password usati.

Per altre informazioni, vedere la procedura di [creazione di un'entità servizio con PowerShell per accedere alle risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Parte 2: Creare un'identità di applicazione di Azure AD per l'app Web o l'app per le API

Se l'app Web o l'app per le API è già stata distribuita, è possibile attivare l'autenticazione e creare l'identità di applicazione nel portale di Azure. In alternativa, è possibile [attivare l'autenticazione quando si effettua la distribuzione con un modello di Azure Resource Manager](#authen-deploy). 

**Creare l'identità di applicazione e attivare l'autenticazione nel portale di Azure per le app distribuite**

1. Nel [portale di Azure](https://portal.azure.com "https://portal.azure.com") individuare e selezionare l'app Web o app per le API. 

2. In **Impostazioni** scegliere **Autenticazione/Autorizzazione**. In **Autenticazione servizio app** **attivare** l'autenticazione. In **Provider di autenticazione** scegliere **Azure Active Directory**.

   ![Attivare l'autenticazione](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Creare un'identità di applicazione per l'app Web o l'app per le API come indicato di seguito. Nel pannello **Impostazioni di Azure Active Directory** impostare la **modalità di gestione** su **Rapida**. Scegliere **Crea nuova App AD**. Assegnare un nome all'identità di applicazione e scegliere **OK**. 

   ![Creare un'identità di applicazione per l'app Web o l'app per le API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Nel pannello **Autenticazione/Autorizzazione** scegliere **Salva**.

A questo punto è necessario trovare l'ID client e l'ID tenant per l'identità di applicazione associata all'app Web o app per le API. Questi ID verranno usati nella Parte 3. Continuare con la procedura per il portale di Azure o il [portale di Azure classico](#find-id-classic).

**Trovare l'ID client e l'ID tenant dell'identità di applicazione per l'app Web o app per le API nel portale di Azure**

1. In **Provider di autenticazione** scegliere **Azure Active Directory**. 

   ![Scegliere "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Nel pannello **Impostazioni di Azure Active Directory** impostare la **modalità di gestione** su **Avanzata**.

3. Copiare l'**ID client** e salvare il GUID per usarlo nella Parte 3.

   > [!TIP] 
   > Se l'**ID client** e l'**URL dell'autorità di certificazione** non appaiono, provare ad aggiornare il portale di Azure e ripetere il passaggio 1.

4. In **URL autorità di certificazione** copiare e salvare solo il GUID per la Parte 3. È anche possibile usare questo GUID nel modello di distribuzione dell'app Web o app per le API, se necessario.

   Questo GUID è il GUID del tenant specifico ("ID tenant") e deve apparire in questo URL: `https://sts.windows.net/{GUID}`

5. Senza salvare le modifiche, chiudere il pannello delle **impostazioni di Azure Active Directory**.

<a name="find-id-classic"></a>

**Trovare l'ID client e l'ID tenant dell'identità di applicazione per l'app Web o app per le API nel portale di Azure classico**

1. Nel portale di Azure classico scegliere [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Selezionare la directory che si usa per l'app Web o l'app per le API.

3. Nella casella di **ricerca** trovare e selezionare l'identità di applicazione per l'app Web o app per le API.

4. Nella scheda **Configura** copiare l'**ID client** e salvare il GUID per usarlo nella Parte 3.

5. Dopo avere ottenuto l'ID client, nella parte inferiore della scheda **Configura** scegliere **Visualizza endpoint**.

6. Copiare l'URL del **documento metadati federazione** e passare a tale URL.

7. Nel documento di metadati che si apre individuare l'elemento **EntityDescriptor ID** della radice, che ha un attributo **entityID** in questo formato: `https://sts.windows.net/{GUID}` 

      Il GUID in questo attributo è il GUID del tenant specifico (ID tenant).

8. Copiare l'ID tenant e salvarlo per usarlo nella Parte 3, nonché nel modello di distribuzione dell'app Web o app per le API, se necessario.

Per altre informazioni, vedere gli argomenti seguenti:

* [Autenticazione utente per le app per le API nel servizio app di Azure](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Attivare l'autenticazione quando si esegue la distribuzione con un modello di Azure Resource Manager**

È comunque necessario creare un'identità di applicazione di Azure AD per l'app Web o app per le API che differisce dall'identità di applicazione per l'app per la logica. Per creare l'identità di applicazione, seguire i passaggi descritti in precedenza nella Parte 2 per il portale di Azure. È anche possibile seguire i passaggi della Parte 1, ma assicurarsi di usare l'elemento `https://{URL}` reale dell'app Web o app per le API per **URL accesso** e **URI dell'ID dell'app**. Da questi passaggi è necessario salvare sia l'ID client che l'ID tenant per usarli nel modello di distribuzione dell'app, nonché per la Parte 3.

> [!NOTE]
> Quando si crea l'identità di applicazione di Azure AD per l'app Web o l'app per le API, è necessario usare il portale di Azure o il portale di Azure classico, anziché PowerShell. Il cmdlet di PowerShell non consente di impostare le autorizzazioni necessarie per l'accesso degli utenti in un sito Web.

Dopo aver ottenuto l'ID client e l'ID tenant, includerli come risorsa secondaria dell'app Web o app per le API nel modello di distribuzione:

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

Per implementare automaticamente un'app Web vuota e un'app per la logica con l'autenticazione di Azure Active Directory, [visualizzare il modello completo qui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) oppure fare clic su **Distribuzione in Azure** qui:

[![Distribuzione in Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a>Parte 3: Compilare la sezione Autorizzazione nell'app per la logica

Questa sezione dell'autorizzazione è già stata configurata nel modello precedente, ma se si crea direttamente l'app per la logica, sarà necessario includere l'intera sezione relativa all'autorizzazione.

Aprire la definizione dell'app per la logica nella visualizzazione Codice, passare alla sezione dell'azione **HTTP**, trovare la sezione dell'**autorizzazione** e includere questa riga:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Elemento | Descrizione |
| ------- | ----------- |
| tenant |Il GUID per il tenant di Azure AD |
| audience |Obbligatorio. Il GUID per la risorsa di destinazione a cui si vuole accedere: ID client dall'identità di applicazione per l'app Web o app per le API |
| clientId |Il GUID per il client che richiede l'accesso: ID client dall'identità di applicazione per l'app per la logica |
| secret |Obbligatorio. La chiave o la password dall'identità di applicazione per il client che richiede il token di accesso |
| type |Il tipo di autenticazione. Per l'autenticazione ActiveDirectoryOAuth, il valore è `ActiveDirectoryOAuth`. |

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

Per convalidare le richieste in ingresso dall'app per la logica all'app Web o all'app per le API, è possibile usare i certificati client. Per configurare il codice, vedere le informazioni relative alla [configurazione dell'autenticazione reciproca TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

Includere questa riga nella sezione dell'**autorizzazione**: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Elemento | Descrizione |
| ------- | ----------- |
| type |Obbligatorio. Il tipo di autenticazione. Per i certificati client SSL, il valore deve essere `ClientCertificate`. |
| password |Obbligatorio. La password per accedere al certificato client (file PFX) |
| pfx |Obbligatorio. I contenuti del certificato client in codifica Base64 (file PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Autenticazione di base

Per convalidare le richieste in ingresso dall'app per la logica all'app Web o app per le API, è possibile usare l'autenticazione di base, ad esempio un nome utente e una password. L'autenticazione di base è un modello comune applicabile a qualsiasi linguaggio usato per compilare l'app Web o app per le API.

Includere questa riga nella sezione dell'**autorizzazione**:

`{"type": "basic", "username": "username", "password": "password"}`.

| Elemento | Descrizione |
| --- | --- |
| type |Obbligatorio. Il tipo di autenticazione. Per l'autenticazione di base il valore deve essere `Basic`. |
| username |Obbligatorio. Il nome utente per l'autenticazione |
| password |Obbligatorio. La password per l'autenticazione |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Autenticazione di Azure Active Directory usando il codice

Per impostazione predefinita, l'autenticazione di Azure AD che si attiva nel portale di Azure non offre un'autorizzazione con granularità fine. Ad esempio, questa autenticazione blocca l'API a un tenant specifico, non a un determinato utente o app. 

Per limitare l'accesso dell'API all'app per la logica usando il codice, estrarre l'intestazione che contiene il token JSON Web (JWT). Verificare l'identità del chiamante e rifiutare le richieste che non corrispondono.

Per approfondimenti su come implementare l'autenticazione interamente nel codice e non usare il Portale di Azure, vedere la procedura di [autenticazione con l'istanza locale di Active Directory nell'app Azure](../app-service-web/web-sites-authentication-authorization.md).

È necessario seguire la procedura precedente per creare un'identità di applicazione per l'app per la logica e usarla per chiamare l'API.

## <a name="next-steps"></a>Passaggi successivi

* [Controllare le prestazioni dell'app per la logica con avvisi e log di diagnostica](logic-apps-monitor-your-logic-apps.md)