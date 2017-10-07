---
title: aaaProtect un back-end Web API con Azure Active Directory e gestione API | Documenti Microsoft
description: Informazioni su come tooprotect un back-end Web API con Azure Active Directory e gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Come tooprotect un back-end Web API con Azure Active Directory e gestione API
Hello seguente video viene illustrato come toobuild un back-end Web API e proteggerla mediante il protocollo OAuth 2.0 con Azure Active Directory e gestione API.  In questo articolo viene fornita una panoramica e informazioni aggiuntive per hello i passaggi nel video hello. Il video della durata di 24 minuti mostra come fare per:

* Compilare il back-end di un'API Web e proteggerlo con AAD - iniziando all’1:30
* Importare l'API hello in Gestione API, a partire da 7:10
* Configurare hello Developer toocall portale hello API, a partire da 9:09
* Configurare un hello toocall applicazione desktop API, a partire da 18:08
* Configurare un toopre di criteri di convalida JWT-autorizzare richieste - a partire da 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Creare una directory di Azure AD
toosecure l'API Web eseguito tramite Azure Active Directory è necessario disporre di un un tenant di AAD. Questo video usa un tenant denominato **APIMDemo** . toocreate un tenant di AAD, accedi toohello [portale di Azure classico](https://manage.windowsazure.com) e fare clic su **New**->**servizi App**->**Active Directory**->**Directory**->**creazione personalizzata**. 

![Azure Active Directory][api-management-create-aad-menu]

In questo esempio viene creata una directory denominata **APIMDemo** con un dominio predefinito denominato **DemoAPIM.onmicrosoft.com**. Questa directory viene utilizzata in tutto il video hello.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Creare un servizio API Web protetto da Azure Active Directory
In questo passaggio viene creato il back-end di un'API Web con Visual Studio 2013. Questo passaggio di hello video inizia da 1:30. progetto di back-end Web API toocreate in fare clic su Visual Studio **File**->**New**->**progetto**e scegliere **Web ASP.NET Applicazione** da hello **Web** elenco di modelli. In questo video hello progetto viene denominato **APIMAADDemo**. Fare clic su **OK** progetto hello toocreate. 

![Visual Studio][api-management-new-web-app]

Fare clic su **API Web** da hello **selezionare un modello di elenco** toocreate un progetto di API Web. Fare clic su autenticazione di Azure Directory tooconfigure **Modifica autenticazione**.

![Nuovo progetto][api-management-new-project]

Fare clic su **account aziendali**e specificare hello **dominio** del tenant di AAD. In hello in questo esempio è dominio **DemoAPIM.onmicrosoft.com**. dominio hello di directory può essere ottenuto dalla hello **domini** della directory.

![Domini][api-management-aad-domains]

Configurare le impostazioni di hello desiderato in hello **Modifica autenticazione** la finestra di dialogo e fare clic su **OK**.

![Modifica autenticazione][api-management-change-authentication]

Quando fa clic su **OK** Visual Studio tenterà tooregister l'applicazione con la directory di Azure AD e potrebbe essere richiesta toosign in Visual Studio. Accedere con un account amministrativo per la directory.

![Accedi tooVisual Studio][api-management-sign-in-vidual-studio]

Questo progetto come un hello controllo API Web di Azure di tooconfigure casella per **Host nel cloud hello** e quindi fare clic su **OK**.

![Nuovo progetto][api-management-new-project-cloud]

Potrebbe essere richiesta toosign in tooAzure e quindi è possibile configurare hello App Web.

![Configurare][api-management-configure-web-app]

In questo esempio viene specificato un nuovo **Piano di servizio app** denominato **APIMAADDemo**.

Fare clic su **OK** tooconfigure hello Web App e creare il progetto di hello.

## <a name="add-hello-code-toohello-web-api-project"></a>Aggiungere il progetto API Web di hello codice toohello
passaggio successivo Hello video hello aggiunge il progetto hello codice toohello API Web. Questo passaggio inizia da 4:35 minuti.

