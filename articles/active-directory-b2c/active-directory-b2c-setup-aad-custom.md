---
title: 'Azure Active Directory B2C: aggiungere un provider di Azure AD usando i criteri personalizzati | Microsoft Docs'
description: Informazioni sui criteri personalizzati di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: accedere usando account di Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Questo articolo illustra come tooenable Accedi per gli utenti da un'organizzazione di Azure Active Directory (Azure AD) specifico tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Prerequisiti

Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.

La procedura include i passaggi seguenti:

1. Creazione di un tenant di Azure Active Directory B2C (Azure AD B2C).
2. Creazione di un'applicazione Azure AD B2C.
3. Registrazione di due applicazioni del motore di criteri.
4. Configurazione delle chiavi.
5. Configurazione di pacchetto hello.

## <a name="create-an-azure-ad-app"></a>Creare un'app di Azure AD

tooenable Accedi per gli utenti da uno specifico dell'organizzazione di Azure AD, è necessario tooregister un'applicazione nel tenant di hello Azure AD dell'organizzazione.

>[!NOTE]
> Utilizziamo "contoso.com" per il tenant di Azure AD dell'organizzazione hello e "fabrikamb2c.onmicrosoft.com" come tenant di Azure Active Directory B2C hello in hello attenendosi alle istruzioni.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
1. Nella barra superiore hello, selezionare l'account. Da hello **Directory** scegliere tenant hello Azure AD dell'organizzazione in cui si desidera tooregister dell'applicazione (contoso.com).
1. Selezionare **più servizi** nel riquadro sinistro di hello e cercare "Registrazioni di App".
1. Selezionare **Registrazione nuova applicazione**.
1. Immettere un nome per l'applicazione, ad esempio `Azure AD B2C App`.
1. Selezionare **app Web / API** per il tipo di applicazione hello.
1. Per **Sign-on URL**, immettere hello seguente URL, in cui `yourtenant` viene sostituito dal nome hello del tenant di Azure Active Directory B2C (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Salvare l'ID applicazione hello.
1. Selezionare un'applicazione hello appena creato.
1. In hello **impostazioni** pannello seleziona **chiavi**.
1. Creare una nuova chiave e salvarla. Verrà utilizzato nei passaggi hello nella sezione successiva hello.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Aggiungere tooAzure chiave hello AD Azure Active Directory B2C

È necessario toostore chiave dell'applicazione hello contoso.com nel tenant di Azure Active Directory B2C. toodo questo:
1. Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **identità esperienza Framework** > **chiavi dei criteri**.
1. Selezionare **+Aggiungi**.
1. Selezionare o immettere queste opzioni:
   * Selezionare **Manuale**.
   * Per **Nome** scegliere un nome che corrisponda al nome del tenant di Azure AD, ad esempio `ContosoAppSecret`.  prefisso Hello `B2C_1A_` viene aggiunto automaticamente toohello nome della chiave.
   * Incollare la chiave applicazione hello **Secret** casella.
   * Selezionare **Firma**.
1. Selezionare **Crea**.
1. Verificare di aver creato la chiave hello `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Aggiungere un provider di attestazioni nel criterio di base

Se si desidera toosign gli utenti grazie ad Azure AD, è necessario toodefine Azure AD come provider di attestazioni. In altre parole, è necessario un endpoint di Azure Active Directory B2C con cui comunicherà toospecify. endpoint Hello fornirà un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico. 

È possibile definire Azure AD come provider di attestazioni tramite l'aggiunta di Azure AD toohello `<ClaimsProvider>` nodo nel file di estensione hello dei criteri:

1. Aprire il file di estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro.
1. Trovare hello `<ClaimsProviders>` sezione. Se non esiste, aggiungerla nel nodo radice hello.
1. Aggiungere un nuovo nodo `<ClaimsProvider>` come mostrato di seguito:

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. In hello `<ClaimsProvider>` valore hello di aggiornamento per nodo `<Domain>` tooa un valore univoco che può essere toodistinguish utilizzato da altri provider di identità.
1. In hello `<ClaimsProvider>` valore hello di aggiornamento per nodo `<DisplayName>` tooa nome descrittivo per hello provider di attestazioni. Questo valore non è attualmente usato.

### <a name="update-hello-technical-profile"></a>Aggiornare il profilo tecnico hello

un token dall'endpoint di Azure AD hello tooget, è necessario protocolli hello toodefine che Azure Active Directory B2C deve utilizzare toocommunicate con Azure AD. Questa operazione viene eseguita all'interno di hello `<TechnicalProfile>` elemento `<ClaimsProvider>`.
1. Aggiornare l'ID di hello di hello `<TechnicalProfile>` nodo. Questo ID è utilizzato toorefer toothis profilo tecnica da altre parti del criterio hello.
1. Aggiornare il valore di hello per `<DisplayName>`. Questo valore verrà visualizzato sul pulsante Accedi hello sullo schermo Accedi.
1. Aggiornare il valore di hello per `<Description>`.
1. Azure AD Usa protocollo OpenID Connect hello, verificare il valore di hello per `<Protocol>` è `"OpenIdConnect"`.

È necessario tooupdate hello `<Metadata>` sezione nel file XML di hello cui le impostazioni di configurazione tooearlier tooreflect hello per specifico tenant di Azure AD. Nel file XML di hello, aggiornare i valori dei metadati hello come segue:

1. Impostare `<Item Key="METADATA">` troppo`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, dove `yourAzureADtenant` è il nome di tenant di Azure AD (contoso.com).
1. Aprire il toohello browser e andare `METADATA` URL che hai appena aggiornato.
1. Nel browser hello, cercare l'oggetto 'issuer' hello e copiare il relativo valore. Dovrebbe essere simile al seguente hello: `https://sts.windows.net/{tenantId}/`.
1. Incollare il valore di hello per `<Item Key="ProviderName">` nel file XML di hello.
1. Impostare `<Item Key="client_id">` ID applicazione toohello dalla registrazione dell'app hello.
1. Impostare `<Item Key="IdTokenAudience">` ID applicazione toohello dalla registrazione dell'app hello.
1. Verificare che `<Item Key="response_types">` è troppo`id_token`.
1. Verificare che `<Item Key="UsePolicyInRedirectUri">` è troppo`false`.

È inoltre necessario segreto hello Azure AD toolink registrate nel toohello di tenant Azure AD di Azure Active Directory B2C `<ClaimsProvider>` informazioni:

* In hello `<CryptographicKeys>` sezione hello precedente file XML, aggiornare il valore di hello per `StorageReferenceId` toohello ID di riferimento del segreto hello è definito (ad esempio, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Caricare il file di estensione hello per verifica

A questo punto, sono stati configurati i criteri in modo che Azure Active Directory B2C sa come toocommunicate con la directory di Azure AD. Provare a caricare il file di estensione hello di tooconfirm di solo i criteri che non vi siano finora eventuali problemi. toodo in modo:

1. Aprire hello **tutti i criteri** pannello nel tenant di Azure Active Directory B2C.
1. Controllare hello **sovrascrivere i criteri di hello eventuale** casella.
1. Caricare il file di estensione hello (TrustFrameworkExtensions.xml) e assicurarsi che non riuscire convalida hello.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Registrare il viaggio utente tooa provider di hello Azure AD attestazioni

È ora necessario tooadd hello Azure AD identity provider tooone di viaggi l'utente. A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello. toomake è disponibile, verrà creato un duplicato di un proprio processo utente di modello esistente e quindi modificarlo in modo che include anche i provider di identità hello Azure AD:

1. Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).
1. Trovare hello `<UserJourneys>` elemento e copia hello intero `<UserJourney>` nodo che include `Id="SignUpOrSignIn"`.
1. Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento. Se non esiste l'elemento hello, aggiungerne uno.
1. Hello Incolla intero `<UserJourney>` nodo copiato come figlio di hello `<UserJourneys>` elemento.
1. Rinominare ID hello del viaggio di hello nuovo utente (ad esempio, rinominare come `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Hello visualizzato "pulsante"

Hello `<ClaimsProviderSelection>` elemento è di pulsante di provider di identità tooan analoghi in una schermata di sign-configurazione/Accedi. Se si aggiunge un `<ClaimsProviderSelection>` elemento per Azure AD, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello. tooadd questo elemento:

1. Trovare hello `<OrchestrationStep>` nodo che include `Order="1"` in viaggio utente hello appena creato.
1. Aggiungere hello seguente:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Impostare `TargetClaimsExchangeId` tooan di valore appropriato. È consigliabile seguente hello stessa convenzione come altri:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan

Ora che si dispone di un pulsante, è necessario toolink è tooan azione. azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Azure AD tooreceive un token. Collegamento azione pulsante di hello tooan collegando profilo tecniche hello per il provider di attestazioni di Azure AD:

1. Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
1. Aggiungere hello seguente:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Aggiornamento `Id` toohello lo stesso valore di `TargetClaimsExchangeId` nella precedente sezione hello.
1. Aggiornamento `TechnicalProfileReferenceId` toohello ID di hello tecnica profilo creato in precedenza (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Caricare il file di estensione aggiornata hello

La modifica dei file di estensione hello termine. Salvare il file. Quindi caricare il file hello e assicurarsi che tutte le convalide esito positivo.

### <a name="update-hello-rp-file"></a>File di aggiornamento hello RP

È ora necessario tooupdate hello relying party (RP) file avvierà viaggio utente hello appena creato:

1. Creare una copia di SignUpOrSignIn.xml nella directory di lavoro e rinominarlo (ad esempio, rinominarla tooSignUpOrSignInWithAAD.xml).
1. Hello di file e aggiornamento nuovo hello aprire `PolicyId` attributo per `<TrustFrameworkPolicy>` con un valore univoco (ad esempio, SignUpOrSignInWithAAD). <br> Questo sarà il nome di hello dei criteri (ad esempio, B2C\_1A\_SignUpOrSignInWithAAD).
1. Modificare hello `ReferenceId` attributo `<DefaultUserJourney>` toomatch hello ID di hello nuovo utente proprio processo creato (SignUpOrSignUsingContoso).
1. Salvare le modifiche e caricare file hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Testare i criteri personalizzati hello appena caricato il pannello e facendo clic su **Esegui**. informazioni su problemi toodiagnose, [risoluzione dei problemi](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Passaggi successivi

Fornire commenti e suggerimenti troppo[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
