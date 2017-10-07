---
title: App, autorizzazioni e consenso in Azure Active Directory | Documentazione Microsoft
description: "Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD."
keywords: "tooAzure introduzione AD App, che cos'è Azure AD Connect, installare active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>App, autorizzazioni e consenso in Azure Active Directory
All'interno di Azure Active Directory, è possibile aggiungere directory tooyour delle applicazioni.  applicazioni Hello possono variare a seconda di tipo hello dell'applicazione.  applicazioni tooview nel portale classico hello, selezionare una directory e scegliere le applicazioni.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

## <a name="types-of-apps"></a>Tipi di app

1. **App a tenant singolo** </br>
    - **App single-tenant** -noto anche delle App line-of-business (LOB) tooas. Ciò avviene hello in cui un utente all'interno dell'organizzazione sviluppa l'app e si desidera che gli utenti in toosign in grado di hello organizzazione toobe nell'app toohello.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **App Proxy app** - quando si espone un'applicazione locale con Azure AD App Proxy, un'applicazione single-tenant è registrata nel tenant (in aggiunta toohello servizio Proxy di applicazione). Questa app è ciò che rappresenta l'applicazione locale per tutte le interazioni cloud (ad esempio, autenticazione). L'app proxy richiede Azure AD Basic o versione successiva.


2. **App multi-tenant**
    - **App multi-tenant che altri possano accettare** - simile troppo "app single-tenant che sviluppa organizzazione". Hello differenza principale (oltre alla logica di hello in app hello stessa) è che gli utenti di altri tenant possono anche fornire il consenso tooand Accedi toohello app.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **App multi-tenant sviluppate da terzi per cui Contoso ha ottenuto il consenso**, o, in breve, "app con consenso". Questo è il lato capovolto hello di "multi-tenant App che sviluppate dall'organizzazione". Quando un'altra organizzazione sviluppa un'applicazione multi-tenant, gli utenti dell'organizzazione possono fornire il consenso toohello app e accedere tooit.
    - **App proprietarie di Microsoft**: app che rappresentano i servizi Microsoft. Consenso viene gestito dal fatto di hello che si esegue l'iscrizione per il servizio di hello. È talvolta speciale dell'esperienza utente e la logica per determinate applicazioni prima parte che viene spesso utilizzata per la definizione dei criteri sull'accesso toohello app.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Le app preintegrate** -App disponibili nella raccolta di App di Azure AD, è possibile aggiungere hello tooyour directory tooprovide single sign-on (e in alcuni casi, il provisioning) App SaaS toopopular.
    - **Accesso Single Sign-On di Azure AD**: SSO "reale", per le app che possono essere integrate con Azure AD, tramite un protocollo di accesso supportato, ad esempio SAML 2.0 oppure OpenID Connect. procedura guidata Hello illustra la configurazione.
    - **Password single sign-on**: Azure AD archivia in modo sicuro le credenziali dell'utente hello per app di hello e credenziali hello "inserite" nel modulo di accesso hello dal hello estensione browser di accedere all'App Azure AD. Scenario noto anche come "insieme di credenziali delle password".

## <a name="permissions"></a>Autorizzazioni

Quando si registra un'app, utente hello che esegue hello app registrazione (ovvero, lo sviluppatore hello) definisce quale app hello autorizzazioni deve accedere a e le risorse. le risorse hello sono, autonomamente, definito come le altre app. Ad esempio, un utente la creazione di un'applicazione lettore di posta elettronica, sarebbe stato che la propria applicazione richiede l'autorizzazione "Accesso alle cassette postali come utente connesso di hello" hello "Office 365 Exchange risorsa in linea" hello:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Affinché un'applicazione (client hello) toorequest determinate autorizzazioni da un'altra applicazione (risorse hello), gli sviluppatori di hello di hello risorsa app definisce le autorizzazioni di hello esistenti. In questo esempio, Microsoft, il proprietario di hello di app di risorsa "Office 365 Exchange Online" hello, hanno definito un'autorizzazione denominata "Accedere alle cassette postali come utente connesso di hello".

Quando si definiscono le autorizzazioni, è necessario definire per sviluppatori di app hello se può essere concessa autorizzazione hello, o se è necessario consenso dell'amministratore. In questo modo gli sviluppatori tooallow utenti tooconsent i propri tooapps richiedono solo le autorizzazioni di sensibilità bassa, ma richiedono autorizzazioni di amministratori tooconsent toomore sensibili. Salve, ad esempio, "Azure Active Directory" risorse app, è stato definito, pertanto gli utenti possono fornire il consenso tooapps, richiedono le autorizzazioni di sola lettura limitate.  Tuttavia, il consenso dell'amministratore è obbligatorio per le autorizzazioni di lettura complete e tutte le autorizzazioni di scrittura.

Poiché i client nativi non sono autenticati, un'app definita come app client nativa può richiedere solo autorizzazioni delegate. Ciò significa che deve essere sempre presente un utente effettivo quando si ottiene un token. Le app e le API Web (client riservati) devono sempre eseguire l'autenticazione con Azure AD quando ottengono un token di accesso. Ovvero devono avere anche il possibilità hello che richiedono le autorizzazioni solo per app. Ad esempio, se un servizio back-end è necessario il servizio back-end di tooauthenticate tooanother. Le autorizzazioni che richiedono autorizzazioni di sola app richiedono sempre il consenso dell'amministratore.

Riepilogo:



