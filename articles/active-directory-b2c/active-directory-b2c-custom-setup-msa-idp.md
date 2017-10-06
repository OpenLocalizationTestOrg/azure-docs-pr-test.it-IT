---
title: "Azure Active Directory B2C: Aggiungere un account Microsoft come provider di identità tramite criteri personalizzati"
description: "Esempio di utilizzo di Microsoft come provider di identità basato sul protocollo OpenID Connect (OIDC)"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Aggiungere un account Microsoft come provider di identità tramite criteri personalizzati

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Questo articolo illustra come tooenable Accedi per gli utenti dall'account Microsoft (MSA) tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Prerequisiti
Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.

La procedura include i passaggi seguenti:

1.  Creazione di un'applicazione di account Microsoft.
2.  Aggiunta di hello Microsoft account applicazione chiave tooAzure AD B2C
3.  Aggiunta di criteri tooa provider di attestazioni
4.  Registrazione di viaggio di hello Account Microsoft attestazioni provider tooa utente
5.  Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test

## <a name="create-a-microsoft-account-application"></a>Creare un'applicazione di account Microsoft
toouse Microsoft account come un provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di account Microsoft e fornirlo con i parametri corretti hello. È necessario un account Microsoft. Se non si ha un account, visitare il sito [https://www.live.com/](https://www.live.com/).

1.  Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali dell'account Microsoft.
2.  Fare clic su **Aggiungi un'app**.

    ![Account Microsoft - Aggiungere un'app](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Specificare un **Nome** per l'applicazione e un **Indirizzo di posta elettronica di contatto**, deselezionare l'opzione **Informazioni per l'utilizzo iniziale** e fare clic su **Crea**.

    ![Account Microsoft - Registrare l'applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Copiare il valore di hello di **Id applicazione**. È necessario tooconfigure account Microsoft come provider di identità nel tenant.

    ![Account Microsoft - valore hello copia dell'Id applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Fare clic su **Aggiungi piattaforma**

    ![Account Microsoft - Aggiungi piattaforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Selezionare dall'elenco piattaforma hello **Web**.

    ![Account Microsoft - dall'elenco delle piattaforme hello scegliere Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** campo. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.

    ![Account Microsoft - Impostare gli URL di reindirizzamento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Fare clic su **generare una nuova Password** in hello **applicazione segreti** sezione. Copia hello nuova password visualizzata sullo schermo. È necessario tooconfigure account Microsoft come provider di identità nel tenant. La password è una credenziale di sicurezza importante.

    ![Account Microsoft - Genera nuova password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Account Microsoft - nuova password di copia hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Casella di controllo hello indicante **il supporto di Live SDK** in hello **opzioni avanzate** sezione. Fare clic su **Salva**.

    ![Account Microsoft - Supporto Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Aggiungere hello Microsoft account applicazione chiave tooAzure AD B2C
La federazione con l'account di Microsoft richiede un segreto client per tootrust di account di Microsoft Azure AD B2C per conto di un'applicazione hello. È necessario toostore il secert di applicazione Microsoft account nel tenant di Azure Active Directory B2C:   

1.  Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**
2.  Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.
3.  Fare clic su **+Aggiungi**.
4.  Per **Opzioni** usare **Manuale**.
5.  Per **Nome** usare `MSASecret`.  
    prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.
6.  In hello **Secret** , immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com
7.  Per **Uso chiave** usare **Firma**.
8.  Fare clic su **Crea**
9.  Verificare di aver creato la chiave hello `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Aggiungere un provider di attestazioni nei criteri di estensione
Se si desidera toosign gli utenti utilizzando l'Account Microsoft, è necessario toodefine Account Microsoft come provider di attestazioni. In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica. endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.

Definire l'account Microsoft come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:

1.  Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro. Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.
2.  Trovare hello `<ClaimsProviders>` sezione
3.  Aggiungere il seguente frammento di codice XML in hello `ClaimsProviders` elemento:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Sostituire il valore `client_id` con l'ID client dell'applicazione di account Microsoft

5.  Salvare il file hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrare hello Account Microsoft attestazioni provider tooSign backup oppure accedi viaggio utente

A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello. Ora è necessario tooadd hello Account Microsoft identity provider tooyour utente `SignUpOrSignIn` viaggio utente. toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.  È quindi possibile aggiungere provider di identità Account Microsoft hello:

> [!NOTE]
>
>Se è stato copiato in precedenza hello `<UserJourneys>` elemento dal file di base del file di estensione di criteri toohello `TrustFrameworkExtensions.xml`, è possibile ignorare la sezione toothis.

1.  Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).
2.  Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.
3.  Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento. Se non esiste l'elemento hello, aggiungerne uno.
4.  Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.  `<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi. Se si aggiunge un `<ClaimsProviderSelection>` elemento per l'account Microsoft, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello. tooadd questo elemento:

1.  Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.
2.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
3.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan
Ora che si dispone di un pulsante, è necessario toolink è tooan azione. azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Account Microsoft tooreceive un token. Collegamento azione tooan di hello pulsante profilo tecniche hello il collegamento per il provider di attestazioni di Account Microsoft:

1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello
>   * Verificare `TechnicalProfileReferenceId` impostare l'ID profilo di tecniche toohello creato precedenti (MSA OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Caricare tenant tooyour di hello criteri
1.  In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.
2.  Fare clic su **Framework dell'esperienza di gestione delle identità**.
3.  Aprire hello **tutti i criteri** blade.
4.  Selezionare **Carica criteri**.
5.  Controllare **sovrascrivere i criteri di hello eventuale** casella.
6.  **Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test dei criteri personalizzati di hello tramite Esegui

1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.
> [!NOTE]
>
>**Esegui ora** richiede almeno un'applicazione toobe preregistrate tenant hello. toolearn tooregister applicazioni, vedere hello Azure Active Directory B2C [iniziare](active-directory-b2c-get-started.md) articolo o hello [registrazione dell'applicazione](active-directory-b2c-app-registration.md) articolo.
2.  Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con account Microsoft.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Facoltativo] Registrare il viaggio utente tooProfile Modifica provider di hello Account Microsoft attestazioni
È consigliabile provider di identità Account Microsoft hello tooadd anche tooyour utente `ProfileEdit` viaggio utente. toomake è disponibile, si ripete hello ultimi due passaggi:

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
1.  Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).
2.  Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.
3.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
4.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan
1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui
1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.
2.  Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con account Microsoft.

## <a name="download-hello-complete-policy-files"></a>Scaricare i file di criteri completa hello
Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato hello Introduzione a criteri personalizzati analizzerà anziché utilizzare questi file di esempio.  [File dei criteri di esempio di riferimento](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
