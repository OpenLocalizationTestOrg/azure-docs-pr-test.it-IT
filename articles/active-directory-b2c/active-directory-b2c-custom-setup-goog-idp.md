---
title: "Azure Active Directory B2C: Aggiungere Google+ come provider di identità OAuth2 tramite criteri personalizzati"
description: "Esempio di utilizzo di Google+ come provider di identità basato sul protocollo OAuth2"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Aggiungere Google+ come provider di identità OAuth2 tramite criteri personalizzati

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Questa guida viene spiegato come tooenable Accedi per gli utenti da Google + account tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Prerequisiti

Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.

La procedura include i passaggi seguenti:

1.  Creazione di un'applicazione di account Google+.
2.  Aggiunta di hello Google + account applicazione chiave tooAzure AD B2C
3.  Aggiunta di criteri tooa provider di attestazioni
4.  Registrazione hello Google + account attestazioni provider tooa utente viaggio
5.  Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test

## <a name="create-a-google-account-application"></a>Creare un'applicazione di account Google+
toouse Google + come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Google + e fornirlo con i parametri corretti hello. È possibile registrare un'applicazione Google+ qui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Passare toohello [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google +.
2.  Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.

3.  Fare clic su hello **menu progetti**.

    ![Account Google+ - Selezionare il progetto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Fare clic su hello  **+**  pulsante.

    ![Account Google+ - Creare un nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Fare clic su un **Nome progetto** e quindi su **Crea**.

    ![Account Google+ - Nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Attendere che il progetto hello è pronto e fare clic su hello **menu progetti**.

    ![Account di Google + - attendere il nuovo progetto toouse pronto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Fare clic sul nome del progetto.

    ![Account di Google + - nuovo progetto selezionare hello](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Fare clic su **API Manager** e quindi fare clic su **credenziali** nel riquadro di spostamento sinistro hello.
9.  Fare clic su hello **schermata consenso OAuth** scheda nella parte superiore di hello.

    ![Account Google+ - Impostare la schermata del consenso OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.

    ![Google+ - Credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.

    ![Google + - Creare nuove credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  In **Tipo di applicazione** selezionare **Applicazione Web**.

    ![Google+ - Selezionare il tipo di applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Fornire un **nome** per l'applicazione, immettere `https://login.microsoftonline.com` in hello **autorizzato JavaScript origins** , campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URI**campo. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com. Hello **{tenant}** valore è tra maiuscole e minuscole. Fare clic su **Crea**.

    ![Google+ - Specificare le origini JavaScript autorizzate e gli URI di reindirizzamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Copiare i valori hello di **Id Client** e **segreto Client**. È necessario Google + entrambi tooconfigure come provider di identità nel tenant. **Segreto client** è una credenziale di sicurezza importante.

    ![Google + - valori hello copia della chiave privata Client e l'Id client](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Aggiungere hello Google + account applicazione chiave tooAzure AD B2C
La federazione con Google + account richiede un segreto client per Google + account tootrust Azure Active Directory B2C per conto di un'applicazione hello. È necessario toostore il segreto dell'applicazione Google + nel tenant di Azure Active Directory B2C:  

1.  Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**
2.  Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.
3.  Fare clic su **+Aggiungi**.
4.  Per **Opzioni** usare **Manuale**.
5.  Per **Nome** usare `GoogleSecret`.  
    prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.
6.  In hello **Secret** , immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com
7.  Per **Uso chiave** usare **Firma**.
8.  Fare clic su **Crea**
9.  Verificare di aver creato la chiave hello `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Aggiungere un provider di attestazioni nei criteri di estensione

Se si desidera toosign gli utenti utilizzando account di Google +, è necessario toodefine Google + account come un provider di attestazioni. In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica. endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.

Definire l'account Google+ come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:

1.  Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro. Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.
2.  Trovare hello `<ClaimsProviders>` sezione
3.  Aggiungere hello seguente frammento di codice XML in hello `ClaimsProviders` elemento e sostituire `client_id` valore con Google + ID account personale dell'applicazione client prima di salvare il file hello.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrare hello Google + account attestazioni provider tooSign backup o accedere al proprio processo utente

configurare il provider di identità Hello.  Non è tuttavia disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello. Aggiungere hello Google + account identità tooyour utente del provider `SignUpOrSignIn` viaggio utente. toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.  È quindi possibile aggiungere hello Google + account provider di identità:

>[!NOTE]
>
>Se è stato copiato hello `<UserJourneys>` elemento dal file di base del file di estensione di criteri toohello (TrustFrameworkExtensions.xml), è possibile ignorare la sezione toothis.

1.  Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).
2.  Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.
3.  Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento. Se non esiste l'elemento hello, aggiungerne uno.
4.  Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.  `<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi. Se si aggiunge un `<ClaimsProviderSelection>` elemento per account di Google +, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello. tooadd questo elemento:

1.  Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.
2.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
3.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan
Ora che si dispone di un pulsante, è necessario toolink è tooan azione. azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Google + account tooreceive un token.

1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello
> * Verificare `TechnicalProfileReferenceId` impostare l'ID del profilo di tecniche toohello precedenti (Google OAUTH) è stato creato.

## <a name="upload-hello-policy-tooyour-tenant"></a>Caricare tenant tooyour di hello criteri
1.  In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.
2.  Fare clic su **Framework dell'esperienza di gestione delle identità**.
3.  Aprire hello **tutti i criteri** blade.
4.  Selezionare **Carica criteri**.
5.  Controllare **sovrascrivere i criteri di hello eventuale** casella.
6.  **Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test dei criteri personalizzati di hello tramite Esegui
1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.

    >[!NOTE]
    >
    >    **Esegui ora** richiede almeno un'applicazione toobe preregistrate tenant hello. 
    >    toolearn tooregister applicazioni, vedere hello Azure Active Directory B2C [iniziare](active-directory-b2c-get-started.md) articolo o hello [registrazione dell'applicazione](active-directory-b2c-app-registration.md) articolo.


2.  Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con Google + account.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Facoltativo] Registrare hello Google + account attestazioni provider tooProfile modifica utente viaggio
È consigliabile tooadd hello Google + account provider di identità anche tooyour utente `ProfileEdit` viaggio utente. toomake è disponibile, si ripete hello ultimi due passaggi:

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
1.  Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).
2.  Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.
3.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
4.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan
1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui

1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.
2.  Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con Google + account.

## <a name="download-hello-complete-policy-files"></a>Scaricare i file di criteri completa hello
Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato hello Introduzione a criteri personalizzati analizzerà anziché utilizzare questi file di esempio.  [File dei criteri di esempio di riferimento](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