- Un'applicazione (client) stati autorizzazioni hello che necessarie per altre applicazioni (risorse).
- Un'app (risorsa) indica quali autorizzazioni sono esposti tooother App (client).
- Un'autorizzazione può essere di tipo sola app o delegata.
- Un'autorizzazione delegata può essere contrassegnata come "consente il consenso dell'utente," o "richiede il consenso dell'amministratore".
- Un'app può funzionare come client (dichiarando che deve risorsa tooa autorizzazioni), come una risorsa (dichiarando le autorizzazioni che espone) o come entrambe.

## <a name="controls"></a>Controlli

di seguito Hello è un elenco di hello admin diversi controlli disponibili per tutti i questo comportamento. salve controlli accessibili nel portale classico di hello da configurare nella directory hello.

![](media/active-directory-apps-permissions-consent/apps7.png)

In hello Azure portale, in **gestire**, **impostazioni utente**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- È possibile controllare se gli utenti possono fornire il consenso tooapps:

Nel portale classico di hello selezionare **gli utenti possono concedere applicazioni autorizzazioni tooaccess i propri dati.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Nel portale di Azure hello, selezionare **gli utenti possono consentire App tooaccess i propri dati**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- È possibile controllare se gli utenti possono registrare le proprie App LOB single-tenant: nella finestra Seleziona portale classico hello **gli utenti possono aggiungere applicazioni integrate.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Nel portale di Azure hello, selezionare **gli utenti possono consentire App tooaccess i propri dati**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Anche se si consente agli utenti le app LOB di tooregister single-tenant, vi sono limiti toowhat possono essere registrati.  
>Ad esempio, per gli sviluppatori che non sono amministratori della directory.
>
>- Gli utenti non possono rendere un'app a tenant singolo un'app multi-tenant.
>- Quando si registra App LOB single-tenant, gli utenti possono richiedere le autorizzazioni solo app tooother app.
>- Quando si registra App LOB single-tenant, gli utenti possono richiedere le autorizzazioni delegate tooother App se tali autorizzazioni richiedono consenso dell'amministratore.
>- Gli utenti non possono apportare modifiche tooapps che non sono proprietari del.



- È possibile controllare se gli utenti possono aggiungere app preintegrate che usano password SSO (ossia "insieme di credenziali delle password") ![](media/active-directory-apps-permissions-consent/apps10.png)



- È possibile controllare le condizioni in base alle quali è possibile accedere alle applicazioni (ovvero, accesso condizionale). Tenere presente che questo vale sia app client toohello e toohello risorsa app. In tal caso, si supponga di che impostare un criterio di accesso condizionale che afferma che app "Office 365 Exchange Online" hello è accessibile solo da computer che sono conformi.  Questo criterio verrà attivato anche quando un utente tenta di toouse un'app client che richiede autorizzazioni tooExchange Online.



- Si ha la visibilità in cui le app sono state tooand stato fornito il consenso, quelle che sono in uso.

1.  Quando un utente acconsente tooan app, viene creato un oggetto entità servizio nel tenant di hello. Creazione di entità servizio è incluso nel report di controllo hello.
2.  Report attività di accesso utente indicano quale utente hello app accesso a. 

## <a name="example"></a>Esempio

Ad esempio, è opportuno app "FabrikamMail per Office 365" hello, che si notato accedono gli utenti nel tenant di a. "FabrikamMail" è un'app di lettura della posta elettronica per Android pubblicata da "Fabrikam, Inc.". Questo può essere suddiviso in hello "app multi-tenant altri sviluppare, che è possibile fornire il consenso per Contoso".

Se gli utenti sono autorizzati tooconsent, ricevono un hello dei messaggi di richiesta di consenso i prima volta, che effettuano l'accesso:![](media/active-directory-apps-permissions-consent/apps14.png)

"Accedere le cassette postali" è una stringa di consenso hello rivolta all'utente l'autorizzazione "Accesso alle cassette postali come utente connesso di hello" hello esposti da "Office 365 Exchange Online" (ovvero, Exchange).

È possibile visualizzare le autorizzazioni di hello cercando oggetto entità servizio hello per Exchange (risorsa hello), che è stato aggiunto al momento dell'iscrizione per Office 365. È possibile pensare oggetto entità servizio hello di un' "istanza" hello app nel tenant di cui viene utilizzato per la registrazione di configurazioni e le diverse opzioni.  È possibile vedere questo utilizzando hello `Get-AzureADServicePrincipal` in PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Consenso viene avviato quando l'utente hello fa clic su "Accetto". Innanzitutto, un oggetto entità servizio per "FabrikamMail per Office 365" viene creato nel tenant di hello. Hello ServicePrincipal simile al seguente:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Consenso app tooan crea un collegamento Oauth2PermissionGrant tra segue hello:
  
- oggetto utente Hello
- applicazioni client Hello ServicePrincipalName (SPN)
- Hello risorsa App ServicePrincipalName (SPN)
- autorizzazioni in app risorse hello.  

Nel caso di hello di FabrikamMail, simile al seguente:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** ID di oggetto principal del FabrikamMail servizio (Buongiorno quello appena creato), **PrincipalId** è l'ID di oggetto utente hello (di hello utente che ha concesso il consenso), **ResourceId**è servizio di Exchange ID oggetto dell'entità, l'ambito è l'autorizzazione di hello in Exchange che è stato concesso il consenso).

Se gli utenti non sono consentiti tooconsent, visualizzeranno una schermata in cui è indicato l'autorizzazione è necessaria.

