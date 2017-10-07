---
title: 'Azure Active Directory B2C: aggiunta di un provider SAML Salesforce usando i criteri personalizzati | Microsoft Docs'
description: Per ulteriori informazioni vedere toocreate e gestire i criteri personalizzati di Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: eseguire l'accesso con account Salesforce tramite SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

In questo articolo illustra come toouse [criteri personalizzati](active-directory-b2c-overview-custom.md) tooset backup Accedi per gli utenti da un'organizzazione Salesforce specifico.

## <a name="prerequisites"></a>Prerequisiti

### <a name="azure-ad-b2c-setup"></a>Configurazione di Azure AD B2C

Assicurarsi di aver completato tutti i passaggi di hello che mostrano come troppo[Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).

incluse le seguenti:

* Creare un tenant di Azure AD B2C
* Creare un'applicazione Azure AD B2C
* Registrare due applicazioni con motore di criteri.
* Impostare le chiavi.
* Impostare il pacchetto hello.

### <a name="salesforce-setup"></a>Configurazione di Salesforce

In questo articolo si presuppone di aver già eseguito seguente hello:

* Iscrizione a un account Salesforce. È possibile iscriversi per ottenere un [account Developer Edition gratuito](https://developer.salesforce.com/signup).
* [Configurazione di un dominio personale](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) per la propria organizzazione Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Configurare Salesforce in modo che gli utenti possano eseguire la federazione

toohelp Azure Active Directory B2C comunicare con Salesforce, è necessario l'URL dei metadati di tooget hello Salesforce.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Configurare Salesforce come provider di identità

> [!NOTE]
> Questo articolo presuppone che si stia usando [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Accedi tooSalesforce](https://login.salesforce.com/). 
2. Nella hello sinistra dal menu in **impostazioni**, espandere **identità**, quindi fare clic su **Provider di identità**.
3. Fare clic su **Enable Identity Provider** (Abilita provider di identità).
4. In **certificato selezionare hello**, selezionare il certificato di hello desiderato toocommunicate toouse Salesforce con Azure Active Directory B2C. (È possibile utilizzare certificato predefinito hello). Fare clic su **Salva**. 

### <a name="create-a-connected-app-in-salesforce"></a>Creare un'app connessa in Salesforce

1. In hello **Provider di identità** pagina, andare troppo**i provider di servizi**.
2. Fare clic su **Service Providers are now created via Connected Apps. Click here** (I provider di servizi vengono ora creati tramite app connesse. Fare clic qui).
3. In **le informazioni di base**, immettere i valori hello necessario per l'app connessa.
4. In **impostazioni App Web**selezionare hello **Enable SAML** casella di controllo.
5. In hello **ID entità** immettere l'URL seguente hello. Assicurarsi di sostituire il valore di hello per `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. In hello **URL ACS** immettere l'URL seguente hello. Assicurarsi di sostituire il valore di hello per `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Lasciare i valori predefiniti di hello per tutte le altre impostazioni.
8. Scorrere fino alla fine di toohello dell'elenco di hello e quindi fare clic su **salvare**.

### <a name="get-hello-metadata-url"></a>Ottenere l'URL dei metadati hello

1. Nella pagina di panoramica hello dell'app connessa, fare clic su **Gestisci**.
2. Copiare il valore di hello per **Endpoint di individuazione dei metadati**, quindi salvarlo. Questo valore sarà usato più avanti in questo articolo.

### <a name="set-up-salesforce-users-toofederate"></a>Impostare toofederate agli utenti di Salesforce

1. In hello **Gestisci** pagina dell'app connessa, andare troppo**profili**.
2. Fare clic su **Manage Profiles** (Gestisci profili).
3. Selezionare i profili di hello (o gruppi di utenti) che si desidera toofederate con Azure Active Directory B2C. Come amministratore di sistema, selezionare hello **amministratore di sistema** casella di controllo in modo che è possibile attuare la federazione usando l'account di Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Generare un certificato di firma per Azure AD B2C

Le richieste inviate tooSalesforce necessità toobe firmato da Azure Active Directory B2C. toogenerate un certificato di firma, aprire Azure PowerShell e quindi eseguire hello i comandi seguenti.

> [!NOTE]
> Assicurarsi di aggiornare il nome di tenant hello e una password in due linee superiore hello.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Aggiungere hello SAML firma certificato tooAzure AD B2C

Caricare hello tenant di Azure Active Directory B2C tooyour certificato di firma: 

1. Passare il tenant di Azure Active Directory B2C tooyour. Fare clic su **Impostazioni** > **Framework dell'esperienza di gestione delle identità** > **Chiavi dei criteri**.
2. Fare clic su **+Aggiungi** e quindi eseguire le operazioni seguenti:
    1. Fare clic su **Opzioni** > **Carica**.
    2. Immettere un **Nome**, ad esempio SAMLSigningCert. prefisso Hello *B2C_1A_* viene aggiunto automaticamente toohello nome della chiave.
    3. tooselect il certificato, seleziona **file controllo caricamento**. 
    4. Immettere la password del certificato hello impostati nello script di PowerShell hello.
3. Fare clic su **Crea**.
4. Verificare di avere creato una chiave, ad esempio B2C_1A_SAMLSigningCert. Prendere nota del nome completo di hello (inclusi *B2C_1A_*). Si farà riferimento toothis chiave in un secondo momento nei criteri di hello.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Creare provider di attestazioni SAML Salesforce hello nei criteri di base

Consentire agli utenti di accedere con Salesforce, è necessario toodefine Salesforce come provider di attestazioni. In altre parole, è necessario endpoint hello toospecify comunicare con Azure Active Directory B2C. endpoint Hello verrà *fornire* un set di *attestazioni* che Azure Active Directory B2C utilizza tooverify che ha autenticato un utente specifico. toodo, aggiungere un `<ClaimsProvider>` per Salesforce nel file di estensione hello dei criteri:

1. Nella directory di lavoro, aprire il file di estensione hello (TrustFrameworkExtensions.xml).
2. Trovare hello `<ClaimsProviders>` sezione. Se non esiste, crearla nel nodo radice hello.
3. Aggiungere un nuovo `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

In hello `<ClaimsProvider>` nodo:

1. Modificare il valore di hello per `<Domain>` tooa un valore univoco che distingue `<ClaimsProvider>` da altri provider di identità.
2. Aggiornare il valore di hello per `<DisplayName>` tooa nome visualizzato hello provider di attestazioni. Questo valore non viene usato attualmente.

### <a name="update-hello-technical-profile"></a>Aggiornare il profilo tecnico hello

tooget un token SAML da Salesforce, definire i protocolli di hello che Azure Active Directory B2C utilizzerà toocommunicate con Azure Active Directory (Azure AD). Eseguire questa operazione in hello `<TechnicalProfile>` elemento `<ClaimsProvider>`:

1. Aggiornare l'ID di hello di hello `<TechnicalProfile>` nodo. Questo ID è utilizzato toorefer toothis profilo tecnica da altre parti del criterio hello.
2. Aggiornare il valore di hello per `<DisplayName>`. Questo valore viene visualizzato sul pulsante Accedi hello nella pagina di accesso.
3. Aggiornare il valore di hello per `<Description>`.
4. Salesforce utilizza il protocollo di hello SAML 2.0. Verificare che tale valore hello per `<Protocol>` è **SAML2**.

Hello aggiornamento `<Metadata>` sezione hello precedenti impostazioni di hello tooreflect XML per l'account di Salesforce specifico. Nel XML hello, aggiornare i valori dei metadati hello:

1. Aggiornare il valore di hello di `<Item Key="PartnerEntity">` con l'URL dei metadati di Salesforce hello copiato in precedenza. Dispone di hello seguente formato: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. In hello `<CryptographicKeys>` sezione aggiornamento hello valore per entrambe le istanze di `StorageReferenceId` toohello nome della chiave di hello del certificato di firma (ad esempio, B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Caricare il file di estensione hello per verifica

Il criterio è ora configurato in modo che Azure Active Directory B2C sa come toocommunicate con Salesforce. Provare a caricare il file di estensione hello dei criteri, che non vi siano problemi finora tooverify. file di estensione hello tooupload dei criteri:

1. Nel tenant di Azure Active Directory B2C, visitare toohello **tutti i criteri** blade.
2. Seleziona hello **sovrascrivere i criteri di hello eventuale** casella di controllo.
3. Caricare il file di estensione hello (TrustFrameworkExtensions.xml). Verificare che la relativa convalida abbia esito positivo.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Registrare hello viaggio di Salesforce SAML attestazioni provider tooa utente

Successivamente, aggiungere hello tooone di provider di identità SAML Salesforce di viaggi l'utente. A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in uno qualsiasi di pagine di iscrizione o accesso utente hello. tooadd hello identity provider tooa pagina di accesso, creare innanzitutto un duplicato di un proprio processo utente di modello esistente. Quindi, modificare il modello di hello in modo che include anche i provider di identità hello Azure AD.

1. Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).
2. Trovare hello `<UserJourneys>` elemento, quindi hello copia intera `<UserJourney>` valore, inclusi Id = "SignUpOrSignIn".
3. Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml). Trovare hello `<UserJourneys>` elemento. Se l'elemento hello non esiste, crearne uno.
4. Intero hello Incolla copiato `<UserJourney>` come figlio di hello `<UserJourneys>` elemento.
5. Rinominare ID hello di hello nuova `<UserJourney>` (ad esempio, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Pulsante di visualizzazione hello identity provider

Hello `<ClaimsProviderSelection>` elemento è di pulsante di provider di identità tooan analoghi in una pagina di iscrizione o accesso. Aggiungendo un `<ClaimsProviderSelection>` viene visualizzato un pulsante nuovo elemento per Salesforce, quando un utente passa alla pagina toothis. pulsante del provider toodisplay hello identità:

1. In hello `<UserJourney>` creato, trovare hello `<OrchestrationStep>` con `Order="1"`.
2. Aggiungere hello XML seguente:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Impostare `TargetClaimsExchangeId` valore logico tooa. È consigliabile seguente hello stessa convenzione di altri utenti (ad esempio,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Azione del collegamento hello identity provider pulsante tooan

Ora che si dispone di un pulsante di provider di identità, collegarlo tooan azione. In questo caso, l'azione di hello è per Azure Active Directory B2C toocommunicate con Salesforce tooreceive un token SAML. È possibile farlo mediante il collegamento profilo tecniche hello per le SAML Salesforce provider di attestazioni:

1. In hello `<UserJourney>` nodo, hello trova `<OrchestrationStep>` con `Order="2"`.
2. Aggiungere hello XML seguente:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Aggiornamento `Id` toohello stesso valore che è stato utilizzato in precedenza per `TargetClaimsExchangeId`.
4. Aggiornamento `TechnicalProfileReferenceId` toohello `Id` di hello tecnica profilo creato in precedenza (ad esempio, ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Caricare il file di estensione aggiornata hello

La modifica dei file di estensione hello termine. Salvare e caricare il file. Verificare che tutte le convalide abbiano esito positivo.

### <a name="update-hello-relying-party-file"></a>Aggiornare il file di hello relying party

Successivamente, aggiornare hello relying party (RP) file che avvia viaggio utente hello creato:

1. Creare una copia di SignUpOrSignIn.xml nella directory di lavoro. Rinominare quindi il file, ad esempio SignUpOrSignInWithAAD.xml.
2. Hello di file e aggiornamento nuovo hello aprire `PolicyId` attributo per `<TrustFrameworkPolicy>` con un valore univoco. Questo è il nome di hello dei criteri (ad esempio, SignUpOrSignInWithAAD).
3. Modificare hello `ReferenceId` attributo `<DefaultUserJourney>` toomatch hello `Id` del viaggio utente nuovo hello creato (ad esempio, SignUpOrSignUsingContoso).
4. Salvare le modifiche e quindi caricare il file hello.

## <a name="test-and-troubleshoot"></a>Testare e risolvere i problemi

andare a pannello criteri toohello, tootest hello criteri personalizzati appena caricato, nel portale di Azure, hello e quindi fare clic su **Esegui**. Se i test hanno esito negativo, vedere l'articolo sulla [risoluzione dei problemi relativi a criteri personalizzati](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Passaggi successivi

Fornire commenti e suggerimenti troppo[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