Hello API Web in questo esempio implementa un servizio di calcolatrice di base usando un modello e un controller. modello di hello tooadd per il servizio di hello, fare doppio clic su **modelli** in **Esplora** e scegliere **Aggiungi**, **classe**. Nome classe hello `CalcInput` e fare clic su **Aggiungi**.

Aggiungere il seguente hello `using` hello cima toohello istruzione `CalcInput.cs` file.

```c#
using Newtonsoft.Json;
```

Sostituire la classe hello generato con hello seguente codice.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Fare clic con il pulsante destro del mouse su **Controller** in **Esplora soluzioni** e scegliere **Aggiungi**->**Controller**. Scegliere **Web API 2 Controller - Empty** e fare clic su **Aggiungi**. Tipo **CalcController** per hello Controller e fare clic su **Aggiungi**.

![Aggiungi controller][api-management-add-controller]

Aggiungere il seguente hello `using` hello cima toohello istruzione `CalcController.cs` file.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Sostituire classe controller hello generato con hello seguente codice. Questo codice implementa hello `Add`, `Subtract`, `Multiply`, e `Divide` operazioni di base API Calculator hello.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Premere **F6** toobuild e verificare la soluzione hello.

## <a name="publish-hello-project-tooazure"></a>Pubblicare hello progetto tooAzure
In questo hello passaggio Visual Studio progetto è tooAzure pubblicato. Questo passaggio di hello video inizia in corrispondenza di 5:45.

toopublish hello progetto tooAzure destro del mouse su hello **APIMAADDemo** sul progetto in Visual Studio e scegliere **pubblica**. Mantenere le impostazioni predefinite di hello in hello **pubblica sul Web** la finestra di dialogo e fare clic su **pubblica**.

