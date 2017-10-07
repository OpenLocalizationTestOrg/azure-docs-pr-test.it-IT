---
title: risorse modello di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui tipi di hello delle risorse disponibili per l'utilizzo nei modelli di portale per sviluppatori in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Risorse del modello Gestione API di Azure
Gestione API di Azure fornisce i seguenti tipi di risorse da utilizzare nei modelli del portale per sviluppatori di hello hello.  
  
-   [Risorse di tipo stringa](#strings)  
  
-   [Risorse di tipo glifo](#glyphs)  
  
##  <a name="strings"></a> Risorse di tipo stringa  
 Gestione API fornisce un set completo di stringhe di risorse da utilizzare nel portale per sviluppatori hello. Queste risorse sono localizzate in tutte le lingue hello supportate dall'API di gestione. set predefinito di Hello dei modelli utilizza le risorse per le intestazioni di pagina, etichette e le stringhe costanti che vengono visualizzate nel portale per sviluppatori hello. toouse una risorsa stringa nei modelli di fornire hello risorse stringa prefisso seguita dal nome di stringa hello, come illustrato nell'esempio seguente hello.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Hello riportato è dal modello di elenco prodotto hello e Visualizza **prodotti** nella parte superiore di hello della pagina hello.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Vedere le tabelle per le risorse stringa hello disponibili per l'utilizzo dei modelli del portale per sviluppatori seguenti toohello. Utilizzare il nome di tabella hello prefisso hello per le risorse stringa hello in tale tabella.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentazione](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|Nome|Text|  
|----------|----------|  
|PageTitleApis|API|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|Nome|Text|  
|----------|----------|  
|WebApplicationsDetailsTitle|Application preview (Anteprima dell'applicazione)|  
|WebApplicationsRequirementsHeader|Requisiti|  
|WebApplicationsScreenshotAlt|Schermata|  
|WebApplicationsScreenshotsHeader|Screenshots (Schermate)|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|Nome|Text|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Sono certi di voler tooremove applicazione?|  
|WebDevelopersAppNotPublished|Not published (Non pubblicata)|  
|WebDevelopersAppNotSubminted|Not submitted (Non inviata)|  
|WebDevelopersAppTableCategoryHeader|Categoria|  
|WebDevelopersAppTableNameHeader|Nome|  
|WebDevelopersAppTableStateHeader|Stato|  
|WebDevelopersEditLink|Modificare|  
|WebDevelopersRegisterAppLink|Registrare l'applicazione|  
|WebDevelopersRemoveLink|Rimuovere|  
|WebDevelopersSubmitLink|Submit|  
|WebDevelopersYourApplicationsHeader|Applicazioni|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|Nome|Text|  
|----------|----------|  
|WebApplicationsHeader|Applicazioni|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|Nome|Text|  
|----------|----------|  
|NoItemsToDisplay|No results found. (Nessun risultato trovato.)|  
|GeneralExceptionMessage|Something is not right. (Si è verificato un problema.) It could be a temporary glitch or a bug. (Potrebbe trattarsi di un problema temporaneo o di un bug.) Please, try again. (Riprovare.)|  
|GeneralJsonExceptionMessage|Something is not right. (Si è verificato un problema.) It could be a temporary glitch or a bug. (Potrebbe trattarsi di un problema temporaneo o di un bug.) ., Ricaricare la pagina hello e riprovare.|  
|ConfirmationMessageUnsavedChanges|There are some unsaved changes. (Sono presenti modifiche non salvate.) Si certi desiderato toocancel e annullare le modifiche di hello?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|Http Request Body too large. (Corpo della richiesta HTTP troppo grande.)|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|Nome|Text|  
|----------|----------|  
|ButtonLabelCancel|Annulla|  
|ButtonLabelSave|Salva|  
|GeneralExceptionMessage|Something is not right. (Si è verificato un problema.) It could be a temporary glitch or a bug. (Potrebbe trattarsi di un problema temporaneo o di un bug.) Please, try again. (Riprovare.)|  
|NoItemsToDisplay|Non esistono alcun toodisplay elementi.|  
|PagerButtonLabelFirst|First (Primo)|  
|PagerButtonLabelLast|Last (Ultimo)|  
|PagerButtonLabelNext|Avanti|  
|PagerButtonLabelPrevious|Prev (Precedente)|  
|PagerLabelPageNOfM|Page {0} of {1} (Pagina {0} di {1})|  
|PasswordTooShort|Hello Password è troppo breve|  
|EmailAsPassword|Do not use your email as your password (La password non può contenere l'indirizzo di posta elettronica)|  
|PasswordSameAsUserName|Your password cannot contain your username (La password non può contenere il nome utente)|  
|PasswordTwoCharacterClasses|Use different character classes (Usare classi di caratteri differenti)|  
|PasswordTooManyRepetitions|Too many repetitions (Troppe ripetizioni)|  
|PasswordSequenceFound|Your password contains sequences (La password contiene sequenze)|  
|PagerLabelPageSize|Page size (Dimensione della pagina)|  
|CurtainLabelLoading|Loading... (Caricamento in corso...)|  
|TablePlaceholderNothingToDisplay|Non sono presenti dati per l'ambito e il periodo di hello selezionato|  
|ButtonLabelClose|Chiudi|  
  
###  <a name="Documentation"></a> Documentazione  
  
|Nome|Text|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Invalid header '{0}' (Intestazione '{0}' non valida)|  
|WebDocumentationInvalidRequestErrorMessage|Invalid Request URL (URL della richiesta non valido)|  
|TextboxLabelAccessToken|Token di accesso *|  
|DropdownOptionPrimaryKeyFormat|Primary-{0} ({0}-primario)|  
|DropdownOptionSecondaryKeyFormat|Secondary-{0} (Secondario-{0})|  
|WebDocumentationSubscriptionKeyText|Your subscription key (Chiave della sottoscrizione)|  
|WebDocumentationTemplatesAddHeaders|Add required HTTP headers (Aggiungere intestazioni HTTP obbligatorie)|  
|WebDocumentationTemplatesBasicAuthSample|Basic Authorization Sample (Esempio di autorizzazione di base)|  
|WebDocumentationTemplatesCurlForBasicAuth|for Basic Authorization use: --user {username}:{password} (per l'utilizzo dell'autorizzazione di base:--user {nomeutente}: {password})|  
|WebDocumentationTemplatesCurlValuesForPath|Specify values for path parameters (shown as {...}), your subscription key and values for query parameters (Specificare i valori dei parametri del percorso (mostrati come {…}), la chiave di sottoscrizione e i valori dei parametri di query)|  
|WebDocumentationTemplatesDeveloperKey|Specify your subscription key (Specificare la chiave della sottoscrizione)|  
|WebDocumentationTemplatesJavaApache|In questo esempio utilizza i client di Apache HTTP hello dai componenti HTTP (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Specify values for optional parameters, as needed (Specificare i valori per i parametri facoltativi in base alle esigenze)|  
|WebDocumentationTemplatesPhpPackage|Questo esempio utilizza i pacchetti hello HTTP_Request2. (for more information: http://pear.php.net/package/HTTP_Request2) ((per altre informazioni: http://pear.php.net/package/HTTP_Request2))|  
|WebDocumentationTemplatesPythonValuesForPath|Specify values for path parameters (shown as {...}) and request body if needed (Specificare i valori dei parametri del percorso (mostrati come {…}) e il corpo della richiesta se necessario)|  
|WebDocumentationTemplatesRequestBody|Specify request body (Specificare il corpo della richiesta)|  
|WebDocumentationTemplatesRequiredParams|Specificare i valori per i seguenti parametri obbligatori hello|  
|WebDocumentationTemplatesValuesForPath|Specify values for path parameters (shown as {...}) (Specificare i valori dei parametri del percorso (mostrati come {…}))|  
|OAuth2AuthorizationEndpointDescription|endpoint di autorizzazione Hello viene utilizzato toointeract con proprietario della risorsa hello e ottenere una concessione di autorizzazione.|  
|OAuth2AuthorizationEndpointName|Authorization endpoint (Endpoint di autorizzazione)|  
|OAuth2TokenEndpointDescription|endpoint token Hello viene utilizzato per hello client tooobtain un token di accesso presentando l'autorizzazione concede l'autorizzazione o token di aggiornamento.|  
|OAuth2TokenEndpointName|Token endpoint (Endpoint di token)|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> hello client avvia il flusso di hello indirizzando endpoint di autorizzazione toohello agente utente del proprietario della risorsa hello.  Hello client include il relativo identificatore client, l'ambito richiesto, lo stato locale e un server di autorizzazione hello toowhich URI di reindirizzamento invierà agente utente hello nuovamente una volta completato l'accesso concesso (o negato).     </p\> < p\> server autorizzazione hello autentica proprietario della risorsa hello (tramite hello dell'agente utente) e stabilisce se proprietario della risorsa hello concede o Nega la richiesta di accesso del client hello.     </p\> < p\> supponendo che il proprietario della risorsa hello concede l'accesso, il server di autorizzazione hello reindirizza hello agente utente toohello nascosto mediante il reindirizzamento hello URI fornito precedenti (richiesta hello o durante ai clien registrazione di t).  URI di reindirizzamento Hello include un codice di autorizzazione e qualsiasi stato locale fornito dal client hello in precedenza.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> se l'utente hello Nega la richiesta di accesso hello di se hello richiesta non è valida, verrà indicato client hello utilizzando i seguenti parametri aggiunti nel reindirizzamento toohello hello: </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Authorization request (Richiesta di autorizzazione)|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello client app deve inviare l'endpoint di autorizzazione toohello utente hello in hello tooinitiate ordine processo OAuth.          Endpoint di autorizzazione hello, utente hello autentica e quindi concede o nega l'accesso toohello app.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> supponendo che il proprietario della risorsa hello concede l'accesso, server di autorizzazione reindirizza hello agente utente toohello nascosto mediante il reindirizzamento hello URI fornito precedenti (nella richiesta di hello o durante la registrazione del client).  URI di reindirizzamento Hello include un codice di autorizzazione e qualsiasi stato locale fornito dal client hello in precedenza. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> client hello richiede un token di accesso dal server di autorizzazione hello ' endpoint del token s includendo il codice di autorizzazione hello ottenuto nel passaggio precedente hello.  Quando si effettua la richiesta di hello, hello client esegue l'autenticazione con il server di autorizzazione hello.  client di Hello include hello reindirizzamento URI utilizzato tooobtain hello autorizzazione codice per la verifica. </p\> < p\> server autorizzazione hello hello client viene autenticato, convalida il codice di autorizzazione hello e garantisce che il reindirizzamento hello URI ricevute corrispondenze hello URI utilizzato tooredirect hello client nel passaggio (C).  Se è valido, il server di autorizzazione hello risponde con un token di accesso e, facoltativamente, un token di aggiornamento. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> se l'autenticazione del client richiesta hello non riuscito o non è valido, il server di autorizzazione hello risponde con un codice di stato HTTP 400 (Bad Request) (se non diversamente specificato) e include i seguenti parametri con risposta hello hello. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> client hello rende un endpoint del token toohello richiesta inviando hello seguenti parametri con hello "application/x-www-form-urlencoded" formato di codifica dei caratteri UTF-8 in hello HTTP richiesta corpo entità. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> server autorizzazione hello emette un token di accesso e un token di aggiornamento facoltativo e costrutti hello risposta aggiungendo hello seguenti parametri toohello corpo entità della risposta HTTP hello con un codice di 200 stato (OK). </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello autentica con il server di autorizzazione hello e richiede un token di accesso dall'endpoint token hello. </p\> < p\> hello client viene autenticato, il server di autorizzazione hello e se valido, genera un token di accesso. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> se richiesta hello client autenticazione non riuscita o non è valido il server di autorizzazione hello risponde con un codice di stato HTTP 400 (Bad Request) (se non diversamente specificato) e include i seguenti parametri con risposta hello hello. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> client hello rende un endpoint del token toohello richiesta aggiungendo hello seguenti parametri con hello "application/x-www-form-urlencoded" formato di codifica dei caratteri UTF-8 in hello HTTP richiesta corpo entità. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> se richiesta di token di accesso di hello è validi e autorizzati, il server di autorizzazione hello emette un token di accesso e un token di aggiornamento facoltativo e costrutti hello risposta aggiungendo hello seguenti parametri toohello corpo entità di hello HTTP risposta con un codice di 200 stato (OK). </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> hello client avvia il flusso di hello indirizzando proprietario della risorsa hello ' endpoint di autorizzazione toohello s agente utente.  Hello client include il relativo identificatore client, l'ambito richiesto, lo stato locale e un server di autorizzazione hello toowhich URI di reindirizzamento invierà agente utente hello nuovamente una volta completato l'accesso concesso (o negato). </p\> < p\> server autorizzazione hello autentica proprietario della risorsa hello (tramite hello dell'agente utente) e stabilisce se proprietario della risorsa hello concede o Nega client hello "richiesta di accesso s. </p\> < p\> supponendo che il proprietario della risorsa hello concede l'accesso, il server di autorizzazione hello reindirizza hello agente utente toohello nascosto mediante il reindirizzamento di hello URI fornito in precedenza.  URI di reindirizzamento Hello include il token di accesso di hello nel frammento dell'URI hello. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> se proprietario della risorsa hello rifiuta la richiesta di accesso di hello o se la richiesta hello non riesce per motivi diversi da un URI di reindirizzamento mancante o non valido, il server di autorizzazione hello informa client hello aggiungendo i seguenti parametri toohello fragme hello componente di NT di URI di reindirizzamento hello utilizzando hello formato "application/x-www-form-urlencoded". </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello client app deve inviare l'endpoint di autorizzazione toohello utente hello in hello tooinitiate ordine processo OAuth.      Endpoint di autorizzazione hello, utente hello autentica e quindi concede o nega l'accesso toohello app. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> se il proprietario della risorsa hello concede la richiesta di accesso hello, server di autorizzazione hello emette un token di accesso e li recapita client toohello aggiungendo hello seguente componente frammento toohello di parametri dell'URI di reindirizzamento hello utilizzando hello "a applicativi/x-www-form-urlencoded"formato. </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Flusso del codice di autorizzazione è ottimizzato per i client in grado di mantenere la riservatezza hello delle loro credenziali (ad esempio, server applicazioni web implementate utilizzando PHP, Java, Python, Ruby, ASP.NET, ecc.).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Authorization Code grant (Concessione del codice di autorizzazione)|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Flusso di credenziali client è adatto nei casi in cui il client di hello (applicazione) richiede accesso alle risorse protetta toohello sotto il controllo. client Hello viene considerato come un proprietario della risorsa, pertanto non è richiesta alcuna interazione dell'utente finale.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Client Credentials grant (Concessione delle credenziali client)|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Flusso implicito è ottimizzato per i client in grado di mantenere la riservatezza hello dei loro toooperate noti credenziali un particolare URI di reindirizzamento. These clients are typically implemented in a browser using a scripting language such as JavaScript. (Questi client sono generalmente implementati in un browser usando un linguaggio di scripting come JavaScript.)|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Implicit grant (Concessione implicita)|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Flusso di credenziali di password proprietario risorsa è appropriato nei casi in cui proprietario della risorsa hello ha una relazione di trust con il client di hello (applicazione), ad esempio sistema operativo del dispositivo hello o un'applicazione con privilegi elevati. Questo flusso è adatto per i client in grado di ottenere le credenziali del proprietario della risorsa hello (nome utente e password, in genere tramite un modulo interattivo).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Resource Owner Password Credentials grant (Concessione delle credenziali di tipo password del proprietario delle risorse)|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> proprietario della risorsa hello fornisce hello client il nome utente e la password. </p\> < p\> client hello richiede un token di accesso dal server di autorizzazione hello ' endpoint del token s includendo le credenziali di hello ricevute dal proprietario della risorsa hello.  Quando si effettua la richiesta di hello, hello client esegue l'autenticazione con il server di autorizzazione hello. </p\> < p\> server autorizzazione hello hello client viene autenticato e convalida delle credenziali del proprietario risorsa hello e se valido, genera un token di accesso. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> se richiesta hello client autenticazione non riuscita o non è valido il server di autorizzazione hello risponde con un codice di stato HTTP 400 (Bad Request) (se non diversamente specificato) e include i seguenti parametri con risposta hello hello. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> client hello rende un endpoint del token toohello richiesta aggiungendo hello seguenti parametri con hello "application/x-www-form-urlencoded" formato di codifica dei caratteri UTF-8 in hello HTTP richiesta corpo entità. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> se richiesta di token di accesso di hello è validi e autorizzati, il server di autorizzazione hello emette un token di accesso e un token di aggiornamento facoltativo e costrutti hello risposta aggiungendo i seguenti parametri toohello corpo entità di hello HTTP reseller hello nSe con un codice di 200 stato (OK). </p\>|  
|OAuth2Step_AccessTokenRequest_Name|Access token request (Richiesta di token di accesso)|  
|OAuth2Step_AuthorizationRequest_Name|Authorization request (Richiesta di autorizzazione)|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|OBBLIGATORIO. token di accesso Hello rilasciato dal server di autorizzazione hello.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|OBBLIGATORIO. token di accesso Hello rilasciato dal server di autorizzazione hello.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|OBBLIGATORIO. token di accesso Hello rilasciato dal server di autorizzazione hello.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBBLIGATORIO. token di accesso Hello rilasciato dal server di autorizzazione hello.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|OBBLIGATORIO. Client identifier. (Identificatore cliente.)|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|NECESSARIA se il client di hello non esegue l'autenticazione con il server di autorizzazione hello.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|OBBLIGATORIO. Identificatore Hello del client.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|OBBLIGATORIO. codice di autorizzazione Hello generato dal server di autorizzazione hello.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|OBBLIGATORIO. codice di autorizzazione Hello ricevuto dal server di autorizzazione hello.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|FACOLTATIVO. Human-readable ASCII text providing additional information. (Testo ASCII leggibile dall'utente che fornisce informazioni aggiuntive.)|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|FACOLTATIVO. Human-readable ASCII text providing additional information. (Testo ASCII leggibile dall'utente che fornisce informazioni aggiuntive.)|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|FACOLTATIVO. Human-readable ASCII text providing additional information. (Testo ASCII leggibile dall'utente che fornisce informazioni aggiuntive.)|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|FACOLTATIVO. Human-readable ASCII text providing additional information. (Testo ASCII leggibile dall'utente che fornisce informazioni aggiuntive.)|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|FACOLTATIVO. Human-readable ASCII text providing additional information. (Testo ASCII leggibile dall'utente che fornisce informazioni aggiuntive.)|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|FACOLTATIVO. URI che identifica una pagina web leggibile con le informazioni sull'errore hello.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|FACOLTATIVO. URI che identifica una pagina web leggibile con le informazioni sull'errore hello.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|FACOLTATIVO. URI che identifica una pagina web leggibile con le informazioni sull'errore hello.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|FACOLTATIVO. URI che identifica una pagina web leggibile con le informazioni sull'errore hello.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|FACOLTATIVO. URI che identifica una pagina web leggibile con le informazioni sull'errore hello.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|OBBLIGATORIO. Un singolo codice di errore ASCII dal successivo hello: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|OBBLIGATORIO. Un singolo codice di errore ASCII dal successivo hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|OBBLIGATORIO. Un singolo codice di errore ASCII dal successivo hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|OBBLIGATORIO. Un singolo codice di errore ASCII dal successivo hello: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OBBLIGATORIO. Un singolo codice di errore ASCII dal successivo hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|CONSIGLIATO. durata Hello in secondi del token di accesso hello.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|CONSIGLIATO. durata Hello in secondi del token di accesso hello.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|CONSIGLIATO. durata Hello in secondi del token di accesso hello.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|CONSIGLIATO. durata Hello in secondi del token di accesso hello.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|OBBLIGATORIO. Valore deve essere impostato troppo "authorization_code".|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|OBBLIGATORIO. Valore deve essere impostato troppo "client_credentials".|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBBLIGATORIO. Valore deve essere impostato troppo "password".|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBBLIGATORIO. password del proprietario risorsa Hello.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|FACOLTATIVO. URI dell'endpoint Hello reindirizzamento deve essere un URI assoluto.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|OBBLIGATORIO se il parametro "redirect_uri" hello è stato incluso nella richiesta di autorizzazione hello e i relativi valori devono essere identici.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|FACOLTATIVO. URI dell'endpoint Hello reindirizzamento deve essere un URI assoluto.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|FACOLTATIVO. token di aggiornamento Hello, che può essere utilizzato tooobtain nuovi token di accesso.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|FACOLTATIVO. token di aggiornamento Hello, che può essere utilizzato tooobtain nuovi token di accesso.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|FACOLTATIVO. token di aggiornamento Hello, che può essere utilizzato tooobtain nuovi token di accesso.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|OBBLIGATORIO. Valore deve essere impostato troppo "code".|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|OBBLIGATORIO. Valore deve essere impostato troppo "token".|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|FACOLTATIVO. ambito Hello della richiesta di accesso hello.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|FACOLTATIVO se toohello identici ambito richiesto dal client hello. in caso contrario, è necessario.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|FACOLTATIVO. ambito Hello della richiesta di accesso hello.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|Ambito toohello facoltativo, se sono identici, richiesto da client hello; in caso contrario, è necessario.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|FACOLTATIVO. ambito Hello della richiesta di accesso hello.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|FACOLTATIVO se toohello identici ambito richiesto dal client hello. in caso contrario, è necessario.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|FACOLTATIVO. ambito Hello della richiesta di accesso hello.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Ambito toohello facoltativo, se sono identici, richiesto da client hello; in caso contrario, è necessario.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|NECESSARIA se il parametro "state" hello è presente nella richiesta di autorizzazione hello del client.  Hello il valore esatto ricevuto da hello client.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|CONSIGLIATO. Un valore opaco utilizzato da uno stato di hello client toomaintain tra hello richiesta e il callback.  server di autorizzazione Hello include questo valore quando si reindirizzano client toohello indietro di hello agente utente.  parametro Hello deve essere utilizzato per impedire richieste intersito false.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|NECESSARIA se il parametro "state" hello è presente nella richiesta di autorizzazione hello del client.  Hello il valore esatto ricevuto da hello client.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|NECESSARIA se il parametro "state" hello è presente nella richiesta di autorizzazione hello del client.  Hello il valore esatto ricevuto da hello client.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|CONSIGLIATO. Un valore opaco utilizzato da uno stato di hello client toomaintain tra hello richiesta e il callback.  server di autorizzazione Hello include questo valore quando si reindirizzano client toohello indietro di hello agente utente.  parametro Hello deve essere utilizzato per impedire richieste intersito false.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|NECESSARIA se il parametro "state" hello è presente nella richiesta di autorizzazione hello del client.  Hello il valore esatto ricevuto da hello client.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|OBBLIGATORIO. tipo di Hello di hello token rilasciato.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|OBBLIGATORIO. tipo di Hello di hello token rilasciato.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|OBBLIGATORIO. tipo di Hello di hello token rilasciato.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBBLIGATORIO. tipo di Hello di hello token rilasciato.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBBLIGATORIO. nome utente del proprietario risorsa Hello.|  
|OAuth2UnsupportedTokenType|Token type '{0}' is not supporetd. (Il tipo di token "{0}" non è supportato.)|  
|OAuth2InvalidState|Invalid response from authorization server (Risposta non valida dal server di autorizzazione)|  
|OAuth2GrantType_AuthorizationCode|Authorization code (Codice di autorizzazione)|  
|OAuth2GrantType_Implicit|Implicit (Implicita)|  
|OAuth2GrantType_ClientCredentials|Credenziali del client|  
|OAuth2GrantType_ResourceOwnerPassword|Resource owner password. (Password del proprietario delle risorse.)|  
|WebDocumentation302Code|302 - Trovato|  
|WebDocumentation400Code|400 - Richiesta non valida|  
|OAuth2SendingMethod_AuthHeader|Authorization header (Intestazione dell'autorizzazione)|  
|OAuth2SendingMethod_QueryParam|Query parameter (Parametro di query)|  
|OAuth2AuthorizationServerGeneralException|An error has occurred while authorizing access via {0} (Si è verificato un errore durante l'autorizzazione all'accesso tramite {0})|  
|OAuth2AuthorizationServerCommunicationException|Non è stato possibile stabilire un server di tooauthorization connessione HTTP o è stato chiuso in modo imprevisto.|  
|WebDocumentationOAuth2GeneralErrorMessage|Errore imprevisto.|  
|AuthorizationServerCommunicationException|Authorization server communication exception has happened. (Si è verificata un'eccezione di comunicazione con il server di autorizzazione.) Contattare l'amministratore.|  
|TextblockSubscriptionKeyHeaderDescription|Chiave di sottoscrizione che fornisce accesso toothis API. Si trova in <a href='/developer'\>Profilo</a\>.|  
|TextblockOAuthHeaderDescription|OAuth 2.0 access token obtained from <i\>{0}</i\>. (Token di accesso OAuth 2.0 ottenuto da <> </> \>{0}\>.) Supported grant types: <i\>{1}</i\>. (Tipi di concessione supportati: <i\>{1}</i\>.)|  
|TextblockContentTypeHeaderDescription|Tipo di supporto del corpo di hello inviato toohello API.|  
|ErrorMessageApiNotAccessible|Hello API che si sta tentando di toocall non è accessibile in questo momento. Contattare il server di pubblicazione di API hello < un href = "/ Rilascia"\>qui < /a\>.|  
|ErrorMessageApiTimedout|Hello API che si sta tentando di toocall richiede più di risposta normale tooget nuovamente. Contattare il server di pubblicazione di API hello < un href = "/ Rilascia"\>qui < /a\>.|  
|BadRequestParameterExpected|"'{0}' parameter is expected" ("È previsto il parametro '{0}'")|  
|TooltipTextDoubleClickToSelectAll|Fare doppio clic tooselect tutti.|  
|TooltipTextHideRevealSecret|Mostra/Nascondi|  
|ButtonLinkOpenConsole|Prova|  
|SectionHeadingRequestBody|Corpo della richiesta|  
|SectionHeadingRequestParameters|Parametri della richiesta|  
|SectionHeadingRequestUrl|URL richiesta|  
|SectionHeadingResponse|Response|  
|SectionHeadingRequestHeaders|Intestazioni della richiesta|  
|FormLabelSubtextOptional|Facoltativo|  
|SectionHeadingCodeSamples|Esempi di codice|  
|TextblockOpenidConnectHeaderDescription|OpenID Connect id token obtained from <i\>{0}</i\>. (Token ID di OpenID Connect ottenuto da <i\>{0}</i\>.) Supported grant types: <i\>{1}</i\>. (Tipi di concessione supportati: <i\>{1}</i\>.)|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|Nome|Text|  
|----------|----------|  
|LinkLabelBack|Indietro|  
|LinkLabelHomePage|home page|  
|LinkLabelSendUsEmail|Inviare un messaggio di posta elettronica|  
|PageTitleError|Si è verificato una pagina di richiesta di problema servono hello|  
|TextblockPotentialCauseIntermittentIssue|This may be an intermittent data access issue that is already gone. (Potrebbe trattarsi di un problema di accesso intermittente ai dati ora non presente.)|  
|TextblockPotentialCauseOldLink|non hai fatto clic sul collegamento di Hello sia precedente e non punto toohello correzione percorso più.|  
|TextblockPotentialCauseTechnicalProblem|There may be a technical problem on our end. (Potenziale problema tecnico.)|  
|TextblockPotentialSolutionRefresh|Provare ad aggiornare la pagina hello.|  
|TextblockPotentialSolutionStartOver|Start over from our {0}. (Ricominciare dal nostro {0}.)|  
|TextblockPotentialSolutionTryAgain|Andare a {0} e ripetere l'azione hello che nuovamente eseguito.|  
|TextReportProblem|{0} describing what went wrong and we will look at it as soon as we can. ({0} descrivendo l'errore; verrà esaminato non appena possibile.)|  
|TitlePotentialCause|Potential cause (Causa potenziale)|  
|TitlePotentialSolution|Probabilmente è semplicemente un problema temporaneo, alcuni aspetti tootry|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|Nome|Text|  
|----------|----------|  
|WebIssuesIndexTitle|Problemi|  
|WebIssuesNoActiveSubscriptions|Non si dispone di sottoscrizioni attive. È necessario toosubscribe per tooreport un prodotto un problema.|  
|WebIssuesNotSignin|You're not signed in. (Non è stato eseguito l'accesso.) Eseguire {0} tooreport un problema o inserire un commento.|  
|WebIssuesReportIssueButton|Report Issue (Segnala un problema)|  
|WebIssuesSignIn|sign in|  
|WebIssuesStatusReportedBy|Status: {0} &#124; Reported by {1} (Stato: {0} &#124; Segnalato da {1})|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|Nome|Text|  
|----------|----------|  
|LinkLabelHomePage|home page|  
|LinkLabelSendUsEmail|Inviare un messaggio di posta elettronica|  
|PageTitleNotFound|Impossibile trovare hello pagina desiderata|  
|TextblockPotentialCauseMisspelledUrl|Si è errato hello URL se è stato digitato.|  
|TextblockPotentialCauseOldLink|non hai fatto clic sul collegamento di Hello sia precedente e non punto toohello correzione percorso più.|  
|TextblockPotentialSolutionRetype|Provare a ridigitare hello URL.|  
|TextblockPotentialSolutionStartOver|Start over from our {0}. (Ricominciare dal nostro {0}.)|  
|TextReportProblem|{0} describing what went wrong and we will look at it as soon as we can. ({0} descrivendo l'errore; verrà esaminato non appena possibile.)|  
|TitlePotentialCause|Potential cause (Causa potenziale)|  
|TitlePotentialSolution|Potential solution (Potenziale soluzione)|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|Nome|Text|  
|----------|----------|  
|WebProductsAgreement|Sottoscrivendo troppo {0} prodotto, accetto toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Condizioni per l'utilizzo|  
|WebProductsSubscribeButton|Sottoscrivi|  
|WebProductsUsageLimitsHeader|Limiti di consumo|  
|WebProductsYouAreNotSubscribed|Si è sottoscritto toothis prodotto.|  
|WebProductsYouRequestedSubscription|È richiesta prodotto toothis di sottoscrizione.|  
|ErrorYouNeedtoAgreeWithLegalTerms|È necessario accettare le condizioni di utilizzo toohello prima di procedere.|  
|ButtonLabelAddSubscription|Aggiungi sottoscrizione|  
|LinkLabelChangeSubscriptionName|change (modifica)|  
|ButtonLabelConfirm|Confirm|  
|TextblockMultipleSubscriptionsCount|Si dispone di {0} sottoscrizioni toothis prodotto:|  
|TextblockSingleSubscriptionsCount|Si dispone di {0} sottoscrizione toothis prodotto:|  
|TextblockSingleApisCount|This product contains {0} API: (Questo prodotto contiene {0} API:)|  
|TextblockMultipleApisCount|This product contains {0} APIs: (Questo prodotto contiene {0} API:)|  
|TextblockHeaderSubscribe|La sottoscrizione tooproduct|  
|TextblockSubscriptionDescription|A new subscription will be created as follows: (Verrà creata la nuova sottoscrizione indicata di seguito:)|  
|TextblockSubscriptionLimitReached|Subscriptions limit reached. (È stato raggiunto il limite di sottoscrizioni.)|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|Nome|Text|  
|----------|----------|  
|PageTitleProducts|Prodotti|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|Nome|Text|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Accedi sono disabilitata per gli amministratori di hello un determinato momento hello.|  
|TextboxExternalIdentitiesSigninInvitation|Alternatively, sign in with (In alternativa, accedere con)|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Sign in with: (Accedere con:)|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|Nome|Text|  
|----------|----------|  
|PrincipalNotFound|Principal is not found or signature is invalid (Entità non trovata o firma non valida)|  
|ErrorSsoAuthenticationFailed|SSO authentication failed (Autenticazione SSO non riuscita)|  
|ErrorSsoAuthenticationFailedDetailed|Invalid token provided or signature cannot be verified. (È stato fornito un token non valido oppure è impossibile verificare la firma.)|  
|ErrorSsoTokenInvalid|SSO token is invalid (Token SSO non valido.)|  
|ValidationErrorSpecificEmailAlreadyExists|Email '{0}' already registered (L'indirizzo di posta elettronica '{0}' è già registrato)|  
|ValidationErrorSpecificEmailInvalid|Email '{0}' is invalid (L'indirizzo di posta elettronica '{0}' non è valido)|  
|ValidationErrorPasswordInvalid|Password non valida. . Correggere gli errori di hello e riprovare.|  
|PropertyTooShort|{0} is too short ({0} è troppo breve)|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Indirizzo di posta elettronica non valido.|  
|ValidationMessageNewPasswordConfirmationRequired|Conferma nuova password|  
|ValidationErrorPasswordConfirmationRequired|Confirm password is empty (La password di conferma è vuota)|  
|WebAuthenticationEmailChangeNotice|Il messaggio di conferma modifica verrà troppo hello {0}. Seguire le istruzioni all'interno di esso tooconfirm il nuovo indirizzo di posta elettronica. Se la posta elettronica hello arrivano posta in arrivo tooyour in hello Avanti alcuni minuti, controllare la cartella posta indesiderata.|  
|WebAuthenticationEmailChangeNoticeHeader|Your email change request was successfully processed (La richiesta di modifica dell'indirizzo di posta elettronica è stata elaborata)|  
|WebAuthenticationEmailChangeNoticeTitle|Email change requested (Modifica dell'indirizzo di posta elettronica richiesta)|  
|WebAuthenticationEmailHasBeenRevertedNotice|You email already exist. (Indirizzo di posta elettronica già esistente.) Request has been reverted (La richiesta è stata ripristinata)|  
|ValidationErrorEmailAlreadyExists|Email already exist. (Indirizzo di posta elettronica già esistente)|  
|ValidationErrorEmailInvalid|Invalid e-mail address (Indirizzo di posta elettronica non valido)|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|L'indirizzo di posta elettronica è obbligatorio.|  
|WebAuthenticationErrorNoticeHeader|Errore|  
|WebAuthenticationFieldLengthErrorMessage|{0} must be a maximum length of {1} ({0} deve avere una lunghezza massima di {1})|  
|TextboxLabelEmailFirstName|Nome|  
|ValidationErrorFirstNameRequired|First name is required. (Un nome è obbligatorio.)|  
|ValidationErrorFirstNameInvalid|Invalid first name (Nome non valido)|  
|NoticeInvalidInvitationToken|Please note that confirmation links are valid for only 48 hours. (I collegamenti di conferma sono validi solo per 48 ore.) If you are still within this timeframe, please make sure your link is correct. (Se si è ancora entro questo intervallo di tempo, verificare che il collegamento sia corretto.) Se il collegamento è scaduto, ripetere azione hello che stai tentando tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Invalid invitation token (Token di invito non valido)|  
|NoticeTitleInvalidInvitationToken|Confirmation error (Errore di conferma)|  
|WebAuthenticationLastNameInvalidErrorMessage|Cognome non valido|  
|TextboxLabelEmailLastName|Cognome|  
|ValidationErrorLastNameRequired|Il cognome è obbligatorio.|  
|WebAuthenticationLinkExpiredNotice|Collegamento di conferma inviato tooyou è scaduto. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Your password reset link is invalid or expired. (Il collegamento per il ripristino della password non è valido o è scaduto).|  
|WebAuthenticationLinkExpiredNoticeTitle|Link sent (Collegamento inviato)|  
|WebAuthenticationNewPasswordLabel|Nuova password|  
|ValidationMessageNewPasswordRequired|New password is required. (La nuova password è obbligatoria.)|  
|TextboxLabelNotificationsSenderEmail|Notifications sender email (Indirizzo di posta elettronica del mittente delle notifiche)|  
|TextboxLabelOrganizationName|Nome organizzazione|  
|WebAuthenticationOrganizationRequiredErrorMessage|Organization name is empty (Il nome dell'organizzazione è vuoto)|  
|WebAuthenticationPasswordChangedNotice|Your password was successfully updated (Aggiornamento della password completato)|  
|WebAuthenticationPasswordChangedNoticeTitle|Password aggiornata|  
|WebAuthenticationPasswordCompareErrorMessage|Passwords don't match (Le password non corrispondono)|  
|WebAuthenticationPasswordConfirmLabel|Conferma password|  
|ValidationErrorPasswordInvalidDetailed|Password is too weak. (La password è troppo debole.)|  
|WebAuthenticationPasswordLabel|Password|  
|ValidationErrorPasswordRequired|Password is required. (La password è obbligatoria.)|  
|WebAuthenticationPasswordResetSendNotice|Posta elettronica di conferma di modifica password è troppo hello {0}. Seguire le istruzioni di hello all'interno di hello toocontinue di posta elettronica il processo di modifica della password.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Your passowrd change request was successfully processed (La richiesta di modifica della password è stata elaborata)|  
|WebAuthenticationPasswordResetSendNoticeTitle|Password reset requested (Reimpostazione password richiesta)|  
|WebAuthenticationRequestNotFoundNotice|Request not found (Richiesta non trovata)|  
|WebAuthenticationSenderEmailRequiredErrorMessage|Notifications sender email is empty (L'indirizzo di posta elettronica del mittente delle notifiche è vuoto)|  
|WebAuthenticationSigninPasswordLabel|Confermare la modifica hello immettendo una password|  
|WebAuthenticationSignupConfirmNotice|Posta elettronica di conferma di registrazione è troppo {0}. < br /\> Please seguire istruzioni all'interno di hello tooactivate di posta elettronica dell'account. < br /\> controllare se la posta elettronica hello arrivano nella posta in arrivo all'interno di hello Avanti alcuni minuti, la cartella posta indesiderata.|  
|WebAuthenticationSignupConfirmNoticeHeader|Your account was successfully created (L'account è stato creato)|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|Registration confirmation email was sent again (Il messaggio di posta elettronica di conferma della registrazione è stato inviato di nuovo)|  
|WebAuthenticationSignupConfirmNoticeTitle|Account creato|  
|WebAuthenticationTokenRequiredErrorMessage|Token is empty (Il token è vuoto)|  
|WebAuthenticationUserAlreadyRegisteredNotice|Sembra che un utente con questo indirizzo e-mail è già registrato nel sistema hello. Se hai dimenticato la password, provare a toorestore oppure contattare il team di supporto.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|User already registered (Utente già registrato)|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Already registered (Già registrato)|  
|ButtonLabelChangePassword|Cambia password|  
|ButtonLabelChangeAccountInfo|Change account information(Modifica informazioni sull'account)|  
|ButtonLabelCloseAccount|Close account (Chiudi account)|  
|WebAuthenticationInvalidCaptchaErrorMessage|Testo immesso non corrisponde a testo sull'immagine di hello. Riprova più tardi.|  
|ValidationErrorCredentialsInvalid|Email or password is invalid. (Indirizzo email o password non validi.) . Correggere gli errori di hello e riprovare.|  
|WebAuthenticationRequestIsNotValid|Richiesta non valida.|  
|WebAuthenticationUserIsNotConfirm|Conferma la registrazione prima di tentare di toosign in.|  
|WebAuthenticationInvalidEmailFormated|Email is invalid: {0} (L'indirizzo di posta elettronica non è valido: {0})|  
|WebAuthenticationUserNotFound|Utente non trovato|  
|WebAuthenticationTenantNotRegistered|L'account appartiene tooa tenant di Azure Active Directory che non è autorizzato tooaccess questo portale.|  
|WebAuthenticationAuthenticationFailed|Authentication has failed. (Autenticazione non riuscita.)|  
|WebAuthenticationGooglePlusNotEnabled|Authentication has failed. (Autenticazione non riuscita.) Se l'utente autorizzato l'applicazione hello quindi contattare hello admin toomake assicurarsi che l'autenticazione di Google è configurato correttamente.|  
|ValidationErrorAllowedTenantIsRequired|Allowed Tenant is required (Il campo Tenant consentito è obbligatorio)|  
|ValidationErrorTenantIsNotValid|tenant di Azure Active Directory Hello '{0}' non è valido.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Log in using your {0} account (Accedere con l'account {0})|  
|WebAuthenticationUserLimitNotice|Questo servizio ha raggiunto il numero massimo di hello di utenti consentiti. . `<a href="mailto:{0}"\>contact hello administrator</a\>` Tooupgrade la registrazione di servizio e abilitare di nuovo utente.|  
|WebAuthenticationUserLimitNoticeHeader|User registration disabled (Registrazione utente disabilitata)|  
|WebAuthenticationUserLimitNoticeTitle|User registration disabled (Registrazione utente disabilitata)|  
|WebAuthenticationUserRegistrationDisabledNotice|Registrazione degli utenti è stata disabilitata dall'amministratore di hello. Please login with external identity provider. (Accedere con un provider di identità esterno.)|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|User registration disabled (Registrazione utente disabilitata)|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|User registration disabled (Registrazione utente disabilitata)|  
|WebAuthenticationSignupPendingConfirmationNotice|Prima di è possibile completare la creazione di hello del tuo account, è necessario tooverify indirizzo di posta elettronica. È stato inviato un messaggio di posta elettronica troppo {0}. Seguire hello istruzioni all'interno di hello tooactivate di posta elettronica all'account. Se la posta elettronica hello non perviene entro hello Avanti alcuni minuti, controllare la cartella posta indesiderata.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|È stato rilevato un account non confermato per indirizzo di posta elettronica hello {0}. creazione di hello toocomplete del tuo account che abbiamo bisogno di tooverify indirizzo di posta elettronica. È stato inviato un messaggio di posta elettronica troppo {0}. Seguire hello istruzioni all'interno di hello tooactivate di posta elettronica all'account. Se la posta elettronica hello non perviene entro hello Avanti alcuni minuti, verificare la cartella posta indesiderata|  
|WebAuthenticationSignupConfirmationAlmostDone|Almost Done (La procedura è quasi completata)|  
|WebAuthenticationSignupConfirmationEmailSent|È stato inviato un messaggio di posta elettronica troppo {0}. Seguire hello istruzioni all'interno di hello tooactivate di posta elettronica all'account. Se la posta elettronica hello non perviene entro hello Avanti alcuni minuti, controllare la cartella posta indesiderata.|  
|WebAuthenticationEmailSentNotificationMessage|Messaggio di posta elettronica inviato troppo {0}|  
|WebAuthenticationNoAadTenantConfigured|Tenant di Azure Active Directory non configurato per il servizio di hello.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Accetto toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Please review `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>` (Rivedere le `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`)|  
|DialogHeadingTermsOfUse|Condizioni per l'utilizzo|  
|ValidationMessageConsentNotAccepted|È necessario accettare le condizioni di utilizzo toohello prima di procedere.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|Nome|Text|  
|----------|----------|  
|WebAuthenticationForgotPassword|Password dimenticata?|  
|WebAuthenticationIfAdministrator|If you are an Administrator you must sign in `<a href="{0}"\>here</a\>`. (Gli amministratori devono accedere da `<a href="{0}"\>here</a\>`.)|  
|WebAuthenticationNotAMember|Not a member yet? (Non si è ancora membri?) `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Remember me on this computer (Memorizza utente su questo computer)|  
|WebAuthenticationSigininWithPassword|Sign in with your username and password (Immettere il proprio nome utente e la password)|  
|WebAuthenticationSigninTitle|pagina di accesso|  
|WebAuthenticationSignUpNow|Effettua l'iscrizione ora|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|Nome|Text|  
|----------|----------|  
|PageTitleSignup|Iscrizione|  
|WebAuthenticationAlreadyAMember|Already a member? (Si è già membri?)|  
|WebAuthenticationCreateNewAccount|Create a new API Management account (Creare un nuovo account di Gestione API)|  
|WebAuthenticationSigninNow|Sign in now (Accedere ora)|  
|ButtonLabelSignup|Iscrizione|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|Nome|Text|  
|----------|----------|  
|SubscriptionCancelConfirmation|Sono certi di voler toocancel questa sottoscrizione?|  
|SubscriptionRenewConfirmation|Sono certi di voler toorenew questa sottoscrizione?|  
|WebDevelopersManageSubscriptions|Gestisci sottoscrizioni|  
|WebDevelopersPrimaryKey|Chiave primaria|  
|WebDevelopersRegenerateLink|Regenerate (Rigenera)|  
|WebDevelopersSecondaryKey|Secondary key (Chiave secondaria)|  
|ButtonLabelShowKey|Mostra|  
|ButtonLabelRenewSubscription|Renew|  
|WebDevelopersSubscriptionReqested|Requested on {0} (Richiesta il {0})|  
|WebDevelopersSubscriptionRequestedState|Requested (Richiesta)|  
|WebDevelopersSubscriptionTableNameHeader|Nome|  
|WebDevelopersSubscriptionTableStateHeader|Stato|  
|WebDevelopersUsageStatisticsLink|Analytics reports (Report di analisi)|  
|WebDevelopersYourSubscriptions|Your subscriptions (Sottoscrizioni)|  
|SubscriptionPropertyLabelRequestedDate|Requested on (Richiesta il)|  
|SubscriptionPropertyLabelStartedDate|Started on (Avviata il)|  
|PageTitleRenameSubscription|Rename subscription (Rinomina sottoscrizione)|  
|SubscriptionPropertyLabelName|Nome della sottoscrizione|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|Nome|Text|  
|----------|----------|  
|SectionHeadingCloseAccount|Ricerca tooclose all'account?|  
|PageTitleDeveloperProfile|Profilo|  
|ButtonLabelHideKey|Nascondi|  
|ButtonLabelRegenerateKey|Regenerate (Rigenera)|  
|InformationMessageKeyWasRegenerated|Sono certi di voler tooregenerate questa chiave?|  
|ButtonLabelShowKey|Mostra|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|Nome|Text|  
|----------|----------|  
|ButtonLabelUpdateProfile|Update profile (Aggiorna profilo)|  
|PageTitleUpdateProfile|Update account information (Aggiorna informazioni sull'account)|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|Nome|Text|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Change account information(Modifica informazioni sull'account)|  
|ButtonLabelChangePassword|Cambia password|  
|ButtonLabelCloseAccount|Close account (Chiudi account)|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|Nome|  
|TextboxLabelEmailLastName|Cognome|  
|TextboxLabelNotificationsSenderEmail|Notifications sender email (Indirizzo di posta elettronica del mittente delle notifiche)|  
|TextboxLabelOrganizationName|Nome organizzazione|  
|SubscriptionStateActive|Attivo|  
|SubscriptionStateCancelled|Operazione annullata|  
|SubscriptionStateExpired|Scaduto|  
|SubscriptionStateRejected|Rifiutato|  
|SubscriptionStateRequested|Requested (Richiesta)|  
|SubscriptionStateSuspended|Suspended|  
|DefaultSubscriptionNameTemplate|{0}  (impostazione predefinita)|  
|SubscriptionNameTemplate|Accesso sviluppatore n.: {0}|  
|TextboxLabelSubscriptionName|Nome della sottoscrizione|  
|ValidationMessageSubscriptionNameRequired|Il nome della sottoscrizione non può essere vuoto.|  
|ApiManagementUserLimitReached|Questo servizio ha raggiunto il numero massimo di hello di utenti consentiti. Eseguire l'aggiornamento tooa maggiore livello di prezzo.|  
  
##  <a name="glyphs"></a> Risorse di tipo glifo  
 Modelli del portale di gestione API per sviluppatori possono utilizzare glifi hello [Glyphicons da Bootstrap](http://getbootstrap.com/components/#glyphicons). Questo set di glifi include più di 250 glifi in formato carattere dalla hello [Glyphicon](http://glyphicons.com/) Halflings impostato. toouse un glifo da questo set, utilizzare la seguente sintassi hello.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Per l'elenco completo di hello di icone, vedere [Glyphicons da Bootstrap](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).
