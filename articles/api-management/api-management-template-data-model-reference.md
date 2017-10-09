---
title: riferimento del modello di dati di modello di gestione API aaaAzure | Documenti Microsoft
description: "Scopri le rappresentazioni di tipo di entità e hello gli elementi comuni utilizzati nei modelli di dati hello per i modelli del portale per sviluppatori di hello in Gestione API di Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Informazioni di riferimento sui modelli di dati per i modelli di Gestione API di Azure
Questo argomento descrive le rappresentazioni di tipo di entità e hello gli elementi comuni utilizzati nei modelli di dati hello per i modelli del portale per sviluppatori di hello in Gestione API di Azure.  
  
 Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [Riepilogo delle API](#APISummary)  
-   [Applicazione](#Application)  
-   [Allegato](#Attachment)  
-   [Codice di esempio](#Sample)  
-   [Comment](#Comment)  
-   [Filtri](#Filtering)  
-   [Intestazione](#Header)  
-   [Richiesta HTTP](#HTTPRequest)  
-   [Risposta HTTP](#HTTPResponse)  
-   [Problema](#Issue)  
-   [Operazione](#Operation)  
-   [Menu operazione](#Menu)  
-   [Voce di menu operazione](#MenuItem)  
-   [Paging](#Paging)  
-   [Parametro](#Parameter)  
-   [Prodotto](#Product)  
-   [Provider](#Provider)  
-   [Rappresentazione](#Representation)  
-   [Sottoscrizione](#Subscription)  
-   [Riepilogo delle sottoscrizioni](#SubscriptionSummary)  
-   [Informazioni sull'account utente](#UserAccountInfo)  
-   [Accesso utente](#UseSignIn)  
-   [Iscrizione utente](#UserSignUp)  
  
##  <a name="API"></a>API  
 Hello `API` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|id|string|Identificatore di risorsa. Identifica in modo univoco l'API di hello nell'istanza del servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `apis/{id}` dove `{id}` è un identificatore API. Questa proprietà è di sola lettura.|  
|name|string|Nome dell'API hello. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|description|string|Descrizione dell'API hello. Non deve essere vuoto. Può includere tag di formattazione HTML. La lunghezza massima consentita è di 1000 caratteri.|  
|serviceUrl|string|URL assoluto del servizio back-end hello implementa questa API.|  
|path|string|URL relativo che identifica in modo univoco questa API e tutti i relativi percorsi delle risorse nell'istanza del servizio Gestione API di hello. Viene aggiunto l'URL di base dell'endpoint toohello API specificato durante tooform creazione istanza del servizio di hello un URL pubblico per questa API.|  
|protocols|matrice di valori numero|Descrive in quale hello protocolli operazioni in questa API possono essere richiamate. I valori consentiti sono `1 - http` e `2 - https` o entrambi.|  
|authenticationSettings|[Impostazioni di autenticazione del server di autorizzazione](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Raccolta delle impostazioni di autenticazione incluse in questa API.|  
|subscriptionKeyParameterNames|object|Proprietà facoltativa che può essere utilizzato toospecify nomi personalizzati per i parametri di query e/o intestazione contenente la chiave di sottoscrizione hello. Quando questa proprietà è presente deve contenere almeno una delle due proprietà seguenti di hello.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a>Riepilogo delle API  
 Hello `API summary` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|id|string|Identificatore di risorsa. Identifica in modo univoco l'API di hello nell'istanza del servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `apis/{id}` dove `{id}` è un identificatore API. Questa proprietà è di sola lettura.|  
|name|string|Nome dell'API hello. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|description|string|Descrizione dell'API hello. Non deve essere vuoto. Può includere tag di formattazione HTML. La lunghezza massima consentita è di 1000 caratteri.|  
  
##  <a name="Application"></a> Applicazione  
 Hello `application` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|Identificatore univoco dell'applicazione hello di Hello.|  
|Titolo|string|titolo Hello dell'applicazione hello.|  
|Descrizione|string|descrizione di Hello dell'applicazione hello.|  
|Url|URI|Hello URI per un'applicazione hello.|  
|Versione|string|Informazioni sulla versione per un'applicazione hello.|  
|Requisiti|string|Una descrizione dei requisiti per un'applicazione hello.|  
|Stato|number|stato corrente di Hello dell'applicazione hello.<br /><br /> - 0 - Registrato<br /><br /> - 1 - Inviato<br /><br /> - 2 - Pubblicato<br /><br /> - 3 - Rifiutato<br /><br /> - 4 - Non pubblicato|  
|RegistrationDate|DateTime|un'applicazione hello data e ora Hello è stata registrata.|  
|CategoryId|number|categoria di Hello di un'applicazione hello (Finance, intrattenimento e così via).|  
|DeveloperId|string|Identificatore univoco di Hello dello sviluppatore hello che ha inviato l'applicazione hello.|  
|Attachments|Raccolta di entità [allegato](#Attachment).|Eventuali allegati per un'applicazione hello, ad esempio schermate o icone.|  
|Icona|[Allegato](#Attachment)|hello di icona Hello per un'applicazione hello.|  
  
##  <a name="Attachment"></a>Allegato  
 Hello `attachment` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|UniqueId|string|Identificatore univoco per l'allegato hello di Hello.|  
|Url|string|Hello l'URL della risorsa hello.|  
|Tipo|string|tipo di Hello dell'allegato.|  
|ContentType|string|tipo di supporto Hello di allegato hello.|  
  
##  <a name="Sample"></a>Codice di esempio  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|title|string|nome Hello dell'operazione di hello.|  
|snippet|string|Questa proprietà è deprecata e non deve essere usata.|  
|brush|string|Quale modello toobe utilizzato per la visualizzazione nell'esempio di codice hello di colorazione della sintassi del codice. I valori consentiti sono `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` e `csharp`.|  
|template|string|nome Hello di questo modello di esempio di codice.|  
|body|string|Un segnaposto per parte di esempio di codice hello del frammento di codice hello.|  
|statico|string|metodo HTTP dell'operazione hello Hello.|  
|scheme|string|Hello toouse di protocollo per la richiesta di operazione hello.|  
|path|string|percorso di Hello dell'operazione di hello.|  
|query|string|Esempio di stringa di query con parametri definiti.|  
|host|string|URL di Hello hello API del servizio di gateway di gestione per hello API che contiene questa operazione.|  
|headers|Raccolta di entità [intestazione](#Header).|Intestazioni per l'operazione.|  
|Parametri|Raccolta di entità[parametro](#Parameter).|Parametri definiti per l'operazione.|  
  
##  <a name="Comment"></a>Commento  
 Hello `API` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|number|id di Hello del commento hello.|  
|CommentText|string|corpo Hello del commento hello. Può includere HTML.|  
|DeveloperCompany|string|nome della società Hello dello sviluppatore hello.|  
|PostedOn|DateTime|commento di hello Hello data e ora è stato registrato.|  
  
##  <a name="Issue"></a>Problema  
 Hello `issue` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|Identificatore univoco di Hello per problema hello.|  
|ApiID|string|id Hello hello API per cui si è verificato il problema.|  
|Titolo|string|Titolo del problema hello.|  
|Descrizione|string|Descrizione del problema hello.|  
|SubscriptionDeveloperName|string|Nome dello sviluppatore hello che hello problemi segnalati.|  
|IssueState|string|stato corrente di Hello del problema hello. I valori possibili sono Proposto, Aperto e Chiuso.|  
|ReportedOn|DateTime|si è verificato un problema di hello Hello data e ora.|  
|Commenti|Raccolta di entità [commento](#Comment).|Commenti sul problema.|  
|Attachments|Raccolta di entità [allegato](api-management-template-data-model-reference.md#Attachment).|Qualsiasi problema di toohello allegati.|  
|Services|Raccolta di entità [API](#API).|Hello API sottoscritto utente hello tooby che è archiviato il problema di hello.|  
  
##  <a name="Filtering"></a>Filtri  
 Hello `filtering` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Modello|string|termine di ricerca corrente Hello; o `null` se non vi è alcun termine di ricerca.|  
|Placeholder|string|Hello toodisplay di testo nella casella di ricerca hello quando è presente alcun termine di ricerca specificato.|  
  
##  <a name="Header"></a>Intestazione  
 In questa sezione descrive hello `parameter` rappresentazione.  
  
|Proprietà|Descrizione|Tipo|  
|--------------|-----------------|----------|  
|name|string|Nome del parametro.|  
|description|string|Descrizione del parametro.|  
|value|string|Valore dell'intestazione.|  
|typeName|string|Tipo di dati del valore dell'intestazione.|  
|options|string|Opzioni.|  
|Obbligatoria|boolean|Indica se l'intestazione hello è obbligatorio.|  
|readOnly|boolean|Indica se intestazione hello è di sola lettura.|  
  
##  <a name="HTTPRequest"></a>Richiesta HTTP  
 In questa sezione descrive hello `request` rappresentazione.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|description|string|Descrizione della richiesta dell'operazione.|  
|Headers|matrice di entità [Intestazione](#Header).|Intestazioni della richiesta.|  
|Parametri|matrice di valori [Parametro](#Parameter)|Raccolta di parametri della richiesta dell'operazione.|  
|representations|matrice di valori [Rappresentazione](#Representation)|Raccolta di rappresentazioni della richiesta dell'operazione.|  
  
##  <a name="HTTPResponse"></a>Risposta HTTP  
 In questa sezione descrive hello `response` rappresentazione.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|statusCode|intero positivo|Codice di stato della risposta dell'operazione.|  
|description|string|Descrizione della risposta dell'operazione.|  
|representations|matrice di valori [Rappresentazione](#Representation)|Raccolta di rappresentazioni della risposta dell'operazione.|  
  
##  <a name="Operation"></a>Operazione  
 Hello `operation` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|id|string|Identificatore di risorsa. Identifica in modo univoco l'operazione di hello nell'istanza di servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `apis/{aid}/operations/{id}` in `{aid}` è un identificatore di API e `{id}` è un identificatore di operazione. Questa proprietà è di sola lettura.|  
|name|string|Nome dell'operazione di hello. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|description|string|Descrizione dell'operazione di hello. Non deve essere vuoto. Può includere tag di formattazione HTML. La lunghezza massima consentita è di 1000 caratteri.|  
|scheme|string|Descrive in quale hello protocolli operazioni in questa API possono essere richiamate. I valori consentiti sono `http`, `https` o sia `http` sia `https`.|  
|uriTemplate|string|Modello di URL relativo che identifica la risorsa di destinazione hello per questa operazione. Può includere parametri. Esempio: `customers/{cid}/orders/{oid}/?date={date}`|  
|host|string|Hello API Gestione gateway URL che ospita l'API di hello.|  
|httpMethod|string|Metodo HTTP dell'operazione.|  
|richiesta|[Richiesta HTTP](#HTTPRequest)|Entità contenente i dettagli della richiesta.|  
|responses|matrice di valori [Risposta HTTP](#HTTPResponse)|Matrice di entità [Risposta HTTP](#HTTPResponse) dell'operazione.|  
  
##  <a name="Menu"></a>Menu operazione  
 Hello `operation menu` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ApiID|string|id di Hello dell'API di hello corrente.|  
|CurrentOperationId|string|id di Hello dell'operazione corrente hello.|  
|Azione|string|tipo di menu Hello.|  
|MenuItems|Raccolta di entità [Voce di menu operazione](#MenuItem).|operazioni di Hello per API corrente hello.|  
  
##  <a name="MenuItem"></a>Voce di menu operazione  
 Hello `operation menu item` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|id di Hello dell'operazione di hello.|  
|Titolo|string|Descrizione Hello dell'operazione di hello.|  
|HttpMethod|string|metodo Http dell'operazione hello Hello.|  
  
##  <a name="Paging"></a>Paging  
 Hello `paging` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Page|number|numero di pagina corrente Hello.|  
|PageSize|number|Hello toobe numero massimo di risultati visualizzato in una singola pagina.|  
|TotalItemCount|number|numero di Hello di elementi per la visualizzazione.|  
|ShowAll|boolean|Se toosho tutti i risultati in una singola pagina.|  
|PageCount|number|numero di Hello di pagine di risultati.|  
  
##  <a name="Parameter"></a>Parametro  
 In questa sezione descrive hello `parameter` rappresentazione.  
  
|Proprietà|Descrizione|Tipo|  
|--------------|-----------------|----------|  
|name|string|Nome del parametro.|  
|description|string|Descrizione del parametro.|  
|value|string|Valore del parametro.|  
|options|matrice di valori string|Valori definiti per i valori del parametro di query.|  
|Obbligatoria|boolean|Indica se il parametro è obbligatorio o no.|  
|kind|number|Se questo parametro è un parametro di percorso (1) o un parametro di stringa di query (2).|  
|typeName|string|Tipo di parametro.|  
  
##  <a name="Product"></a>Prodotto  
 Hello `product` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|Identificatore di risorsa. Identifica in modo univoco il prodotto di hello nell'istanza del servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `products/{pid}` dove `{pid}` è un identificatore di prodotto. Questa proprietà è di sola lettura.|  
|Titolo|string|Nome del prodotto hello. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|Descrizione|string|Descrizione del prodotto hello. Non deve essere vuoto. Può includere tag di formattazione HTML. La lunghezza massima consentita è di 1000 caratteri.|  
|Termini|string|Condizioni per l'utilizzo del prodotto. Gli sviluppatori tentano toosubscribe toohello prodotto verranno visualizzati e necessario tooaccept questi termini prima di poter completare il processo di sottoscrizione hello.|  
|ProductState|number|Specifica se il prodotto hello è pubblicato o meno. I prodotti pubblicati possono essere individuati dagli sviluppatori sul portale per sviluppatori hello. I prodotti non pubblicati sono visibili tooadministrators solo.<br /><br /> valori consentiti di Hello per lo stato del prodotto sono:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|boolean|Specifica se un utente può contenere più prodotti di toothis le sottoscrizioni in hello contemporaneamente.|  
|MultipleSubscriptionsCount|number|Hello numero di sottoscrizioni toothis prodotto dall'utente corrente hello.|  
  
##  <a name="Provider"></a>Provider  
 Hello `provider` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Proprietà|dizionario di stringhe|Proprietà per questo provider di autenticazione.|  
|AuthenticationType|string|tipo di provider Hello. (Azure Active Directory, account di accesso di Facebook, account Google, account Microsoft, Twitter).|  
|Sottotitolo|string|Nome visualizzato del provider di hello.|  
  
##  <a name="Representation"></a>Rappresentazione  
 Questa sezione descrive una `representation`.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|contentType|string|Specifica un tipo di contenuto registrato o personalizzato per questa rappresentazione, ad esempio `application/xml`.|  
|sample|string|Un esempio di rappresentazione hello.|  
  
##  <a name="Subscription"></a>Sottoscrizione  
 Hello `subscription` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|Identificatore di risorsa. Identifica in modo univoco la sottoscrizione hello nell'istanza di servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `subscriptions/{sid}` dove `{sid}` è un identificatore di sottoscrizione. Questa proprietà è di sola lettura.|  
|ProductId|string|Identificatore di risorsa prodotto Hello di hello sottoscritto prodotto. il valore di Hello è un URL relativo valido con formato hello `products/{pid}` dove `{pid}` è un identificatore di prodotto.|  
|ProductTitle|string|Nome del prodotto hello. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|ProductDescription|string|Descrizione del prodotto hello. Non deve essere vuoto. Può includere tag di formattazione HTML. La lunghezza massima consentita è di 1000 caratteri.|  
|ProductDetailsUrl|string|Dettagli del prodotto toohello URL relativi.|  
|state|string|stato di Hello della sottoscrizione hello. Gli stati possibili sono elencati di seguito:<br /><br /> - `0 - suspended`: hello sottoscrizione è bloccata e il sottoscrittore hello non è possibile chiamare le API del prodotto hello.<br /><br /> - `1 - active`: hello sottoscrizione è attiva.<br /><br /> - `2 - expired`: hello ha raggiunto la data di scadenza ed è stata disattivata.<br /><br /> - `3 - submitted`: la richiesta di sottoscrizione hello è stata effettuata dallo sviluppatore di hello, ma non è ancora stata approvata o rifiutata.<br /><br /> - `4 - rejected`: hello sottoscrizione richiesta è stata rifiutata da un amministratore.<br /><br /> - `5 - cancelled`-sottoscrizione hello è stata annullata dallo sviluppatore hello o un amministratore.|  
|DisplayName|string|Nome visualizzato della sottoscrizione hello.|  
|CreatedDate|dateTime|sottoscrizione di hello data Hello è stato creato, nel formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|boolean|Se la sottoscrizione hello può essere annullata dall'utente corrente hello.|  
|IsAwaitingApproval|boolean|Se la sottoscrizione hello è in attesa di approvazione.|  
|StartDate|dateTime|Hello data di inizio per la sottoscrizione di hello, in formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|dateTime|Data di scadenza Hello sottoscrizione hello, in formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|NotificationDate|dateTime|Data di notifica Hello per sottoscrizione hello, in formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|primaryKey|string|chiave di sottoscrizione primaria Hello. La lunghezza massima consentita è di 256 caratteri.|  
|secondaryKey|string|chiave di sottoscrizione secondaria Hello. La lunghezza massima consentita è di 256 caratteri.|  
|CanBeRenewed|boolean|Se la sottoscrizione hello può essere rinnovata dall'utente corrente hello.|  
|HasExpired|boolean|Se la sottoscrizione hello è scaduto.|  
|IsRejected|boolean|Se la richiesta di sottoscrizione hello è stata negata.|  
|CancelUrl|string|Hello relativo Url toocancel hello sottoscrizione.|  
|RenewUrl|string|Hello relativo Url toorenew hello sottoscrizione.|  
  
##  <a name="SubscriptionSummary"></a>Riepilogo delle sottoscrizioni  
 Hello `subscription summary` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|ID|string|Identificatore di risorsa. Identifica in modo univoco la sottoscrizione hello nell'istanza di servizio Gestione API corrente hello. il valore di Hello è un URL relativo valido con formato hello `subscriptions/{sid}` dove `{sid}` è un identificatore di sottoscrizione. Questa proprietà è di sola lettura.|  
|DisplayName|string|Hello nome visualizzato della sottoscrizione hello|  
  
##  <a name="UserAccountInfo"></a>Informazioni sull'account utente  
 Hello `user account info` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|FirstName|string|Nome. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|LastName|string|Cognome. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|Email|string|Indirizzo di posta elettronica. Non deve essere vuoto e deve essere univoco nell'istanza di servizio hello. La lunghezza massima consentita è di 254 caratteri.|  
|Password|string|Password dell'account utente.|  
|NameIdentifier|string|Account, identificatore hello come messaggio di posta elettronica utente hello.|  
|ProviderName|string|Nome del provider di autenticazione.|  
|IsBasicAccount|boolean|True se questo account è stato registrato tramite posta elettronica e la password. false se è stata registrata utilizzando un provider di account hello.|  
  
##  <a name="UseSignIn"></a>Accesso utente  
 Hello `user sign in` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Email|string|Indirizzo di posta elettronica. Non deve essere vuoto e deve essere univoco nell'istanza di servizio hello. La lunghezza massima consentita è di 254 caratteri.|  
|Password|string|Password dell'account utente.|  
|ReturnUrl|string|Hello l'URL della pagina di hello in hello scelto di accesso.|  
|RememberMe|boolean|Se toosave hello informazioni dell'utente corrente.|  
|RegistrationEnabled|boolean|Se la registrazione è abilitata.|  
|DelegationEnabled|boolean|Se l'accesso delegato è abilitato.|  
|DelegationUrl|string|Hello delegata sign in url, se abilitato.|  
|SsoSignUpUrl|string|Hello unico URL di accesso per utente hello, se presente.|  
|AuxServiceUrl|string|Se l'utente corrente di hello è un amministratore, questa è un'istanza del servizio toohello collegamento nel portale di Azure classico hello.|  
|Providers|Raccolta di entità [Provider](#Provider).|Hello provider di autenticazione per questo utente.|  
|UserRegistrationTerms|string|Condizioni che un utente deve accettare toobefore accesso.|  
|UserRegistrationTermsEnabled|boolean|Se le condizioni sono accettate.|  
  
##  <a name="UserSignUp"></a>Iscrizione utente  
 Hello `user sign up` entità dispone di hello le proprietà seguenti.  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|PasswordConfirm|boolean|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up)controllo per l'abbonamento.|  
|Password|string|Password dell'account utente.|  
|PasswordVerdictLevel|number|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up)controllo per l'abbonamento.|  
|UserRegistrationTerms|string|Condizioni che un utente deve accettare toobefore accesso.|  
|UserRegistrationTermsOptions|number|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up)controllo per l'abbonamento.|  
|ConsentAccepted|boolean|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up)controllo per l'abbonamento.|  
|Email|string|Indirizzo di posta elettronica. Non deve essere vuoto e deve essere univoco nell'istanza di servizio hello. La lunghezza massima consentita è di 254 caratteri.|  
|FirstName|string|Nome. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|LastName|string|Cognome. Non deve essere vuoto. La lunghezza massima consentita è di 100 caratteri.|  
|UserData|string|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up) controllo.|  
|NameIdentifier|string|Valore usato da hello [iscrizione](api-management-page-controls.md#sign-up)controllo per l'abbonamento.|  
|ProviderName|string|Nome del provider di autenticazione.|

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).
