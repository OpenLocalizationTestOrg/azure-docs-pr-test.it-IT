---
title: 'Azure Active Directory B2C: modificare l''iscrizione nei criteri personalizzati e configurare il provider di autocertificazione'
description: Procedura dettagliata relativa all'aggiunta di attestazioni all'iscrizione e alla configurazione dell'input utente
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="59bb0-103">Azure Active Directory B2C: modificare l'iscrizione per aggiungere nuove attestazioni e configurare l'input utente.</span><span class="sxs-lookup"><span data-stu-id="59bb0-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="59bb0-104">Questo articolo illustra come aggiungere una nuova voce specificata dall'utente, un'attestazione, al percorso utente di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="59bb0-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="59bb0-105">La voce verrà configurata come elenco a discesa e verrà indicato se è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="59bb0-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="59bb0-106">Modificato da Sipi per attivare la consegna di test.</span><span class="sxs-lookup"><span data-stu-id="59bb0-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59bb0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="59bb0-107">Prerequisites</span></span>

* <span data-ttu-id="59bb0-108">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="59bb0-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="59bb0-109">Prima di procedere, testare il percorso utente di iscrizione/accesso per l'iscrizione di un nuovo account locale.</span><span class="sxs-lookup"><span data-stu-id="59bb0-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="59bb0-110">La raccolta dei dati iniziali dagli utenti avviene mediante l'iscrizione/accesso.</span><span class="sxs-lookup"><span data-stu-id="59bb0-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="59bb0-111">In un secondo momento è possibile raccogliere attestazioni aggiuntive tramite i percorsi utente di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="59bb0-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="59bb0-112">Ogni volta che Azure AD B2C raccoglie informazioni direttamente dall'utente in modo interattivo, il framework dell'esperienza di gestione delle identità usa il relativo `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="59bb0-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="59bb0-113">I passaggi seguenti si applicano ogni volta che tale provider viene usato.</span><span class="sxs-lookup"><span data-stu-id="59bb0-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="59bb0-114">Definire l'attestazione, il nome visualizzato e il tipo di input utente</span><span class="sxs-lookup"><span data-stu-id="59bb0-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="59bb0-115">Per chiedere all'utente di indicare la propria città,</span><span class="sxs-lookup"><span data-stu-id="59bb0-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="59bb0-116">aggiungere l'elemento seguente all'elemento `<ClaimsSchema>` nel file dei criteri TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="59bb0-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="59bb0-117">Sono disponibili opzioni aggiuntive che è possibile definire qui per personalizzare l'attestazione.</span><span class="sxs-lookup"><span data-stu-id="59bb0-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="59bb0-118">Per uno schema completo, vedere il documento **Identity Experience Framework Technical Reference Guide** (Guida di riferimento tecnico al framework dell'esperienza di gestione delle identità),</span><span class="sxs-lookup"><span data-stu-id="59bb0-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="59bb0-119">che verrà presto pubblicata nella sezione dei riferimenti.</span><span class="sxs-lookup"><span data-stu-id="59bb0-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="59bb0-120">`<DisplayName>` è una stringa che definisce l'*etichetta* destinata all'utente.</span><span class="sxs-lookup"><span data-stu-id="59bb0-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="59bb0-121">`<UserHelpText>` consente all'utente di identificare i requisiti.</span><span class="sxs-lookup"><span data-stu-id="59bb0-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="59bb0-122">`<UserInputType>` include le quattro opzioni evidenziate di seguito.</span><span class="sxs-lookup"><span data-stu-id="59bb0-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="59bb0-123">`RadioSingleSelectduration` applica una selezione singola.</span><span class="sxs-lookup"><span data-stu-id="59bb0-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="59bb0-124">`DropdownSingleSelect` consente di selezionare solo valori validi.</span><span class="sxs-lookup"><span data-stu-id="59bb0-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="59bb0-126">`CheckboxMultiSelect` consente di selezionare uno o più valori.</span><span class="sxs-lookup"><span data-stu-id="59bb0-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="59bb0-128">Aggiungere l'attestazione al percorso utente di iscrizione/accesso</span><span class="sxs-lookup"><span data-stu-id="59bb0-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="59bb0-129">Aggiungere l'attestazione come `<OutputClaim ClaimTypeReferenceId="city"/>` all'oggetto TechnicalProfile `LocalAccountSignUpWithLogonEmail` incluso nel file dei criteri TrustFrameworkBase.</span><span class="sxs-lookup"><span data-stu-id="59bb0-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="59bb0-130">Si noti che TechnicalProfile qui usa SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="59bb0-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="59bb0-131">Aggiungere l'attestazione ad AAD-UserWriteUsingLogonEmail come `<PersistedClaim ClaimTypeReferenceId="city" />` per scrivere l'attestazione nella directory di AAD dopo averla raccolta dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59bb0-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="59bb0-132">Se non si vuole mantenere l'attestazione nella directory per un uso futuro, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="59bb0-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="59bb0-133">Aggiungere l'attestazione all'oggetto TechnicalProfile che legge dalla directory quando un utente esegue l'accesso come `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="59bb0-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="59bb0-134">Aggiungere `<OutputClaim ClaimTypeReferenceId="city" />` al file dei criteri relying party SignUporSignIn.xml in modo che l'attestazione venga inviata all'applicazione nel token quando il percorso utente ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="59bb0-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="59bb0-135">Testare i criteri personalizzati tramite "Esegui adesso"</span><span class="sxs-lookup"><span data-stu-id="59bb0-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="59bb0-136">Aprire il pannello **Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità > Criteri personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="59bb0-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="59bb0-137">Selezionare il criterio personalizzato che è stato caricato e fare clic sul pulsante **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="59bb0-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="59bb0-138">Dovrebbe essere possibile iscriversi usando un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="59bb0-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="59bb0-139">La schermata di iscrizione in modalità di test avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="59bb0-139">The signup screen in test mode should look similar to this:</span></span>

![Screenshot dell'opzione di iscrizione modificata](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="59bb0-141">Il token restituito all'applicazione ora include l'attestazione `city`, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="59bb0-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="59bb0-142">Facoltativo: Rimuovere la verifica di posta elettronica dal percorso di iscrizione</span><span class="sxs-lookup"><span data-stu-id="59bb0-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="59bb0-143">Per ignorare la verifica di posta elettronica, l'autore dei criteri può scegliere di rimuovere `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="59bb0-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="59bb0-144">L'indirizzo di posta elettronica verrà richiesto ma non verificato, a meno che "Required" = true non venga rimosso.</span><span class="sxs-lookup"><span data-stu-id="59bb0-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="59bb0-145">Valutare attentamente se questa opzione è adatta ai casi d'uso.</span><span class="sxs-lookup"><span data-stu-id="59bb0-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="59bb0-146">La verifica di posta elettronica è abilitata per impostazione predefinita in `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` nel file dei criteri TrustFrameworkBase nel pacchetto iniziale:</span><span class="sxs-lookup"><span data-stu-id="59bb0-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="59bb0-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59bb0-147">Next steps</span></span>

<span data-ttu-id="59bb0-148">Aggiungere la nuova attestazione ai flussi per gli accessi con account di social networking modificando gli elementi TechnicalProfile elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="59bb0-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="59bb0-149">Questi vengono usati per gli accessi con account di social networking/federati per scrivere e leggere i dati utente usando alternativeSecurityId come localizzatore.</span><span class="sxs-lookup"><span data-stu-id="59bb0-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