![Pubblicazione sul Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Concedere le autorizzazioni applicazione del servizio back-end toohello Azure AD
Viene creata una nuova applicazione per il servizio back-end hello nella directory di Azure AD come parte della configurazione hello e processo di pubblicazione del progetto API Web. In questo passaggio di hello video a partire da 6:13, le autorizzazioni vengono concesse back-end Web API toohello.

![Applicazione][api-management-aad-backend-app]

Fare clic su nome hello di autorizzazioni di hello applicazione tooconfigure hello necessario. Passare toohello **configura** scheda e scorrere verso il basso toohello **autorizzazioni tooother applicazioni** sezione. Fare clic su hello **autorizzazioni applicazione** elenco a discesa accanto a **Windows** **Azure Active Directory**, casella hello per **lettura dati directory**, fare clic su **salvare**.

![Aggiungere autorizzazioni][api-management-aad-add-permissions]

> [!NOTE]
> Se **Windows** **Azure Active Directory** non è elencato nel autorizzazioni tooother applicazioni, fare clic su **aggiungere applicazione** e aggiungere l'elenco di hello.
> 
> 

Prendere nota di hello **URI Id App** per l'utilizzo in un passaggio successivo, quando un'applicazione Azure AD è configurata per portale per sviluppatori di hello gestione API.

![URI ID app][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Importare hello API Web in Gestione API
Le API vengono configurate dal portale di pubblicazione di hello API, è possibile accedervi tramite hello portale di Azure. tooreach, fare clic su **portale di pubblicazione** dalla barra degli strumenti hello del servizio Gestione API. Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [gestione API prima] [ Manage your first API] esercitazione.

![Portale di pubblicazione][api-management-management-console]

Le operazioni possono essere [aggiunti manualmente tooAPIs](api-management-howto-add-operations.md), o possono essere importati. In questo video le operazioni vengono importante in formato Swagger a partire da 6:40 minuti.

Creare un file denominato `calcapi.json` con contenuto seguente e salvarlo tooyour computer. Verificare che hello `host` attributo punta back-end Web API tooyour. In questo esempio viene usato `"host": "apimaaddemo.azurewebsites.net"` .

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

Calcolatrice hello tooimport API, fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importazione API**.

![Pulsante Importa API][api-management-import-api]

Eseguire hello seguendo i passaggi tooconfigure hello calcolatrice API.

1. Fare clic su **dal file**, Sfoglia toohello `calculator.json` file salvato e fare clic su hello **Swagger** pulsante di opzione.
2. Tipo **calc** in hello **suffisso URL di Web API** casella di testo.
3. Fare clic nella hello **prodotti (facoltativi)** e scegliere **Starter**.
4. Fare clic su **salvare** tooimport hello API.

![Add new API][api-management-import-new-api]

Una volta importato, hello API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Chiamare API hello correttamente dal portale per sviluppatori hello
A questo punto, hello API è stata importata in Gestione API, ma può ancora essere chiamato correttamente dal portale per sviluppatori hello perché il servizio back-end hello è protetto con autenticazione di Azure AD. Come illustrato nel video hello a partire da 7:40 utilizzando hello alla procedura seguente.

Fare clic su **portale per sviluppatori** dalla parte superiore destra hello del portale di pubblicazione hello.

![Portale per sviluppatori][api-management-developer-portal-menu]

Fare clic su **API** e fare clic su hello **Calcolatrice** API.

![Portale per sviluppatori][api-management-dev-portal-apis]

Fare clic su **Prova**.

![Prova][api-management-dev-portal-try-it]

Fare clic su **inviare** e prendere nota di stato della risposta hello **401 non autorizzato**.

![Invio][api-management-dev-portal-send-401]

non è autorizzato richiesta Hello poiché API back-end hello è protetto da Azure Active Directory. Prima di esito positivo della chiamata API hello portale per sviluppatori hello deve essere configurato tooauthorize sviluppatori mediante OAuth 2.0. Questo processo è descritto nelle seguenti sezioni hello.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Registrare il portale per sviluppatori di hello come un'applicazione AAD
primo passaggio di Hello nella configurazione gli sviluppatori di tooauthorize portale per sviluppatori hello mediante OAuth 2.0 è portale per sviluppatori di hello tooregister come un'applicazione AAD. A partire da 8:27 video hello illustrato.

Passare a tenant di Azure AD toohello innanzitutto hello del video, in questo esempio **APIMDemo** e passare toohello **applicazioni** scheda.

![Nuova applicazione][api-management-aad-new-application-devportal]

Fare clic su hello **Aggiungi** toocreate una nuova applicazione Azure Active Directory e scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.

![Nuova applicazione][api-management-new-aad-application-menu]

Scegliere **Web dell'applicazione e/o API Web**, immettere un nome e fare clic sulla freccia avanti hello. In questo esempio viene usato **APIMDeveloperPortal** .

![Nuova applicazione][api-management-aad-new-application-devportal-1]

Per **Sign-on URL** immettere hello URL del servizio Gestione API e aggiungere `/signin`. In questo esempio viene usato `https://contoso5.portal.azure-api.net/signin` .

Per **URL Id App** immettere hello URL del servizio Gestione API e aggiungere alcuni caratteri univoci. Si può usare qualsiasi carattere. In questo esempio vengono usati `https://contoso5.portal.azure-api.net/dp`. Quando lo si desidera hello **proprietà App** sono configurate, fare clic su un'applicazione hello toocreate hello segno di spunta.

![Nuova applicazione][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Configurare un server autorizzazione OAuth 2.0 in Gestione API
passaggio successivo Hello è tooconfigure un server di autorizzazione OAuth 2.0 in Gestione API. Questo passaggio è illustrato in hello video a partire da 9:43.

Fare clic su **sicurezza** hello gestione API scegliere dal menu a sinistra di hello **OAuth 2.0**, quindi fare clic su **aggiungere autorizzazione** server.

![Add authorization server][api-management-add-authorization-server]

Immettere un nome e una descrizione facoltativa in hello **nome** e **descrizione** campi. Questi campi sono server di autorizzazione OAuth 2.0 hello tooidentify utilizzati nell'istanza del servizio Gestione API di hello. In questo esempio viene usato **Authorization server demo** . In un secondo momento quando si specifica un toobe server OAuth 2.0 utilizzata per l'autenticazione per un'API, si selezionerà il nome specificato.

Per hello **URL pagina di registrazione Client** immettere un valore segnaposto, ad esempio `http://localhost`.  Hello **URL pagina di registrazione Client** punti toohello pagina che gli utenti possono utilizzare toocreate e configurare i propri account per i provider di OAuth 2.0 che supportano la gestione degli account utente. In questo esempio gli utenti non creano e configurano i propri account, quindi si usa un segnaposto.

![Add authorization server][api-management-add-authorization-server-1]

Successivamente, specificare un valore per **Authorization endpoint URL** e **Token endpoint URL**.

![Serve autorizzazione][api-management-add-authorization-server-1a]

Questi valori possono essere recuperati da hello **endpoint dell'App** pagina dell'applicazione AAD creato per il portale per sviluppatori di hello hello. gli endpoint hello tooaccess passare toohello **configura** per un'applicazione hello AAD scheda e fare clic su **visualizzare endpoint**.

![Applicazione][api-management-aad-devportal-application]

![Visualizza endpoint][api-management-aad-view-endpoints]

Hello copia **endpoint di autorizzazione OAuth 2.0** e incollarlo in hello **autorizzazione URL dell'endpoint** casella di testo.

![Add authorization server][api-management-add-authorization-server-2]

Hello copia **endpoint token OAuth 2.0** e incollarlo in hello **URL dell'endpoint del Token** casella di testo.

![Add authorization server][api-management-add-authorization-server-2a]

Inoltre toopasting nell'endpoint token hello, aggiungere un parametro aggiuntivo corpo denominato **risorse** e per valore hello utilizzare hello **URI Id App** da hello applicazione AAD per il servizio back-end hello che è stato Quando è stato pubblicato il progetto di Visual Studio hello creata.

![URI ID app][api-management-aad-sso-uri]

Successivamente, specificare le credenziali di hello del client. Queste sono le credenziali di hello per risorsa hello da tooaccess, in questo caso hello portale per sviluppatori.

![Credenziali del client][api-management-client-credentials]

hello tooget **Id Client**, passare toohello **configura** scheda di hello applicazione AAD per hello di portale e copia developer hello **Id Client**.

hello tooget **segreto Client** fare clic su hello **Seleziona durata** menu a discesa hello **chiavi** sezione e specificare un intervallo. In questo esempio viene usato 1 anno.

![ID client][api-management-aad-client-id]

Fare clic su **salvare** chiave hello configurazione e la visualizzazione toosave hello. 

> [!IMPORTANT]
> Annotare il valore relativo alla chiave. Quando si chiude una finestra di configurazione di hello Azure Active Directory, non è più visualizzata chiave hello.
> 
> 

Chiave hello toohello chiave negli Appunti Copia hello portale di pubblicazione toohello indietro di commutatore, incollare hello **segreto Client** casella di testo, fare clic su **salvare**.

![Add authorization server][api-management-add-authorization-server-3]

Subito dopo le credenziali del client hello è una concessione del codice di autorizzazione. Copiare questo codice di autorizzazione e switch back tooyour dell'applicazione del portale di Azure AD per sviluppatori pagina di configurazione e incollare la concessione di autorizzazione hello hello **URL di risposta** campo e fare clic su **salvare** nuovamente.

![URL di risposta][api-management-aad-reply-url]

passaggio successivo Hello è autorizzazioni hello tooconfigure per il portale per sviluppatori hello applicazione AAD. Fare clic su **autorizzazioni applicazione** e casella hello per **lettura dati directory**. Fare clic su **salvare** toosave questa modifica e quindi fare clic su **aggiungere applicazione**.

![Aggiungere autorizzazioni][api-management-add-devportal-permissions]

Fare clic sull'icona di ricerca di hello, tipo **ruoli** in hello a partire dalla casella, selezionare **APIMAADDemo**, fare clic su hello toosave di segno di spunta.

![Aggiungere autorizzazioni][api-management-aad-add-app-permissions]

Fare clic su **autorizzazioni delegate** per **APIMAADDemo** e casella hello per **accesso APIMAADDemo**, fare clic su **salvare**. In questo modo developer hello servizio back-end di hello tooaccess dell'applicazione del portale.

![Aggiungere autorizzazioni][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Attivare l'autorizzazione utente OAuth 2.0 per hello API calcolatrice
Ora che hello OAuth 2.0 server è configurato, è possibile specificarla nelle impostazioni di sicurezza hello per le API. Questo passaggio è illustrato in hello video a partire da 14:30.

Fare clic su **API** in hello menu a sinistra, quindi fare clic su **Calcolatrice** tooview e configurare le impostazioni.

![API Calculator][api-management-calc-api]

Passare toohello **sicurezza** scheda, controllare hello **OAuth 2.0** casella di controllo, il server di autorizzazione desiderato selezionare hello da hello **server autorizzazione** elenco a discesa e fare clic su **Salvare**.

![API Calculator][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Chiamare correttamente hello calcolatrice API dal portale per sviluppatori hello
Ora che l'autorizzazione di OAuth 2.0 hello è configurata su hello API, le operazioni possono essere chiamate correttamente dal centro per sviluppatori hello. Questo passaggio è illustrato in hello video a partire da 15:00.

Spostarsi indietro toohello **aggiungere due numeri interi** operazione del servizio di calcolatrice hello nel portale per sviluppatori hello e fare clic su **provarla**. Nuovo elemento hello nota in hello **autorizzazione** sezione appena aggiunto un server di autorizzazione toohello corrispondente.

![API Calculator][api-management-calc-authorization-server]

Selezionare **codice di autorizzazione** dall'autorizzazione hello elenco a discesa elenco e immettere le credenziali di hello di hello account toouse. Se già eseguito l'accesso con account hello potrebbero non essere richieste.

![API Calculator][api-management-devportal-authorization-code]

Fare clic su **inviare** e hello nota **stato della risposta** di **200 OK** e hello risultati dell'operazione di hello nel contenuto della risposta hello.

![API Calculator][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Configurare un hello toocall applicazione desktop API
procedura Hello in hello video inizia in corrispondenza di 16:30 e configura hello di toocall API una semplice applicazione desktop. primo passaggio Hello è tooregister applicazione desktop di hello in Azure AD e assegnargli accesso toohello directory e toohello back-end del servizio. 18:25 è una dimostrazione di un'applicazione desktop hello richiamare un'operazione su Calcolatrice hello API.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Configurare un toopre di criteri di convalida JWT-autorizzare richieste
inizia da 20:48 Hello procedura finale nel video hello e illustra come hello toouse [convalidare JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre criteri-autorizzare richieste convalidando i token di accesso hello di ogni richiesta in ingresso. Se è richiesta hello non vengono convalidato dai criteri di convalida JWT hello, richiesta hello è bloccato da Gestione API e viene passato non toohello di back-end.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Per un altro dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più le funzionalità di gestione API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too13:50. Avanzamento rapido too15:00 criteri hello toosee configurati nell'editor Criteri di hello e quindi too18:50 per una dimostrazione di chiamata di un'operazione dal portale per sviluppatori di hello con e senza hello necessari token di autorizzazione.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sui [video](https://azure.microsoft.com/documentation/videos/index/?services=api-management) relativi a Gestione API.
* Per altri modi toosecure servizio back-end, vedere [autenticazione reciproca del certificato](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
