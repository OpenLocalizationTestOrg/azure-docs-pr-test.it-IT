---
title: "Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati"
description: Un tooarticle procedura su come configurare ADFS 2016 utilizzando il protocollo SAML e i criteri personalizzati
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Questo articolo illustra come tooenable Accedi per gli utenti dall'account ADFS tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Prerequisiti

Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.

La procedura include i passaggi seguenti:

1.  Creazione di un trust della relying party di AD FS.
2.  Aggiunta di hello ADFS Trust della Relying Party certificato tooAzure Active Directory B2C.
3.  Aggiunta di criteri tooa di provider di attestazioni.
4.  Account di ad FS hello registrazione viaggio utente tooa di provider di attestazioni.
5.  Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate un Trust della Relying Party grado di riconoscere attestazioni

toouse ADFS come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un ADFS Trust della Relying Party e fornirlo con i parametri corretti hello.

tooadd nuovo relying party trust tramite lo snap-in Gestione ADFS hello Active Directory e configurare manualmente le impostazioni di hello, eseguire hello seguente procedura in un server federativo.

L'appartenenza a **amministratori**, o equivalente nel computer locale hello toocomplete necessari minimo hello questa procedura. Altre informazioni sull'uso degli account appropriati hello e appartenenze a [dominio gruppi predefiniti locali e](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  In Server Manager selezionare **Strumenti** e quindi **Gestione AD FS**.

2.  Fare clic su **Aggiungi attendibilità componente**.
    ![Aggiungi attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  In hello **iniziale** pagina, scegliere **grado di riconoscere attestazioni** e fare clic su **avviare**.
    ![Nella pagina di benvenuto hello, scegliere il grado di riconoscere attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  In hello **Seleziona origine dati** pagina, fare clic su **immettere manualmente i dati sulla relying party di hello**, quindi fare clic su **Avanti**.
    ![Immettere i dati sulla relying party di hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  In hello **Specifica nome visualizzato** , digitare un nome in **nome visualizzato**in **note** digitare una descrizione per questo trust della relying party e quindi fare clic su **successivo** .
    ![Specificare il nome visualizzato e le note](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Facoltativo. Se sono presenti un certificato di crittografia token facoltativa, quindi hello **Configura certificato** pagina, fare clic su **Sfoglia** toolocate il file di certificato e quindi fare clic su **Avanti** .
    ![Configura certificato](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  In hello **Configura URL** pagina, seleziona hello **abilitare il supporto per il protocollo SAML 2.0 WebSSO hello** casella di controllo. In **Relying party SAML 2.0 SSO service URL**, digitare l'URL dell'endpoint del servizio hello Security Assertion Markup Language (SAML) per questo trust della relying party e quindi fare clic su **Avanti**.  Per hello **Relying party SAML 2.0 SSO service URL**, incollare hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Sostituire {tenant} con il nome del tenant (ad esempio, contosob2c.onmicrosoft.com) e sostituire hello {criteri} con il nome del criterio estensioni (ad esempio, B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >nome del criterio Hello è hello uno da cui eredita criteri signup_or_signin, in questo caso è: `B2C_1A_TrustFrameworkExtensions`.
    >Ad esempio in cui potrebbe essere URL hello: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![Componente URL del servizio SAML 2.0 SSO](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. In hello **Configura identificatori** specificare hello stesso URL come passaggio precedente hello, fare clic su **Aggiungi** tooadd li toohello elenco e quindi fare clic su **Avanti**.
    ![Identificatori dell'attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  In hello **scegliere Criteri di controllo di accesso** selezionare un criterio e fare clic su **Avanti**.
    ![Scegli criteri di controllo di accesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  In hello **pronto tooAdd Trust** pagina, rivedere le impostazioni di hello e quindi fare clic su **Avanti** toosave la relying party trust informazioni.
    ![Salvare le informazioni sul trust della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  In hello **fine** pagina, fare clic su **Chiudi**, questa azione consente di visualizzare automaticamente hello **Modifica regole attestazione** la finestra di dialogo.
    Selezionare ![Modifica regole attestazione](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Fare clic su **Aggiungi regola**.  
      ![Aggiungi nuova regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  In **Modello di regola attestazione** selezionare **Inviare attributi LDAP come attestazioni**.
    ![Selezionare la regola modello Inviare attributi LDAP come attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Specificare **Nome regola attestazione**. Per hello **archivio attributi** selezionare **selezionare Active Directory** aggiungere hello seguendo le attestazioni, quindi fare clic su **fine** e **OK**.
    ![Impostare le proprietà di regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  In Server Manager, selezionare **Relying Party Trusts** selezionare hello trust della relying party è stato creato, quindi fare clic su **proprietà**.
    ![Proprietà di modifica della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Uno hello relying party trust (B2C Demo) finestra Proprietà selezionare **firma** scheda e fare clic su **Aggiungi**.  
    ![Imposta firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Aggiungere il certificato di firma (file con estensione CERT, senza chiave privata).  
    ![Aggiungere il certificato di firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Nella finestra dei comandi di hello relying party trust (B2C Demo) fare clic su **avanzate** scheda e modificare hello **algoritmo hash protetto** troppo**SHA-1**, fare clic su **Ok**.  
    ![Impostare l'algoritmo di hash protetto tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Aggiungere hello ADFS account applicazione chiave tooAzure AD B2C
Federazione con l'account ADFS richiede un segreto client per ad FS tootrust di account Azure Active Directory B2C per conto di un'applicazione hello. È necessario un certificato ADFS toostore nel tenant di Azure Active Directory B2C. 

1.  Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**
2.  Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.
3.  Fare clic su **+Aggiungi**.
4.  Per **Opzioni** usare **Carica**.
5.  Per **Nome** usare `ADFSSamlCert`.  
    prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.
6.  Nel caricamento del File hello, * * selezionare il file pfx del certificato con chiave privata. Nota: questo certificato (con la chiave privata hello) deve essere identico a quello che emesso e utilizzato per relying party ADFS hello hello.
![Carica chiave criteri](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Fare clic su **Crea**
8.  Verificare di aver creato la chiave hello `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Aggiungere un provider di attestazioni nei criteri di estensione
Se si desidera toosign gli utenti utilizzando l'account ADFS, è necessario account ADFS toodefine come provider di attestazioni. In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica. endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.

Definire AD FS come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:

1. Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro. Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.
2. Trovare hello `<ClaimsProviders>` sezione
3. Aggiungere hello seguente frammento di codice XML in hello `ClaimsProviders` elemento e sostituire `identityProvider` con il server DNS (valore arbitrario che indica il dominio), quindi salvare il file hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrare hello ADFS account attestazioni provider tooSign backup o accedere al proprio processo utente
A questo punto, il provider di identità hello è stato impostato.  Non è tuttavia disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello. È possibile procedere tooadd hello ADFS account identity provider tooyour utente `SignUpOrSignIn` viaggio utente. toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.  Quindi, abbiamo modificarlo in modo da includere il provider di identità ADFS hello:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).
2.  Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.
3.  Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento. Se non esiste l'elemento hello, aggiungerne uno.
4.  Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.  `<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi. Se si aggiunge un `<ClaimsProviderSelection>` elemento per conto ADFS, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello. tooadd questo elemento:

1.  Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.
2.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
3.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan

Ora che si dispone di un pulsante, è necessario toolink è tooan azione. azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con ADFS account tooreceive un token. Collegamento azione pulsante di hello tooan collegando profilo tecniche hello per il provider di attestazioni ADFS account:

1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello.
> * Verificare `TechnicalProfileReferenceId` è impostare il profilo di tecniche toohello precedenti (Contoso-SAML2) è stato creato.

## <a name="upload-hello-policy-tooyour-tenant"></a>Caricare tenant tooyour di hello criteri
1.  In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.
2.  Fare clic su **Framework dell'esperienza di gestione delle identità**.
3.  Aprire hello **tutti i criteri** blade.
4.  Selezionare **Carica criteri**.
5.  Controllare **sovrascrivere i criteri di hello eventuale** casella.
6.  **Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test dei criteri personalizzati di hello tramite Esegui
1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.
2.  Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con account ADFS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Facoltativo] Registrare viaggio di hello ADFS account attestazioni provider tooProfile modifica utente
È consigliabile provider di identità account ADFS hello tooadd anche tooyour utente `ProfileEdit` viaggio utente. toomake è disponibile, si ripete hello ultimi due passaggi:

### <a name="display-hello-button"></a>Pulsante di visualizzazione hello
1.  Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).
2.  Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.
3.  Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`
4.  Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Azione di collegamento hello pulsante tooan
1.  Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.
2.  Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui
1.  Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.
2.  Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.
3.  È necessario essere in grado di toosign con account ADFS.

## <a name="download-hello-complete-policy-files"></a>Scaricare i file di criteri completa hello
Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato l'introduzione a criteri personalizzati analizzerà hello. [File dei criteri di esempio solo per riferimento](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
