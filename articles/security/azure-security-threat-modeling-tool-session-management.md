---
title: Gestione - di modellazione strumento Microsoft Threat - Azure aaaSession | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Infrastruttura di sicurezza: gestione della sessione - Articoli 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD](#logout-adal)</li></ul> |
| Dispositivo IoT | <ul><li>[Usare durate limitate per i token di firma di accesso condiviso generati](#finite-tokens)</li></ul> |
| **Azure Document DB** | <ul><li>[Usare durate minime per i token delle risorse generati](#resource-tokens)</li></ul> |
| **AD FS** | <ul><li>[Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS](#wsfederation-logout)</li></ul> |
| **Identity Server** | <ul><li>[Implementare la disconnessione appropriata quando si usa Identity Server](#proper-logout)</li></ul> |
| **Applicazione Web** | <ul><li>[Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri](#https-secure-cookies)</li><li>[Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie](#cookie-definition)</li><li>[Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET](#csrf-asp)</li><li>[Configurare una sessione per la durata dell'inattività](#inactivity-lifetime)</li><li>[Implementa la disconnessione appropriata da un'applicazione hello](#proper-app-logout)</li></ul> |
| **API Web** | <ul><li>[Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Se un'applicazione hello si basa sul token di accesso rilasciato da Azure AD, è necessario chiamare gestore eventi di disconnessione hello |

### <a name="example"></a>Esempio
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Esempio
Eliminerà anche definitivamente la sessione dell'utente chiamando il metodo Session.Abandon(). Il metodo seguente illustra l'implementazione sicura della disconnessione utente:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Usare durate limitate per i token di firma di accesso condiviso generati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | I token di firma di accesso condiviso generati per l'autenticazione tooAzure IoT Hub dovrebbero avere un periodo di scadenza precisa. Mantenere hello SaS durata dei token tooa toolimit minimo hello tempo totale che possono essere riprodotte nel caso in cui i token hello risultano compromesse.|

## <a id="resource-tokens"></a>Usare durate minime per i token delle risorse generati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Ridurre timespan hello del valore minimo tooa token risorsa richiesto. I token delle risorse hanno un intervallo di tempo valido predefinito di 1 ora.|

## <a id="wsfederation-logout"></a>Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | AD FS | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Se un'applicazione hello si basa sul token di servizio token di sicurezza emesso da ADFS, gestore eventi di disconnessione hello deve chiamare WSFederationAuthenticationModule.FederatedSignOut() metodo toolog utente hello. Anche hello sessione corrente deve essere eliminato e valore del token di sessione hello deve essere reimpostato e considerati eliminati.|

### <a name="example"></a>Esempio
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implementare la disconnessione appropriata quando si usa Identity Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [IdentityServer3: disconnessione federata](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Passaggi** | IdentityServer supporta hello possibilità toofederate con i provider di identità esterna. Quando un utente esce da un provider di identità a monte, in base al protocollo hello utilizzato, potrebbe essere possibile tooreceive una notifica al momento della disconnessione utente hello. Consente di toonotify IdentityServer dei client in modo che possano accedere anche hello utente out. Controllare la documentazione di hello nella sezione dei riferimenti per i dettagli di implementazione hello hello.|

## <a id="https-secure-cookies"></a>Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: locale |
| **Riferimenti**              | [Elemento httpCookies (schema delle impostazioni ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Proprietà HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Passaggi** | I cookie sono in genere solo per i quali vengono sono stati nell'ambito di dominio toohello accessibile. Purtroppo, definizione hello di "dominio" non include il protocollo di hello in modo che i cookie che vengono creati tramite HTTPS sono accessibili tramite HTTP. attributo "sicuro" Hello indica browser toohello hello cookie devono solo essere resi disponibili tramite HTTPS. Assicurarsi che tutti i cookie impostati su HTTPS utilizzino hello **sicura** attributo. requisito di Hello può essere applicata nel file Web. config hello impostando tootrue attributo requireSSL di hello. Si tratta di hello preferito approccio perché applicherà hello **sicura** attributo per tutti i cookie attuali e futuri senza hello necessità toomake eventuali ulteriori modifiche al codice.|

### <a name="example"></a>Esempio
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
anche se quest'ultimo è un'applicazione hello tooaccess usato, viene applicata l'impostazione di Hello. Se viene utilizzato HTTP tooaccess hello applicazione, le interruzioni di impostazione applicazione hello perché i cookie hello sono impostati con i browser di attributo e hello sicuro hello non invierà li hello riaggiungere toohello applicazione.

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form, MVC 5 |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: locale |
| **Riferimenti**              | N/D  |
| **Passaggi** | Quando un'applicazione web hello è hello Relying Party e hello IdP è server ADFS, attributo di protezione del token FedAuth hello può essere configurato dall'impostazione tooTrue requireSSL in `system.identityModel.services` sezione di Web. config:|

### <a name="example"></a>Esempio
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Secure Cookie Attribute](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) (Attributo dei cookie Secure) |
| **Passaggi** | rischio di hello toomitigate divulgazione di informazioni con un attacco di tipo cross-site scripting (XSS), un nuovo attributo - httpOnly - è stato introdotto toocookies ed è supportato da tutti i browser principali. attributo di Hello specifica che un cookie non è accessibile tramite script. Utilizzando cookie HttpOnly, un'applicazione web riduce le possibilità hello che informazioni riservate contenute nel cookie hello possono essere rubate tramite script e inviate tooan suo sito Web. |

### <a name="example"></a>Esempio
Tutte le applicazioni basate su HTTP che usano cookie devono specificare HttpOnly nella definizione di cookie hello, mediante l'implementazione seguente configurazione in Web. config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Proprietà FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Passaggi** | valore della proprietà RequireSSL Hello è impostato nel file di configurazione hello per un'applicazione ASP.NET tramite l'attributo requireSSL hello dell'elemento di configurazione hello. È possibile specificare nel file Web. config hello per l'applicazione ASP.NET se SSL (Secure Sockets Layer) è necessario tooreturn hello autenticazione basata su form cookie toohello dall'impostazione dell'attributo requireSSL hello.|

### <a name="example"></a>Esempio 
Hello esempio di codice seguente imposta attributo requireSSL hello nel file Web. config hello.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5 |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: locale |
| **Riferimenti**              | [Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) (Configurazione di Windows Identity Foundation (WIF): parte II) |
| **Passaggi** | attributo httpOnly tooset dei cookie FedAuth hideFromCsript valore di attributo deve essere impostato tooTrue. |

### <a name="example"></a>Esempio
Configurazione seguente mostra la configurazione corretta di hello:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Falsificazione della richiesta tra siti tra (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di sicurezza hello di sessione stabilita di un altro utente in un sito web. obiettivo di Hello è toomodify o eliminare il contenuto del sito web di destinazione hello si basa esclusivamente su richiesta ricevuta tooauthenticate i cookie di sessione. Un utente malintenzionato potrebbe sfruttare questa vulnerabilità tramite il recupero di un URL con un comando tooload browser di un utente diverso da un sito vulnerabile in cui hello utente è già connesso. Esistono molti modi per toodo un utente malintenzionato che, ad esempio da un altro sito web di hosting che carica una risorsa dal server vulnerabile hello o recupero hello utente tooclick un collegamento. è possibile evitare l'attacco Hello se server hello invia un client toohello token aggiuntivi, è necessario hello client tooinclude token in tutte le richieste successive e verifica che tutte le richieste successive includono un token relativo toohello sessione corrente, ad esempio da utilizzo di ASP.NET AntiForgeryToken hello o ViewState. |

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) (Prevenzione delle richieste intersito false in ASP.NET MVC e nelle pagine Web ASP.NET) |
| **Passaggi** | Form di anti-CSRF e ASP.NET MVC - hello utilizzare `AntiForgeryToken` il metodo di supporto per le viste; put un `Html.AntiForgeryToken()` in formato hello, ad esempio,|

### <a name="example"></a>Esempio
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Esempio
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Esempio
In hello stesso tempo visitatore di hello Html.AntiForgeryToken() offre un cookie denominato __RequestVerificationToken, con lo stesso valore hello casuale nascosto sopra specificato hello. Toovalidate un post del form in ingresso, successivamente, aggiungere metodo di azione destinazione toohello filtro hello [ValidateAntiForgeryToken]. ad esempio:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro di autorizzazione che controlla che:
* richiesta in ingresso Hello dispone di un cookie denominato __RequestVerificationToken
* Hello richiesta in arrivo è un `Request.Form` voce denominata __RequestVerificationToken
* Questi cookie e `Request.Form` è ben corrispondono ai valori presupponendo che tutti, hello richiesta viene eseguita come di consueto. In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido". 

### <a name="example"></a>Esempio
AJAX and anti-CSRF: token del form hello può costituire un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare i dati JSON, non i dati di form HTML. Una soluzione è il token hello toosend in un'intestazione HTTP personalizzata. Hello codice seguente usa i token hello toogenerate di sintassi Razor e quindi aggiunge hello token tooan AJAX richiesta. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Esempio
Quando si elabora una richiesta di hello, estrarre il token hello dall'intestazione della richiesta di hello. Quindi chiamare il metodo AntiForgery.Validate hello token hello toovalidate. il metodo Validate Hello genera un'eccezione se i token hello non sono validi.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Take Advantage of ASP.NET predefinito Features tooFend Off Web attacchi](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Passaggi** | Attacchi CSRF nelle applicazioni Web Form di base possono essere contrastati impostando ViewStateUserKey tooa stringa casuale che varia per ogni utente - ID utente o, meglio ancora, ID di sessione. Per diversi motivi tecnici e legati ai social network, l'ID sessione è molto più appropriato perché non è prevedibile, scade ed è diverso per ogni utente.|

### <a name="example"></a>Esempio
Di seguito è riportato il codice di hello necessario toohave in tutte le pagine:
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Configurare una sessione per la durata dell'inattività

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Proprietà HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Passaggi** | Timeout della sessione rappresenta hello evento si verifica quando un utente non esegue nessuna azione in un sito web durante un intervallo (come definito dal server web). Salve, evento sul lato server, modificare lo stato di hello di hello utente sessione too'invalid' (ad esempio "non è più utilizzata") e indicherà hello web server toodestroy (l'eliminazione di tutti i dati contenuti al suo interno). Hello esempio di codice seguente imposta hello timeout sessione attributo too15 in minuti nel file Web. config hello.|

### <a name="example"></a>Esempio
```Codice XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Elemento forms per authentication (schema delle impostazioni ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Passaggi** | Impostare minuti hello too15 timeout di Ticket di autenticazione form cookie|

### <a name="example"></a>Esempio
```Codice XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Esempio
Anche hello ADFS rilasciato la durata del token SAML attestazione deve essere impostato too15 minuti, eseguendo il comando di powershell nel server ADFS hello seguente hello:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Implementa la disconnessione appropriata da un'applicazione hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Eseguire Disconnetti appropriato da un'applicazione hello, quando l'utente preme disconnettersi dal pulsante. Durante la disconnessione, l'applicazione deve eliminare definitivamente la sessione dell'utente e anche reimpostare e rendere null il valore del cookie della sessione, oltre a reimpostare e rendere null il valore del cookie di autenticazione. Inoltre, quando più sessioni tooa legati singola identità utente, si deve collettivamente terminare sul lato server hello timeout o disconnessione. Assicurarsi infine che la funzionalità di disconnessione sia disponibile in ogni pagina. |

## <a id="csrf-api"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Falsificazione della richiesta tra siti tra (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di sicurezza hello di sessione stabilita di un altro utente in un sito web. obiettivo di Hello è toomodify o eliminare il contenuto del sito web di destinazione hello si basa esclusivamente su richiesta ricevuta tooauthenticate i cookie di sessione. Un utente malintenzionato potrebbe sfruttare questa vulnerabilità tramite il recupero di un URL con un comando tooload browser di un utente diverso da un sito vulnerabile in cui hello utente è già connesso. Esistono molti modi per toodo un utente malintenzionato che, ad esempio da un altro sito web di hosting che carica una risorsa dal server vulnerabile hello o recupero hello utente tooclick un collegamento. è possibile evitare l'attacco Hello se server hello invia un client toohello token aggiuntivi, è necessario hello client tooinclude token in tutte le richieste successive e verifica che tutte le richieste successive includono un token relativo toohello sessione corrente, ad esempio da utilizzo di ASP.NET AntiForgeryToken hello o ViewState. |

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) (Prevenzione di attacchi basati su richieste intersito false nelle API Web ASP.NET) |
| **Passaggi** | AJAX and anti-CSRF: token del form hello può costituire un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare i dati JSON, non i dati di form HTML. Una soluzione è il token hello toosend in un'intestazione HTTP personalizzata. Hello codice seguente usa i token hello toogenerate di sintassi Razor e quindi aggiunge hello token tooan AJAX richiesta. |

### <a name="example"></a>Esempio
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Esempio
Quando si elabora una richiesta di hello, estrarre il token hello dall'intestazione della richiesta di hello. Quindi chiamare il metodo AntiForgery.Validate hello token hello toovalidate. il metodo Validate Hello genera un'eccezione se i token hello non sono validi.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Esempio
Anti-CSRF e form di ASP.NET MVC - hello di utilizzare il metodo helper AntiForgeryToken sulle viste; Inserire un Html.AntiForgeryToken() modulo hello, ad esempio,
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Esempio
esempio Hello precedente verrà restituito simile alla seguente hello:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Esempio
In hello stesso tempo visitatore di hello Html.AntiForgeryToken() offre un cookie denominato __RequestVerificationToken, con lo stesso valore hello casuale nascosto sopra specificato hello. Toovalidate un post del form in ingresso, successivamente, aggiungere metodo di azione destinazione toohello filtro hello [ValidateAntiForgeryToken]. ad esempio:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro di autorizzazione che controlla che:
* richiesta in ingresso Hello dispone di un cookie denominato __RequestVerificationToken
* Hello richiesta in arrivo è un `Request.Form` voce denominata __RequestVerificationToken
* Questi cookie e `Request.Form` è ben corrispondono ai valori presupponendo che tutti, hello richiesta viene eseguita come di consueto. In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido".

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | Provider di identità: AD FS, provider di identità: Azure AD |
| **Riferimenti**              | [Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) (Proteggere un'API Web con account singoli e account di accesso locale in API Web ASP.NET 2.2) |
| **Passaggi** | Se hello API Web è protetto tramite OAuth 2.0, quindi è previsto che un token di connessione nella richiesta dell'intestazione e concede l'accesso toohello richiesta di autorizzazione solo se il token hello è valido. A differenza dell'autenticazione basata su cookie, i browser non collegare toorequests i token di connessione hello. richiesta di Hello client deve tooexplicitly collegare il token di connessione hello nell'intestazione della richiesta hello. Per le API Web ASP.NET protette con OAuth 2.0, i token di connessione vengono quindi considerati una difesa contro gli attacchi basati su richieste intersito false. Si noti che se un'applicazione hello parte MVC hello utilizza l'autenticazione basata su form (ad esempio, utilizza cookie), i token antifalsificazione toobe usato dall'app web MVC di hello. |

### <a name="example"></a>Esempio
API Web Hello è toobe informati toorely solo i token di connessione e non su cookie. Può essere eseguita da hello seguente configurazione in `WebApiConfig.Register` metodo: ' ' configurazione di codice C#. SuppressDefaultHostAuthentication(); configurazione. Filters. Add (nuovo HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
