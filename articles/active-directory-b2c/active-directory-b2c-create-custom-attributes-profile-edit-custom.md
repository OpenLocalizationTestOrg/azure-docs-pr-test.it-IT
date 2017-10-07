---
title: 'Azure Active B2C di Directory: Aggiungere i propri criteri toocustom gli attributi e utilizzare in Modifica profilo | Documenti Microsoft'
description: "Una procedura dettagliata sull'uso di proprietà di estensione, gli attributi personalizzati e vengono inclusi nell'interfaccia utente di hello"
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
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="0aef8-103">Azure Active Directory B2C: Creazione e utilizzo di attributi personalizzati in criteri personalizzati di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="0aef8-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0aef8-104">In questo articolo creare un attributo personalizzato nella directory di Azure Active Directory B2C e il nuovo attributo utilizzato come un'attestazione personalizzata in viaggio di hello profilo Modifica utente.</span><span class="sxs-lookup"><span data-stu-id="0aef8-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aef8-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0aef8-105">Prerequisites</span></span>

<span data-ttu-id="0aef8-106">Hello completato i passaggi nell'articolo hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0aef8-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="0aef8-107">Utilizzare gli attributi personalizzati toocollect informazioni sui clienti in Azure Active Directory B2C usando i criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="0aef8-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="0aef8-108">La directory di Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di attributi: nome, cognome, città, codice postale, userPrincipalName e così via.  È spesso necessario toocreate attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0aef8-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="0aef8-109">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0aef8-109">For example:</span></span>
* <span data-ttu-id="0aef8-110">Un'applicazione che riguardano il cliente deve toopersist un attributo, ad esempio "LoyaltyNumber".</span><span class="sxs-lookup"><span data-stu-id="0aef8-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="0aef8-111">Un provider di identità ha un identificatore utente univoco che deve essere salvato, ad esempio "uniqueUserGUID".</span><span class="sxs-lookup"><span data-stu-id="0aef8-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="0aef8-112">Stato hello toopersist dell'utente, ad esempio "migrationStatus". è necessario un proprio processo utente personalizzata</span><span class="sxs-lookup"><span data-stu-id="0aef8-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="0aef8-113">Con Azure Active Directory B2C, è possibile estendere il set di hello di attributi archiviati in ogni account utente.</span><span class="sxs-lookup"><span data-stu-id="0aef8-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="0aef8-114">È anche possibile leggere e scrivere tali attributi tramite hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0aef8-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="0aef8-115">Le proprietà di estensione estendono schema hello degli oggetti utente hello nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="0aef8-116">proprietà di estensione Hello termini, un attributo personalizzato e attestazioni personalizzate, vedere toohello stessa operazione nel contesto di hello di questo nome di articolo e hello varia a seconda del contesto di hello (applicazione, oggetto, criteri).</span><span class="sxs-lookup"><span data-stu-id="0aef8-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="0aef8-117">Le proprietà di estensione possono essere registrate solo su un oggetto applicazione anche se possono contenere dati per un utente.</span><span class="sxs-lookup"><span data-stu-id="0aef8-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="0aef8-118">proprietà Hello è applicazione toohello associata.</span><span class="sxs-lookup"><span data-stu-id="0aef8-118">hello property is attached toohello application.</span></span> <span data-ttu-id="0aef8-119">oggetto applicazione Hello deve essere concesso l'accesso in scrittura tooregister una proprietà di estensione.</span><span class="sxs-lookup"><span data-stu-id="0aef8-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="0aef8-120">Proprietà di estensione 100 (tra tutti i tipi e tutte le applicazioni) possono essere scritti tooany singolo oggetto.</span><span class="sxs-lookup"><span data-stu-id="0aef8-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="0aef8-121">Le proprietà di estensione vengono aggiunti toohello tipo di directory di destinazione e diventa immediatamente accessibile nel tenant di directory hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0aef8-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="0aef8-122">Se un'applicazione hello viene eliminata, vengono rimosse anche le proprietà di estensione insieme a tutti i dati in essi contenuti per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="0aef8-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="0aef8-123">Se una proprietà di estensione viene eliminata dall'applicazione hello, viene anche rimossa per hello hello valori eliminati e gli oggetti directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0aef8-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="0aef8-124">Le proprietà di estensione esistono solo nel contesto di hello di un'applicazione registrata nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="0aef8-125">id di oggetto Hello dell'applicazione deve essere incluso in hello TechnicalProfile che lo utilizzano.</span><span class="sxs-lookup"><span data-stu-id="0aef8-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="0aef8-126">directory di Azure Active Directory B2C Hello include in genere un'applicazione Web denominata `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="0aef8-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="0aef8-127">Questa applicazione viene utilizzata principalmente per le attestazioni personalizzate di hello create tramite il portale di Azure hello dai criteri predefiniti di hello b2c.</span><span class="sxs-lookup"><span data-stu-id="0aef8-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="0aef8-128">L'uso di estensioni di tooregister questa applicazione per i criteri personalizzati b2c è consigliato solo per gli utenti esperti.</span><span class="sxs-lookup"><span data-stu-id="0aef8-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="0aef8-129">Istruzioni per questo sono incluse nella sezione passaggi successivi in questo articolo hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="0aef8-130">Creazione di un nuovo toostore applicazione le proprietà di estensione hello</span><span class="sxs-lookup"><span data-stu-id="0aef8-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="0aef8-131">Aprire una sessione di esplorazione e passare toohello [Azure Portal](https://portal.azure.com) e accedere con credenziali amministrative di hello Directory B2C da tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0aef8-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="0aef8-132">Fare clic su **Azure Active Directory** nel menu di navigazione sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="0aef8-133">Potrebbe essere necessario per la selezione di più servizi toofind >.</span><span class="sxs-lookup"><span data-stu-id="0aef8-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="0aef8-134">Selezionare **Registrazioni per l'app** e fare clic su **Registrazione nuova applicazione**</span><span class="sxs-lookup"><span data-stu-id="0aef8-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="0aef8-135">Fornire seguente hello consigliato voci:</span><span class="sxs-lookup"><span data-stu-id="0aef8-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="0aef8-136">Specificare un nome per un'applicazione web hello: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="0aef8-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="0aef8-137">Tipo di applicazione: app Web/API</span><span class="sxs-lookup"><span data-stu-id="0aef8-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="0aef8-138">URL di accesso: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="0aef8-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="0aef8-139">Selezionare **Crea.</span><span class="sxs-lookup"><span data-stu-id="0aef8-139">Select **Create.</span></span> <span data-ttu-id="0aef8-140">Operazione completata viene visualizzato in hello **notifiche**</span><span class="sxs-lookup"><span data-stu-id="0aef8-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="0aef8-141">Selezionare un'applicazione web hello appena creato: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="0aef8-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="0aef8-142">Selezionare Impostazioni: **Autorizzazioni necessarie**</span><span class="sxs-lookup"><span data-stu-id="0aef8-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="0aef8-143">Selezionare l'API **Windows Active Directory**</span><span class="sxs-lookup"><span data-stu-id="0aef8-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="0aef8-144">Inserire un segno di spunta in Autorizzazioni per l'applicazione: **Legge e scrive i dati della directory**, quindi **Salva**</span><span class="sxs-lookup"><span data-stu-id="0aef8-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="0aef8-145">Selezionare **Concedere le autorizzazioni** e quindi fare clic su **Sì** per confermare.</span><span class="sxs-lookup"><span data-stu-id="0aef8-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="0aef8-146">Copiare negli Appunti tooyour e salvare hello seguenti identificatori dagli WebApp-GraphAPI-DirectoryExtensions > Impostazioni > Proprietà ></span><span class="sxs-lookup"><span data-stu-id="0aef8-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="0aef8-147">**ID applicazione**.</span><span class="sxs-lookup"><span data-stu-id="0aef8-147">**Application ID** .</span></span> <span data-ttu-id="0aef8-148">Esempio: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="0aef8-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="0aef8-149">**ID oggetto**.</span><span class="sxs-lookup"><span data-stu-id="0aef8-149">**Object ID**.</span></span> <span data-ttu-id="0aef8-150">Esempio: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="0aef8-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="0aef8-151">Modifica di hello di tooadd ApplicationObjectId i criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="0aef8-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

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
><span data-ttu-id="0aef8-152">Hello <TechnicalProfile Id="AAD-Common"> è tooas cui "comuni" perché gli elementi sono inclusi in e riutilizzati in hello tutti TechnicalProfiles di Azure Active Directory utilizzando l'elemento hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="0aef8-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="0aef8-153">Quando hello TechnicalProfile scrive per la proprietà di estensione di hello prima ora toohello appena creato, è possibile che si verifichi un errore occasionale.</span><span class="sxs-lookup"><span data-stu-id="0aef8-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="0aef8-154">proprietà di estensione Hello creato hello prima volta che viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0aef8-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="0aef8-155">Utilizzando una nuova proprietà di estensione hello / attributo personalizzato in un proprio processo utente</span><span class="sxs-lookup"><span data-stu-id="0aef8-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="0aef8-156">Aprire hello Relying Party(RP) file che descrive i criteri di modifica viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="0aef8-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="0aef8-157">Se si sta avviando, potrebbe essere consigliabile toodownload la versione di hello RP PolicyEdit già configurata file direttamente dalla sezione criteri personalizzati di B2C Azure nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="0aef8-158">In alternativa, aprire il file XML dalla cartella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0aef8-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="0aef8-159">Aggiungere un'attestazione personalizzata `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="0aef8-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="0aef8-160">Includendo hello personalizzato con una richiesta di rimborso in hello `<RelyingParty>` elemento, è passato come un toohello parametro UserJourney TechnicalProfiles e incluse nel token hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
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
3. <span data-ttu-id="0aef8-161">Aggiungere un file di criteri di attestazione definizione toohello estensione `TrustFrameworkExtensions.xml` all'interno di hello `<ClaimsSchema>` elemento, come illustrato.</span><span class="sxs-lookup"><span data-stu-id="0aef8-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="0aef8-162">Aggiungere hello stessa attestazione file di definizione dei criteri di Base toohello `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="0aef8-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="0aef8-163">Aggiunta di un `ClaimType` definizione base hello sia nel hello estensioni file in genere non è necessario, tuttavia, poiché i passaggi successivi hello aggiungerà hello extension_loyaltyId tooTechnicalProfiles nel file di Base hello, convalida criteri hello rifiuterà il caricamento di hello hello file di base senza di esso.</span><span class="sxs-lookup"><span data-stu-id="0aef8-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="0aef8-164">Potrebbe essere utile tootrace esecuzione di hello del viaggio utente hello denominato "ProfileEdit" nel file TrustFrameworkBase.xml hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="0aef8-165">Ricerca di viaggio utente hello di hello stesso nome nell'editor e osservare che il passaggio 5 di orchestrazione richiama hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="0aef8-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="0aef8-166">Ricerca e controllare questo toofamiliarize TechnicalProfile con flusso hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="0aef8-167">Aggiungere loyaltyId come attestazioni di input e output di hello TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="0aef8-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="0aef8-168">Aggiunge l'attestazione "UserWriteProfileUsingObjectId-AAD" TechnicalProfile toopersist hello valore attestazione hello nella proprietà di estensione hello, per l'utente corrente di hello nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
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
7. <span data-ttu-id="0aef8-169">Aggiunge l'attestazione nel valore di hello tooread TechnicalProfile "UserReadUsingObjectId-AAD" dell'attributo di estensione hello ogni volta che un utente accede.</span><span class="sxs-lookup"><span data-stu-id="0aef8-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="0aef8-170">Hello TechnicalProfiles finora sono state modificate nel flusso di hello del solo gli account locali.</span><span class="sxs-lookup"><span data-stu-id="0aef8-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="0aef8-171">Volendo nuovo attributo hello nel flusso di hello di un account o federata sociale, un set diverso di TechnicalProfiles deve toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="0aef8-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="0aef8-172">Vedere i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="0aef8-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
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
><span data-ttu-id="0aef8-173">elemento IncludeTechnicalProfile Hello aggiunge tutti gli elementi di hello di Azure ad comune toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="0aef8-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="0aef8-174">Criterio personalizzato di test hello tramite "Esegui"</span><span class="sxs-lookup"><span data-stu-id="0aef8-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="0aef8-175">Aprire hello **Pannello di Azure Active Directory B2C** e passare troppo**identità esperienza Framework > criteri personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="0aef8-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="0aef8-176">Selezionare i criteri personalizzati hello caricato, quindi scegliere hello **Esegui ora** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0aef8-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="0aef8-177">È necessario essere in grado di toosign utilizzando un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0aef8-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="0aef8-178">token id Hello inviato nuovamente tooyour applicazione include una nuova proprietà di estensione hello come un'attestazione personalizzata preceduta da extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="0aef8-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="0aef8-179">Vedere l'esempio.</span><span class="sxs-lookup"><span data-stu-id="0aef8-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0aef8-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0aef8-180">Next steps</span></span>

<span data-ttu-id="0aef8-181">Aggiungere hello nuova attestazione toohello flussi per gli account di accesso account social modificando hello TechnicalProfiles elencati.</span><span class="sxs-lookup"><span data-stu-id="0aef8-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="0aef8-182">Questi due TechnicalProfiles utilizzate dal toowrite gli account di accesso account sociale o federata e leggere i dati utente hello utilizzando alternativeSecurityId hello come indicatore di posizione dell'oggetto utente hello hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="0aef8-183">Utilizzando hello stessi attributi di estensione tra i criteri predefiniti e personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0aef8-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="0aef8-184">Quando si aggiungono gli attributi dell'estensione (noto anche come attributi personalizzati) tramite l'uso del portale hello, tali attributi vengono registrati utilizzando hello * * b2c-estensioni-app presente in ogni tenant b2c.</span><span class="sxs-lookup"><span data-stu-id="0aef8-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="0aef8-185">toouse questi attributi di estensione per il criterio personalizzato:</span><span class="sxs-lookup"><span data-stu-id="0aef8-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="0aef8-186">All'interno di tenant b2c in portal.azure.com, passare troppo**Azure Active Directory** e selezionare **registrazioni di App**</span><span class="sxs-lookup"><span data-stu-id="0aef8-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="0aef8-187">Trovare **b2c-extensions-app** e selezionarlo</span><span class="sxs-lookup"><span data-stu-id="0aef8-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="0aef8-188">In hello record 'Essentials' **ID applicazione** e hello **ID di oggetto**</span><span class="sxs-lookup"><span data-stu-id="0aef8-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="0aef8-189">Includerli nei metadati del profilo tecnico AAD-Common come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0aef8-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="0aef8-190">la coerenza tookeep con esperienza del portale hello, creare questi attributi utilizzando l'interfaccia utente del portale hello *prima* utilizzarle nei criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0aef8-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="0aef8-191">Quando si crea un attributo "ActivationStatus" nel portale di hello, è necessario consultare tooit come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0aef8-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="0aef8-192">riferimento</span><span class="sxs-lookup"><span data-stu-id="0aef8-192">Reference</span></span>

* <span data-ttu-id="0aef8-193">A **profilo tecnico (TP)** è un tipo di elemento che può essere considerato come un *funzione* che definisce il nome di un endpoint, i metadati, il protocollo e dettagli hello exchange di attestazioni che hello identità Esperienza Framework deve eseguire.</span><span class="sxs-lookup"><span data-stu-id="0aef8-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="0aef8-194">Quando questo *funzione* viene chiamato in un passaggio di orchestrazione o da un altro TechnicalProfile, hello InputClaims e OutputClaims vengono forniti come parametri per il chiamante di hello.</span><span class="sxs-lookup"><span data-stu-id="0aef8-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="0aef8-195">Per una gestione completa sulle proprietà di estensione, vedere l'articolo hello [le estensioni dello SCHEMA di DIRECTORY | CONCETTI RELATIVI ALL'API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="0aef8-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="0aef8-196">Gli attributi di estensione nell'API Graph sono denominati in base alla convenzione hello `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="0aef8-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="0aef8-197">Criteri personalizzati fanno riferimento gli attributi tooextensions come extension_attributename, pertanto l'omissione di hello ApplicationObjectId in hello XML</span><span class="sxs-lookup"><span data-stu-id="0aef8-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
