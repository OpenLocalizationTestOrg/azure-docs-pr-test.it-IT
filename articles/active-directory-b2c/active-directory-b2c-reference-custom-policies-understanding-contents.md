---
title: 'Azure Active B2C di Directory: Informazioni sui criteri personalizzati di pacchetto hello | Documenti Microsoft'
description: Un argomento sui criteri personalizzati di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Informazioni sui criteri personalizzati di hello del pacchetto hello Azure Active Directory B2C criteri personalizzati

Questa sezione sono elencati tutti gli elementi di base hello dei criteri di hello B2C_1A_base fornita con hello **principianti** e che viene utilizzata per la creazione di propri criteri tramite ereditarietà hello di hello *B2C_1A_base_ criteri di estensioni*.

Di conseguenza, più in particolare mette in hello già definito tipi, le trasformazioni di attestazioni, le definizioni di contenuto, i provider di attestazioni con i relativi profili tecnici di attestazione e hello viaggi utente core.

> [!IMPORTANT]
> Microsoft non rilascia alcuna garanzia, esplicita o implicita, riguardo toohello informazioni fornite di seguito. Potrebbero essere apportate modifiche in qualsiasi momento, prima della disponibilità a livello generale, al momento della disponibilità a livello generale o in seguito.

Propri criteri e hello B2C_1A_base_extensions criteri è possibile eseguire l'override di queste definizioni ed estendere questi criteri padre fornendo aggiuntive in base alle esigenze.

gli elementi principali di hello Hello *B2C_1A_base criteri* sono tipi di attestazione, le trasformazioni di attestazioni e le definizioni di contenuto. Questi elementi possono toobe soggetti a cui fa riferimento anche propri criteri come hello *B2C_1A_base_extensions criteri*.

## <a name="claims-schemas"></a>Schema delle attestazioni

Questo schema delle attestazioni è diviso in tre sezioni:

1.  Prima sezione in cui sono elencati hello minimo attestazioni richieste per hello utente viaggi toowork correttamente.
2.  Una seconda sezione che elenchi hello attestazioni richieste per i parametri di stringa di query e altri parametri speciali di toobe passato tooother dai provider di attestazioni, in particolare login.microsoftonline.com per l'autenticazione. **Non modificare queste attestazioni**.
3.  E infine una terza sezione che elenca tutte le attestazioni aggiuntive e facoltative che possono essere raccolti da utente hello, archiviati nella directory hello inviati nei token di accesso. È possibile aggiungere nuove attestazioni toobe tipo raccolti dall'utente hello e/o inviati nel token hello in questa sezione.

> [!IMPORTANT]
> schema di attestazioni Hello contiene restrizioni su determinate attestazioni, ad esempio nomi utente e password. criteri di attendibilità Framework (TF) Hello considera AD Azure come qualsiasi altro provider di attestazioni e tutte le relative restrizioni sono modellate in Criteri di hello premium. Un criterio potrebbe essere modificato tooadd più restrizioni o utilizzare un altro provider di attestazioni per l'archiviazione di credenziali che conterrà i proprio restrizioni.

tipi di attestazione disponibili Hello sono elencati di seguito.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Attestazioni necessarie per i percorsi utente hello

Hello seguendo le attestazioni è necessario per utente viaggi toowork correttamente:

| Tipo di attestazione | Descrizione |
|-------------|-------------|
| *UserId* | Nome utente |
| *signInName* | Nome di accesso |
| *tenantId* | Identificatore del tenant (ID) dell'oggetto utente hello in Azure Active Directory B2C Premium |
| *objectId* | Identificatore di oggetto (ID) dell'oggetto utente hello in Azure Active Directory B2C Premium |
| *password* | Password |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Criteri password utilizzati dalla complessità della password di Azure Active Directory B2C Premium toodetermine scadenza, e così via. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | Numero di telefono dell'utente |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | Indirizzo di posta elettronica che può essere utilizzato toocontact hello utente |
| *signInNamesInfo.emailAddress* | Indirizzo di posta elettronica hello utente può utilizzare toosign in |
| *otherMails* | Indirizzi di posta elettronica che possono essere utilizzato toocontact hello utente |
| *userPrincipalName* | Nome utente archiviato nella hello Premium di Azure Active Directory B2C |
| *upnUserName* | Nome utente per la creazione di nome dell'entità utente |
| *mailNickName* | Nome alternativo posta elettronica dell'utente archiviato nella hello Premium di Azure Active Directory B2C |
| *newUser* | |
| *executed-SelfAsserted-Input* | Attestazione che specifica se gli attributi sono stati raccolti dall'utente hello |
| *executed-PhoneFactor-Input* | Attestazione che specifica se è stato raccolto un numero di telefono da utente hello |
| *authenticationSource* | Specifica se l'utente hello è stato autenticato al Provider di identità di social networking, login.microsoftonline.com o un account locale |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Attestazioni necessarie per i parametri della stringa di query e altri parametri speciali

