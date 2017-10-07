---
title: 'Azure Active Directory B2C: modificare l''iscrizione nei criteri personalizzati e configurare il provider di autocertificazione'
description: Una procedura dettagliata sull'aggiunta di attestazioni toosign backup e configurare l'input dell'utente hello
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="49b12-103">Azure Active B2C di Directory: Modificare l'iscrizione tooadd nuove attestazioni e configurare l'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="49b12-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="49b12-104">In questo articolo, si aggiungerà un utente viaggio nuovo fornito dall'utente (un'attestazione) voce tooyour iscrizione.</span><span class="sxs-lookup"><span data-stu-id="49b12-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="49b12-105">Verrà configurare voce hello come un elenco a discesa e definire se necessario.</span><span class="sxs-lookup"><span data-stu-id="49b12-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="49b12-106">Modificato da Sipi tootrigger test uniforme.</span><span class="sxs-lookup"><span data-stu-id="49b12-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49b12-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="49b12-107">Prerequisites</span></span>

* <span data-ttu-id="49b12-108">Hello completato i passaggi nell'articolo hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="49b12-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="49b12-109">Test hello iscrizione/signin utente viaggio toosignup un nuovo account locale prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="49b12-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="49b12-110">La raccolta dei dati iniziali dagli utenti avviene mediante l'iscrizione/accesso.</span><span class="sxs-lookup"><span data-stu-id="49b12-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="49b12-111">In un secondo momento è possibile raccogliere attestazioni aggiuntive tramite i percorsi utente di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="49b12-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="49b12-112">Ogni volta che Azure Active Directory B2C raccoglie le informazioni direttamente dai utente hello in modo interattivo, hello Usa identità esperienza Framework relativi `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="49b12-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="49b12-113">passaggi di Hello riportati di seguito si applicano ogni volta che questo provider viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="49b12-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="49b12-114">Definire hello attestazione, il relativo nome visualizzato e hello il tipo di input dell'utente</span><span class="sxs-lookup"><span data-stu-id="49b12-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="49b12-115">Consente di chiedere utente hello per le città.</span><span class="sxs-lookup"><span data-stu-id="49b12-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="49b12-116">Aggiungere hello seguente elemento toohello `<ClaimsSchema>` elemento nel file di criteri TrustFrameWorkExtensions hello:</span><span class="sxs-lookup"><span data-stu-id="49b12-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="49b12-117">Sono disponibili opzioni aggiuntive, che è possibile apportare qui toocustomize hello attestazione.</span><span class="sxs-lookup"><span data-stu-id="49b12-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="49b12-118">Per uno schema completo, vedere toohello **identità esperienza Framework Guida di riferimento tecnico**.</span><span class="sxs-lookup"><span data-stu-id="49b12-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="49b12-119">Questa Guida verrà pubblicata non appena nella sezione di riferimento hello.</span><span class="sxs-lookup"><span data-stu-id="49b12-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="49b12-120">`<DisplayName>`è una stringa che definisce rivolta all'utente di hello *etichetta*</span><span class="sxs-lookup"><span data-stu-id="49b12-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="49b12-121">`<UserHelpText>`Consente di comprendere i requisiti utente hello</span><span class="sxs-lookup"><span data-stu-id="49b12-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="49b12-122">`<UserInputType>`è stato hello seguenti quattro opzioni evidenziato di seguito:</span><span class="sxs-lookup"><span data-stu-id="49b12-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="49b12-123">`RadioSingleSelectduration` applica una selezione singola.</span><span class="sxs-lookup"><span data-stu-id="49b12-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="49b12-124">`DropdownSingleSelect`-Consente di selezionare hello unico valore valido.</span><span class="sxs-lookup"><span data-stu-id="49b12-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Screenshot dell'opzione nell'elenco a discesa](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="49b12-126">`CheckboxMultiSelect`Consente la selezione di hello di uno o più valori.</span><span class="sxs-lookup"><span data-stu-id="49b12-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Screenshot dell'opzione di selezione multipla](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="49b12-128">Aggiungere hello attestazione toohello sign up/sign in viaggio utente</span><span class="sxs-lookup"><span data-stu-id="49b12-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="49b12-129">Attestazione hello come aggiungere un `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (trovato nel file di criteri TrustFrameworkBase hello).</span><span class="sxs-lookup"><span data-stu-id="49b12-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="49b12-130">Si noti che il TechnicalProfile utilizza hello SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="49b12-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="49b12-131">Aggiungere hello attestazione toohello AAD UserWriteUsingLogonEmail come un `<PersistedClaim ClaimTypeReferenceId="city" />` directory AAD toohello toowrite hello attestazione dopo la raccolta utente hello.</span><span class="sxs-lookup"><span data-stu-id="49b12-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="49b12-132">È possibile saltare questo passaggio se si preferisce non toopersist hello attestazione nella directory hello per utilizzi futuri.</span><span class="sxs-lookup"><span data-stu-id="49b12-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="49b12-133">Aggiungere hello attestazione toohello TechnicalProfile che legge dalla directory hello quando un utente effettua l'accesso come un`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="49b12-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="49b12-134">Aggiungere hello `<OutputClaim ClaimTypeReferenceId="city" />` file dei criteri RP toohello SignUporSignIn.xml questa attestazione viene inviato l'applicazione toohello token hello dopo viaggio un utente ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="49b12-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="49b12-135">Criterio personalizzato di test hello tramite "Esegui"</span><span class="sxs-lookup"><span data-stu-id="49b12-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="49b12-136">Aprire hello **Pannello di Azure Active Directory B2C** e passare troppo**identità esperienza Framework > criteri personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="49b12-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="49b12-137">Selezionare i criteri personalizzati hello caricato, quindi scegliere hello **Esegui ora** pulsante.</span><span class="sxs-lookup"><span data-stu-id="49b12-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="49b12-138">È necessario essere in grado di toosign utilizzando un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="49b12-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="49b12-139">schermata di iscrizione Hello in modalità test dovrebbe essere simile toothis:</span><span class="sxs-lookup"><span data-stu-id="49b12-139">hello signup screen in test mode should look similar toothis:</span></span>

![Screenshot dell'opzione di iscrizione modificata](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="49b12-141">Hello token tooyour indietro applicazione includeranno ora hello `city` attestazione come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="49b12-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="49b12-142">Facoltativo: Rimuovere la verifica di posta elettronica dal percorso di iscrizione</span><span class="sxs-lookup"><span data-stu-id="49b12-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="49b12-143">verifica della posta elettronica tooskip, l'autore dei criteri hello possibile tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="49b12-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="49b12-144">Hello indirizzo di posta elettronica verrà richiesto ma non verificato, a meno che non "Obbligatorio" = true viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="49b12-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="49b12-145">Valutare attentamente se questa opzione è adatta ai casi d'uso.</span><span class="sxs-lookup"><span data-stu-id="49b12-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="49b12-146">Verifica posta elettronica è abilitata per impostazione predefinita in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` nel file di criteri hello TrustFrameworkBase nel pacchetto hello:</span><span class="sxs-lookup"><span data-stu-id="49b12-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="49b12-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49b12-147">Next steps</span></span>

<span data-ttu-id="49b12-148">Aggiungere hello nuova attestazione toohello flussi per gli account di accesso account social modificando hello TechnicalProfiles elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="49b12-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="49b12-149">Questi sono utilizzati toowrite gli account di accesso account sociale o federata e leggere i dati utente hello utilizzando alternativeSecurityId hello come hello localizzatore.</span><span class="sxs-lookup"><span data-stu-id="49b12-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
