---
title: aaaUnderstanding hello Azure Active Directory Application Manifest | Documenti Microsoft
description: "Descrizione dettagliata del hello Azure Active Directory manifesto dell'applicazione, che rappresenta la configurazione di identità di un'applicazione in un tenant di Azure AD e l'autorizzazione di OAuth usato toofacilitate, l'esperienza di consenso e molto altro ancora."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Manifesto dell'applicazione di conoscenza hello Azure Active Directory
Applicazioni che si integrano con Azure Active Directory (AD) devono essere registrate con un tenant di Azure AD, fornendo una configurazione di identità permanente per un'applicazione hello. Questa configurazione viene consultata in fase di esecuzione, l'abilitazione di scenari che consentono a un'applicazione toooutsource e broker autenticazione/autorizzazione tramite Azure AD. Per ulteriori informazioni sul modello di applicazione hello Azure AD, vedere hello [aggiunta, aggiornamento e rimozione di un'applicazione] [ ADD-UPD-RMV-APP] articolo.

## <a name="updating-an-applications-identity-configuration"></a>Aggiornamento della configurazione dell'identità di un'applicazione
Esistono effettivamente più opzioni per l'aggiornamento delle proprietà hello sulla configurazione di identità di un'applicazione, che variano in grado di difficoltà, inclusi i seguenti hello e funzionalità:

* Hello  **[portale di Azure] [ AZURE-PORTAL] interfaccia utente Web** consente proprietà più comuni di hello tooupdate di un'applicazione. Si tratta di hello più rapido e almeno modo soggetta a errore di aggiornamento delle proprietà dell'applicazione, ma non forniscono proprietà tooall accesso completo, ad esempio hello due metodi.
* Per scenari più avanzati in cui è necessario tooupdate proprietà non esposte nel portale di Azure classico hello, è possibile modificare hello **manifesto dell'applicazione**. Questo è lo stato attivo hello di questo articolo e viene illustrato in dettaglio nella sezione successiva hello a partire da.
* È inoltre possibile troppo**scrivere un'applicazione che utilizza hello [API Graph] [ GRAPH-API]**  tooupdate l'applicazione, che richiede hello la maggior parte delle attività. Può trattarsi di un'opzione attraente, tuttavia, se si sta scrivendo un software di gestione, o necessario tooupdate proprietà dell'applicazione a intervalli regolari in modo automatico.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Utilizzando la configurazione di identità di un'applicazione tooupdate manifesto di applicazione hello
Tramite hello [portale di Azure][AZURE-PORTAL], è possibile gestire la configurazione dell'applicazione identità aggiornando il manifesto di applicazione hello utilizzando l'editor del manifesto hello inline. È anche possibile scaricare e caricare il manifesto dell'applicazione hello come un file JSON. Nessun file effettivo viene archiviato nella directory hello. manifesto dell'applicazione Hello è semplicemente un'operazione HTTP GET sull'entità applicazione hello API Azure AD Graph e caricamento hello è un'operazione HTTP PATCH nell'entità applicazione hello.

Di conseguenza, in formato di ordine toounderstand hello e le proprietà del manifesto dell'applicazione hello, sarà necessario tooreference hello API Graph [entità applicazione] [ APPLICATION-ENTITY] documentazione. Ecco alcuni esempi di aggiornamenti che possono essere eseguiti con il caricamento del manifesto dell'applicazione:

* **Dichiarare gli ambiti di autorizzazione** (oauth2Permissions) esposti dall'API Web. Vedere l'argomento "TooOther API Web esposizione applicazioni" hello [integrazione di applicazioni con Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] per informazioni sull'implementazione della rappresentazione di utenti con hello oauth2Permissions ambito delle autorizzazioni delegate. Come accennato in precedenza, le proprietà delle entità applicazione sono documentate in hello API Graph [entità e il tipo complesso] [ APPLICATION-ENTITY] articolo di riferimento, tra cui hello oauth2Permissions proprietà una raccolta di tipo [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Dichiarare i ruoli applicazione (appRoles) esposti dall'app**. proprietà appRoles dell'entità applicazione Hello è una raccolta di tipo [AppRole][APPLICATION-ENTITY-APP-ROLE]. Vedere hello [controllo di accesso nelle applicazioni cloud mediante Azure AD in base al ruolo] [ RBAC-CLOUD-APPS-AZUREAD] articolo per un esempio di implementazione.
* **Dichiarare client note applicazioni (knownClientApplications)**, che consentono di consenso di hello tie toologically di hello specificato client applicazioni toohello risorsa web e API.
* **Richiedere l'appartenenza al gruppo di Azure AD tooissue attestazione** per hello effettuato l'accesso utente (groupMembershipClaims).  Può anche essere attestazioni tooissue configurato sull'appartenenza ai ruoli di directory dell'utente hello. Vedere hello [autorizzazione nelle applicazioni Cloud tramite i gruppi di Active Directory] [ AAD-GROUPS-FOR-AUTHORIZATION] articolo per un esempio di implementazione.
* **Consenti la concessione di OAuth 2.0 impliciti toosupport applicazione** flussi (oauth2AllowImplicitFlow). Questo tipo di flusso di concessione viene usato con pagine Web con JavaScript incorporato o con applicazioni a pagina singola (Single Page Applications, SPA). Per ulteriori informazioni sulla concessione di autorizzazioni implicite hello, vedere [hello conoscenza implicita OAuth2 concedere del flusso di Azure Active Directory][IMPLICIT-GRANT].
* **Abilitare l'utilizzo di X509 certificati come chiave segreta hello** (keyCredentials). Vedere hello [creazione di applicazioni di servizio e il daemon in Office 365] [ O365-SERVICE-DAEMON-APPS] e [tooauth di Guida per gli sviluppatori con API di gestione risorse di Azure] [ DEV-GUIDE-TO-AUTH-WITH-ARM] articoli per esempi di implementazione.
* **Aggiungere un nuovo URI ID app** per l'applicazione (identifierURIs[]). Usare gli URI ID App toouniquely identificare un'applicazione all'interno di relativi tenant di Azure AD (o in più tenant di Azure AD, per gli scenari di multi-tenant quando qualificato tramite il dominio personalizzato verificato). Vengono utilizzati per la richiesta di applicazione della risorsa autorizzazioni tooa, o l'acquisizione di un token di accesso per un'applicazione della risorsa. Quando si aggiorna questo elemento, hello stesso aggiornamento viene eseguita insieme, [] servicePrincipalNames di toohello corrispondente entità servizio che si trova nel tenant principale dell'applicazione hello.