Hello attestazioni seguenti sono necessari toopass nel provider di attestazioni tooother parametri speciali (inclusi alcuni parametri di stringa di query).

| Tipo di attestazione | Descrizione |
|-------------|-------------|
| *nux* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *nca* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *prompt* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *mkt* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *lc* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *grant_type* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *scope* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *client_id* | Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale |
| *objectIdFromSession* | Parametro fornito dal hello predefinito sessione Gestione provider tooindicate che hello id di oggetto è stato recuperato da una sessione SSO |
| *isActiveMFASession* | Parametro fornito da hello MFA sessione gestione tooindicate che utente hello dispone di una sessione attiva di autenticazione a più fattori |

### <a name="additional-optional-claims-that-can-be-collected"></a>Attestazioni aggiuntive (facoltative) che possono essere raccolte

esempio Hello attestazioni sono attestazioni aggiuntive che possono essere raccolti da utenti hello, archiviati nella directory di hello e inviati nel token hello. Come descritto prima, possono essere aggiunte ulteriori attestazioni toothis elenco.

| Tipo di attestazione | Descrizione |
|-------------|-------------|
| *givenName* | Nome di battesimo dell'utente (noto anche come nome) |
| *surname* | Cognome dell'utente |
| *Extension_picture* | Immagine dell'utente da social network |

## <a name="claim-transformations"></a>Trasformazioni delle attestazioni

le trasformazioni delle attestazioni disponibili di Hello sono elencate di seguito.

| Trasformazione attestazione | Descrizione |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Definizioni del contenuto

Questa sezione vengono descritte le definizioni di hello contenuto già dichiarate in hello *B2C_1A_base* criteri. Queste definizioni di contenuto sono sensibili toobe a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.

| Provider di attestazioni | Descrizione |
|-----------------|-------------|
| *Facebook* | |
| *Accesso all'account locale* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Autocertificazione* | |
| *Account locale* | |
| *Gestione delle sessioni* | |
| *Motore di criteri Trustframework* | |
| *TechnicalProfiles* | |
| *Autorità emittente di token* | |

## <a name="technical-profiles"></a>Profili tecnici

In questa sezione illustra i profili di tecniche hello già dichiarati per ogni provider di attestazioni di hello *B2C_1A_base* criteri. Questi profili tecnici sono sensibili toobe ulteriormente a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.

### <a name="technical-profiles-for-facebook"></a>Profili tecnici per Facebook

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *Facebook-OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Profili tecnici per l'accesso all'account locale

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Profili tecnici per PhoneFactor

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Profili tecnici per Azure Active Directory

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *AAD-Common* | Profilo tecnico incluso da hello altri profili tecnici AAD-xxx |
| *AAD-UserWriteUsingAlternativeSecurityId* | Profilo tecnico per gli accessi basati su social network |
| *AAD-UserReadUsingAlternativeSecurityId* | Profilo tecnico per gli accessi basati su social network |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Profilo tecnico per gli accessi basati su social network |
| *AAD-UserWritePasswordUsingLogonEmail* | Profili tecnici per gli account locali |
| *AAD-UserReadUsingEmailAddress* | Profili tecnici per gli account locali |
| *AAD-UserWriteProfileUsingObjectId* | Profilo tecnico per aggiornare il record utente usando objectId |
| *AAD-UserWritePhoneNumberUsingObjectId* | Profilo tecnico per aggiornare il record utente usando objectId |
| *AAD-UserWritePasswordUsingObjectId* | Profilo tecnico per aggiornare il record utente usando objectId |
| *AAD-UserReadUsingObjectId* | Tecnica profilo è usato tooread dati dopo l'autenticazione dell'utente |

### <a name="technical-profiles-for-self-asserted"></a>Profili tecnici per l'autocertificazione

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Profili tecnici per l'account locale

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Profili tecnici per la gestione delle sessioni

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Nome del profilo è sta toodisambiguate utilizzati AAD sessione tra accesso ed eseguire l'accesso |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Profili tecnici per TechnicalProfiles del motore di criteri Trustframework

Attualmente, non tecnici profili definiti per hello **Trustframework criteri motore TechnicalProfiles** provider di attestazioni.

### <a name="technical-profiles-for-token-issuer"></a>Profili tecnici per l'autorità emittente di token

| Profilo tecnico | Descrizione |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Percorsi utente

In questa sezione illustra i percorsi utente hello già dichiarati in hello *B2C_1A_base* criteri. Questi percorsi utente sono sensibili toobe ulteriormente a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.

| Percorso utente | Descrizione |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
