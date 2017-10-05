---
title: 'Azure Active Directory B2C: Aggiungere attributi a criteri personalizzati e usarli nella modifica del profilo | Microsoft Docs'
description: "Procedura dettagliata che illustra come usare proprietà di estensione e attributi personalizzati e includerli nell'interfaccia utente"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="7a40a-103">Azure Active Directory B2C: Creazione e utilizzo di attributi personalizzati in criteri personalizzati di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="7a40a-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7a40a-104">In questo articolo si crea un attributo personalizzato nella directory di Azure AD B2C e si usa il nuovo attributo come attestazione personalizzata nel percorso utente di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="7a40a-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a40a-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7a40a-105">Prerequisites</span></span>

<span data-ttu-id="7a40a-106">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7a40a-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="7a40a-107">Usare attributi personalizzati per raccogliere informazioni sui clienti in Azure Active Directory B2C usando criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="7a40a-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="7a40a-108">La directory di Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di attributi: nome, cognome, città, codice postale, userPrincipalName e così via.  È spesso necessario creare attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7a40a-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="7a40a-109">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7a40a-109">For example:</span></span>
* <span data-ttu-id="7a40a-110">Un'applicazione per i clienti deve rendere persistente un attributo, ad esempio "LoyaltyNumber".</span><span class="sxs-lookup"><span data-stu-id="7a40a-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="7a40a-111">Un provider di identità ha un identificatore utente univoco che deve essere salvato, ad esempio "uniqueUserGUID".</span><span class="sxs-lookup"><span data-stu-id="7a40a-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="7a40a-112">Un percorso utente personalizzato deve rendere persistente lo stato dell'utente, ad esempio "migrationStatus".</span><span class="sxs-lookup"><span data-stu-id="7a40a-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="7a40a-113">Con Azure AD B2C è possibile estendere il set di attributi archiviati in ogni account utente.</span><span class="sxs-lookup"><span data-stu-id="7a40a-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="7a40a-114">Questi attributi possono anche essere scritti e letti usando l' [API Graph di Azure AD](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7a40a-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="7a40a-115">Le proprietà di estensione estendono lo schema degli oggetti utente nella directory.</span><span class="sxs-lookup"><span data-stu-id="7a40a-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="7a40a-116">I termini proprietà di estensione, attributo personalizzato e attestazione personalizzata fanno riferimento allo stesso concetto nel contesto di questo articolo e il nome varia a seconda del contesto (applicazione, oggetto, criteri).</span><span class="sxs-lookup"><span data-stu-id="7a40a-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="7a40a-117">Le proprietà di estensione possono essere registrate solo su un oggetto applicazione anche se possono contenere dati per un utente.</span><span class="sxs-lookup"><span data-stu-id="7a40a-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="7a40a-118">La proprietà è collegata all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-118">The property is attached to the application.</span></span> <span data-ttu-id="7a40a-119">All'oggetto applicazione deve essere concesso l'accesso in scrittura per registrare una proprietà di estensione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="7a40a-120">In un oggetto possono essere scritte 100 proprietà di estensione per TUTTI i tipi e TUTTE le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7a40a-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="7a40a-121">Le proprietà di estensione vengono aggiunte al tipo di directory di destinazione e diventano immediatamente accessibili nel tenant della directory di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7a40a-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="7a40a-122">Se l'applicazione viene eliminata, vengono rimosse anche le proprietà di estensione insieme a tutti i dati contenuti per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="7a40a-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="7a40a-123">Se una proprietà di estensione viene eliminata dall'applicazione, viene rimossa dagli oggetti della directory di destinazione e i valori vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="7a40a-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="7a40a-124">Le proprietà di estensione esistono solo nel contesto di un'applicazione registrata nel tenant.</span><span class="sxs-lookup"><span data-stu-id="7a40a-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="7a40a-125">L'ID oggetto dell'applicazione deve essere incluso nell'elemento TechnicalProfile che usa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="7a40a-126">La directory di Azure AD B2C include in genere un'app Web denominata `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="7a40a-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="7a40a-127">Questa applicazione viene usata principalmente dai criteri B2C predefiniti per le attestazioni personalizzate create tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a40a-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="7a40a-128">L'uso di questa applicazione per registrare estensioni per i criteri personalizzati B2C è consigliata solo agli utenti esperti.</span><span class="sxs-lookup"><span data-stu-id="7a40a-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="7a40a-129">Le istruzioni per questa operazione sono comprese nella sezione Passaggi successivi di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7a40a-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="7a40a-130">Creazione di una nuova applicazione per archiviare le proprietà di estensione</span><span class="sxs-lookup"><span data-stu-id="7a40a-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="7a40a-131">Aprire una sessione di esplorazione, passare al [portale di Azure](https://portal.azure.com) e accedere con le credenziali amministrative della directory B2C che si vuole configurare.</span><span class="sxs-lookup"><span data-stu-id="7a40a-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="7a40a-132">Nel menu di spostamento sinistro fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a40a-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="7a40a-133">Potrebbe essere necessario selezionare Altri servizi> per trovarlo.</span><span class="sxs-lookup"><span data-stu-id="7a40a-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="7a40a-134">Selezionare **Registrazioni per l'app** e fare clic su **Registrazione nuova applicazione**</span><span class="sxs-lookup"><span data-stu-id="7a40a-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="7a40a-135">Specificare gli elementi seguenti consigliati:</span><span class="sxs-lookup"><span data-stu-id="7a40a-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="7a40a-136">Specificare un nome per l'applicazione web: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="7a40a-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="7a40a-137">Tipo di applicazione: app Web/API</span><span class="sxs-lookup"><span data-stu-id="7a40a-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="7a40a-138">URL di accesso: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="7a40a-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="7a40a-139">Selezionare **Crea.</span><span class="sxs-lookup"><span data-stu-id="7a40a-139">Select **Create.</span></span> <span data-ttu-id="7a40a-140">Il completamento dell'operazione viene visualizzato nella sezione **notifiche**</span><span class="sxs-lookup"><span data-stu-id="7a40a-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="7a40a-141">Selezionare l'applicazione web appena creata: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="7a40a-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="7a40a-142">Selezionare Impostazioni: **Autorizzazioni necessarie**</span><span class="sxs-lookup"><span data-stu-id="7a40a-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="7a40a-143">Selezionare l'API **Windows Active Directory**</span><span class="sxs-lookup"><span data-stu-id="7a40a-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="7a40a-144">Inserire un segno di spunta in Autorizzazioni per l'applicazione: **Legge e scrive i dati della directory**, quindi **Salva**</span><span class="sxs-lookup"><span data-stu-id="7a40a-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="7a40a-145">Selezionare **Concedere le autorizzazioni** e quindi fare clic su **Sì** per confermare.</span><span class="sxs-lookup"><span data-stu-id="7a40a-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="7a40a-146">Copiare negli Appunti e salvare gli identificatori seguenti da WebApp-GraphAPI-DirectoryExtensions>Impostazioni>Proprietà></span><span class="sxs-lookup"><span data-stu-id="7a40a-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="7a40a-147">**ID applicazione**.</span><span class="sxs-lookup"><span data-stu-id="7a40a-147">**Application ID** .</span></span> <span data-ttu-id="7a40a-148">Esempio: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="7a40a-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="7a40a-149">**ID oggetto**.</span><span class="sxs-lookup"><span data-stu-id="7a40a-149">**Object ID**.</span></span> <span data-ttu-id="7a40a-150">Esempio: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="7a40a-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="7a40a-151">Modifica dei criteri personalizzati per l'aggiunta di ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="7a40a-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="7a40a-152"><TechnicalProfile Id="AAD-Common"> viene definito "common" perché i relativi elementi vengono inclusi e riusati in tutti i TechnicalProfile di Azure Active Directory usando l'elemento: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="7a40a-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="7a40a-153">Quando TechnicalProfile scrive per la prima volta nella proprietà di estensione appena creata, può verificarsi un errore occasionale.</span><span class="sxs-lookup"><span data-stu-id="7a40a-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="7a40a-154">La proprietà di estensione viene creata la prima volta che viene usata.</span><span class="sxs-lookup"><span data-stu-id="7a40a-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="7a40a-155">Uso della nuova proprietà di estensione o del nuovo attributo personalizzato in un percorso utente</span><span class="sxs-lookup"><span data-stu-id="7a40a-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="7a40a-156">Aprire il file Relying Party che descrive il percorso utente di modifica del criterio.</span><span class="sxs-lookup"><span data-stu-id="7a40a-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="7a40a-157">Se si è appena iniziato, può essere consigliabile scaricare la versione del file RP-PolicyEdit già configurata direttamente dalla sezione dei criteri personalizzati di Azure B2C nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a40a-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="7a40a-158">In alternativa, aprire il file XML dalla cartella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="7a40a-159">Aggiungere un'attestazione personalizzata `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="7a40a-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="7a40a-160">Includendo l'attestazione personalizzata nell'elemento `<RelyingParty>`, l'attestazione viene passata come parametro agli elementi UserJourney TechnicalProfile e inclusa nel token per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="7a40a-161">Aggiungere una definizione di attestazione al file dei criteri di estensione `TrustFrameworkExtensions.xml` all'interno dell'elemento `<ClaimsSchema>`, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7a40a-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="7a40a-162">Aggiungere la stessa definizione di attestazione al file dei criteri di base `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="7a40a-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="7a40a-163">L'aggiunta di una definizione `ClaimType` al file di base e delle estensioni non è generalmente necessaria. Dato che i passaggi successivi aggiungeranno tuttavia extension_loyaltyId agli elementi TechnicalProfile nel file di base, la convalida dei criteri rifiuterà il caricamento del file di base in assenza della definizione.</span><span class="sxs-lookup"><span data-stu-id="7a40a-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="7a40a-164">Può essere utile tenere traccia dell'esecuzione del percorso utente denominato "ProfileEdit" nel file TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="7a40a-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="7a40a-165">Cercare il percorso utente con lo stesso nome nell'editor e osservare che il passaggio di orchestrazione 5 richiama TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="7a40a-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="7a40a-166">Cercare ed esaminare questo elemento TechnicalProfile per acquisire familiarità con il flusso.</span><span class="sxs-lookup"><span data-stu-id="7a40a-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="7a40a-167">Aggiungere loyaltyId come attestazione di input e output nell'elemento TechnicalProfile "SelfAsserted-ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="7a40a-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="7a40a-168">Aggiungere l'attestazione nell'elemento TechnicalProfile "AAD-UserWriteProfileUsingObjectId" per rendere persistente il valore dell'attestazione nella proprietà di estensione per l'utente corrente nella directory.</span><span class="sxs-lookup"><span data-stu-id="7a40a-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="7a40a-169">Aggiungere l'attestazione nell'elemento TechnicalProfile "AAD-UserReadUsingObjectId" per leggere il valore dell'attributo di estensione ogni volta che l'utente esegue l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7a40a-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="7a40a-170">Fino ad ora gli elementi TechnicalProfile sono stati modificati solo nel flusso degli account locali.</span><span class="sxs-lookup"><span data-stu-id="7a40a-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="7a40a-171">Per inserire il nuovo attributo nel flusso di un account di social networking/federato è necessario modificare un set diverso di elementi TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="7a40a-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="7a40a-172">Vedere i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="7a40a-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="7a40a-173">L'elemento IncludeTechnicalProfile aggiunge tutti gli elementi di AAD-Common a questo TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="7a40a-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="7a40a-174">Testare i criteri personalizzati tramite "Esegui adesso"</span><span class="sxs-lookup"><span data-stu-id="7a40a-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="7a40a-175">Aprire il pannello **Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità > Criteri personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="7a40a-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="7a40a-176">Selezionare il criterio personalizzato che è stato caricato e fare clic sul pulsante **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="7a40a-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="7a40a-177">Dovrebbe essere possibile iscriversi usando un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7a40a-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="7a40a-178">Il token ID inviato all'applicazione include la nuova proprietà di estensione come attestazione personalizzata, preceduta da extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="7a40a-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="7a40a-179">Vedere l'esempio.</span><span class="sxs-lookup"><span data-stu-id="7a40a-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="7a40a-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7a40a-180">Next steps</span></span>

<span data-ttu-id="7a40a-181">Aggiungere la nuova attestazione ai flussi per gli accessi con account di social networking modificando gli elementi TechnicalProfile elencati.</span><span class="sxs-lookup"><span data-stu-id="7a40a-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="7a40a-182">Questi due elementi TechnicalProfile vengono usati per gli accessi con account di social networking/federati per scrivere e leggere i dati utente usando alternativeSecurityId come localizzatore dell'oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="7a40a-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="7a40a-183">È possibile usare gli stessi attributi di estensione tra i criteri predefiniti e personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7a40a-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="7a40a-184">Quando si aggiungono attributi di estensione (noti anche come attributi personalizzati) tramite il portale, gli attributi vengono registrati usando la **b2c-extensions-app presente in ogni tenant b2c.</span><span class="sxs-lookup"><span data-stu-id="7a40a-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="7a40a-185">Per usare questi attributi di estensione nei criteri personalizzati:</span><span class="sxs-lookup"><span data-stu-id="7a40a-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="7a40a-186">All'interno del tenant b2c in portal.azure.com, passare a **Azure Active Directory** e selezionare **Registrazioni dell'app**</span><span class="sxs-lookup"><span data-stu-id="7a40a-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="7a40a-187">Trovare **b2c-extensions-app** e selezionarlo</span><span class="sxs-lookup"><span data-stu-id="7a40a-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="7a40a-188">Nella riga "Essentials" registrare l'**ID applicazione** e l'**ID oggetto**</span><span class="sxs-lookup"><span data-stu-id="7a40a-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="7a40a-189">Includerli nei metadati del profilo tecnico AAD-Common come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7a40a-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="7a40a-190">Per mantenere la coerenza con l'esperienza del portale, creare questi attributi tramite l'interfaccia utente del portale *prima* di usarli nei criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7a40a-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="7a40a-191">Quando si crea un attributo "ActivationStatus" nel portale, è necessario farvi riferimento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7a40a-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="7a40a-192">riferimento</span><span class="sxs-lookup"><span data-stu-id="7a40a-192">Reference</span></span>

* <span data-ttu-id="7a40a-193">Un **profilo tecnico** è un tipo di elemento che può essere considerato una *funzione* che definisce il nome di un endpoint, i relativi metadati, il protocollo e i dettagli dello scambio di attestazioni che deve essere eseguito dal Framework dell'esperienza di gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="7a40a-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="7a40a-194">Quando questa *funzione* viene chiamata in un passaggio di orchestrazione o da un altro TechnicalProfile, gli elementi InputClaims e OutputClaims vengono forniti come parametri dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="7a40a-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="7a40a-195">Per una descrizione completa delle proprietà di estensione, vedere l'articolo [ESTENSIONI DELLO SCHEMA DELLA DIRECTORY | CONCETTI RELATIVI ALL'API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="7a40a-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="7a40a-196">Gli attributi di estensione nell'API Graph vengono denominati usando la convenzione `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="7a40a-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="7a40a-197">I criteri personalizzati fanno riferimento agli attributi di estensione come extension_attributename, omettendo quindi ApplicationObjectId nel file XML</span><span class="sxs-lookup"><span data-stu-id="7a40a-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