Hello manifesto dell'applicazione fornisce inoltre un modo efficace di tootrack hello stato della registrazione dell'applicazione. Poiché è disponibile in formato JSON, rappresentazione del file hello possa essere verificato nel controllo del codice sorgente, insieme al codice dell'applicazione.

## <a name="step-by-step-example"></a>Esempio dettagliato
Ora consente di scorrere hello passaggi necessari tooupdate configurazione dell'identità dell'applicazione tramite manifesto dell'applicazione hello. Verranno evidenziati uno di hello precedenti esempi, che mostra come toodeclare ambito di una nuova autorizzazione su un'applicazione della risorsa:

1. Accedi toohello [portale di Azure][AZURE-PORTAL].
2. Dopo che ha eseguito l'autenticazione, è possibile scegliere tenant di Azure AD selezionandolo hello angolo superiore destro della pagina hello.
3. Selezionare **Azure Active Directory** estensione da hello a sinistra del Pannello di navigazione e fare clic su nella **registrazioni di App**.
4. Trovare un'applicazione hello tooupdate nell'elenco di hello desiderato e fare clic su di esso.
5. Dalla pagina dell'applicazione hello, fare clic su **manifesto** editor del manifesto tooopen hello inline. 
6. È possibile modificare direttamente il manifesto di hello utilizzando l'editor. Si noti che manifesto hello segue lo schema di hello per hello [entità applicazione] [ APPLICATION-ENTITY] come menzionato in precedenza: ad esempio, supponendo che si desidera tooimplement/espongono una nuova autorizzazione chiamato "Employees.Read.All" Nell'applicazione della risorsa (API), è necessario aggiungere una raccolta di nuovo al secondo elemento toohello oauth2Permissions, semplicemente Internet Explorer:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    voce Hello deve essere univoci e pertanto è necessario generare un nuovo globalmente univoco ID (GUID) per hello `"id"` proprietà. In questo caso, poiché è specificato `"type": "User"`, questa autorizzazione può essere stato fornito il consenso tooby qualsiasi account autenticati da hello tenant di Azure AD in cui hello/API risorse applicazione registrata. Questa autorizzazione tooaccess di concessioni hello client dell'applicazione, per conto dell'account hello. stringhe di nomi di descrizione e la visualizzazione Hello vengono utilizzate durante il consenso e per la visualizzazione nel portale di Azure hello.
6. Al termine Aggiorna hello manifesto, fare clic su **salvare** manifesto hello toosave.  
   
Ora che hello manifesto viene salvato, è possibile assegnare un client registrato applicazione toohello nuova autorizzazione di accesso che è stato aggiunto in precedenza. Questa fase che è possibile utilizzare hello dell'interfaccia utente Web del portale di Azure invece di modificare il manifesto dell'applicazione hello client:  

1. Innanzitutto vedere toohello **impostazioni** blade di hello client applicazione toowhich desiderato tooadd accesso toohello nuova API, fare clic su **autorizzazioni obbligatorie** e scegliere **selezionare un'API** .
2. Quindi verrà visualizzato hello elenco delle applicazioni di risorse registrati (API) nel tenant di hello. Fare clic su hello risorse applicazione tooselect, o nome della casella di ricerca di hello applicazione hello hello del tipo. Dopo aver trovato un'applicazione hello, fare clic su **selezionare**.  
3. L'operazione richiederà toohello **selezionare autorizzazioni** pagina, che verrà visualizzato hello elenco di autorizzazioni per l'applicazione e disponibili per l'applicazione della risorsa hello autorizzazioni delegate. Selezionare hello in ordine tooadd nuova autorizzazione è richiesta dal client toohello elenco di autorizzazioni. La nuova autorizzazione verrà archiviata nella configurazione di identità dell'applicazione hello client, nella proprietà di raccolta "requiredResourceAccess" hello.


È tutto. Ora le applicazioni verranno eseguite usando la nuova configurazione dell'identità.

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sulla relazione hello tra gli oggetti applicazione e dell'entità servizio dell'applicazione, vedere [applicazione e oggetti entità servizio in Azure AD][AAD-APP-OBJECTS].
* Vedere hello [glossario di Azure AD per sviluppatori] [ AAD-DEVELOPER-GLOSSARY] per le definizioni di alcuni dei concetti di hello per sviluppatori di Azure Active Directory (AD).

Utilizzare sezione commenti hello tooprovide feedback e consentono di ridefinire e definire il contenuto.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

