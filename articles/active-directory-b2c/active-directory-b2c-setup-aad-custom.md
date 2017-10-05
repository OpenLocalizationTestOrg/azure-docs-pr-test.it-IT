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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="6d875-103">Azure Active Directory B2C: accedere usando account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d875-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6d875-104">Questo articolo illustra come abilitare l'accesso per gli utenti da una specifica organizzazione di Azure Active Directory (Azure AD) tramite l'uso di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6d875-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d875-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6d875-105">Prerequisites</span></span>

<span data-ttu-id="6d875-106">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6d875-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="6d875-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d875-107">These steps include:</span></span>

1. <span data-ttu-id="6d875-108">Creazione di un tenant di Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="6d875-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="6d875-109">Creazione di un'applicazione Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6d875-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="6d875-110">Registrazione di due applicazioni del motore di criteri.</span><span class="sxs-lookup"><span data-stu-id="6d875-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="6d875-111">Configurazione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6d875-111">Setting up keys.</span></span>
5. <span data-ttu-id="6d875-112">Configurazione del pacchetto Starter.</span><span class="sxs-lookup"><span data-stu-id="6d875-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="6d875-113">Creare un'app di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d875-113">Create an Azure AD app</span></span>

<span data-ttu-id="6d875-114">Per abilitare l'accesso agli utenti da una specifica organizzazione di Azure AD, è necessario registrare un'applicazione all'interno del tenant aziendale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d875-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="6d875-115">Nelle istruzioni seguenti vengono usati "contoso.com" per il tenant di Azure AD dell'organizzazione e "fabrikamb2c.onmicrosoft.com" come tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6d875-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="6d875-116">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d875-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="6d875-117">Nella barra in alto selezionare il proprio account.</span><span class="sxs-lookup"><span data-stu-id="6d875-117">On the top bar, select your account.</span></span> <span data-ttu-id="6d875-118">Nell'elenco **Directory** scegliere il tenant di Azure AD dell'organizzazione in cui si desidera registrare l'applicazione (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="6d875-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="6d875-119">Fare clic su **Altri servizi** nel riquadro a sinistra e cercare "Registrazioni per l'app".</span><span class="sxs-lookup"><span data-stu-id="6d875-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="6d875-120">Selezionare **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="6d875-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="6d875-121">Immettere un nome per l'applicazione, ad esempio `Azure AD B2C App`.</span><span class="sxs-lookup"><span data-stu-id="6d875-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="6d875-122">Selezionare **App Web/API** per il tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="6d875-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="6d875-123">Per **URL accesso** immettere l'URL seguente, dove `yourtenant` viene sostituito dal nome del tenant di Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="6d875-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="6d875-124">Salvare l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="6d875-124">Save the application ID.</span></span>
1. <span data-ttu-id="6d875-125">Selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="6d875-125">Select the newly created application.</span></span>
1. <span data-ttu-id="6d875-126">Nel pannello **Impostazioni** selezionare **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="6d875-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="6d875-127">Creare una nuova chiave e salvarla.</span><span class="sxs-lookup"><span data-stu-id="6d875-127">Create a new key, and save it.</span></span> <span data-ttu-id="6d875-128">Questa chiave sarà necessaria nei passaggi della prossima sezione.</span><span class="sxs-lookup"><span data-stu-id="6d875-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="6d875-129">Aggiungere la chiave di Azure AD in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6d875-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="6d875-130">È necessario archiviare la chiave dell'applicazione contoso.com nel tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6d875-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="6d875-131">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6d875-131">To do this:</span></span>
1. <span data-ttu-id="6d875-132">Passare al tenant di Azure AD B2C e selezionare **B2C Settings** (Impostazioni B2C) > **Framework dell'esperienza di gestione delle identità** > **Chiavi dei criteri**.</span><span class="sxs-lookup"><span data-stu-id="6d875-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="6d875-133">Selezionare **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6d875-133">Select **+Add**.</span></span>
1. <span data-ttu-id="6d875-134">Selezionare o immettere queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="6d875-134">Select or enter these options:</span></span>
   * <span data-ttu-id="6d875-135">Selezionare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="6d875-135">Select **Manual**.</span></span>
   * <span data-ttu-id="6d875-136">Per **Nome** scegliere un nome che corrisponda al nome del tenant di Azure AD, ad esempio `ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="6d875-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="6d875-137">Verrà aggiunto automaticamente il prefisso `B2C_1A_` al nome della chiave.</span><span class="sxs-lookup"><span data-stu-id="6d875-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="6d875-138">Incollare la chiave dell'applicazione nella casella **Segreto**.</span><span class="sxs-lookup"><span data-stu-id="6d875-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="6d875-139">Selezionare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="6d875-139">Select **Signature**.</span></span>
1. <span data-ttu-id="6d875-140">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6d875-140">Select **Create**.</span></span>
1. <span data-ttu-id="6d875-141">Confermare di avere creato la chiave `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="6d875-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="6d875-142">Aggiungere un provider di attestazioni nel criterio di base</span><span class="sxs-lookup"><span data-stu-id="6d875-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="6d875-143">Per consentire agli utenti di accedere con Azure AD, è necessario definire Azure AD come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="6d875-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="6d875-144">In altre parole, è necessario specificare un endpoint con cui Azure AD B2C comunicherà.</span><span class="sxs-lookup"><span data-stu-id="6d875-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="6d875-145">L'endpoint offrirà un set di attestazioni che verranno usate da Azure AD B2C per verificare se un utente specifico è stato autenticato.</span><span class="sxs-lookup"><span data-stu-id="6d875-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="6d875-146">È possibile definire Azure AD come provider di attestazioni aggiungendo Azure AD al nodo `<ClaimsProvider>` nel file di estensione dei criteri:</span><span class="sxs-lookup"><span data-stu-id="6d875-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="6d875-147">Aprire il file di estensione (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6d875-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="6d875-148">Trovare la sezione `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="6d875-149">Se non esiste, aggiungerla nel nodo radice.</span><span class="sxs-lookup"><span data-stu-id="6d875-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="6d875-150">Aggiungere un nuovo nodo `<ClaimsProvider>` come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6d875-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="6d875-151">Nel nodo `<ClaimsProvider>` aggiornare il valore di `<Domain>` con un valore univoco che consenta di distinguerlo da altri provider di identità.</span><span class="sxs-lookup"><span data-stu-id="6d875-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="6d875-152">Nel nodo `<ClaimsProvider>` aggiornare il valore di `<DisplayName>` con un nome descrittivo per il provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="6d875-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="6d875-153">Questo valore non è attualmente usato.</span><span class="sxs-lookup"><span data-stu-id="6d875-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="6d875-154">Aggiornare il profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="6d875-154">Update the technical profile</span></span>

<span data-ttu-id="6d875-155">Per ottenere un token dall'endpoint di Azure AD, è necessario definire i protocolli che Azure AD B2C deve usare per comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d875-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="6d875-156">Questa operazione viene eseguita all'interno dell'elemento `<TechnicalProfile>` di `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="6d875-157">Aggiornare l'ID del nodo `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="6d875-158">Questo ID viene usato per fare riferimento al profilo tecnico da altre parti dei criteri.</span><span class="sxs-lookup"><span data-stu-id="6d875-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="6d875-159">Aggiornare il valore di `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="6d875-160">Questo valore verrà visualizzato sul pulsante di accesso nella schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="6d875-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="6d875-161">Aggiornare il valore di `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="6d875-162">Azure AD usa il protocollo OpenID Connect, pertanto è necessario verificare che il valore di `<Protocol>` sia `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="6d875-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="6d875-163">È necessario aggiornare la sezione `<Metadata>` nel file XML precedente in modo da riflettere le impostazioni di configurazione per il tenant di Azure AD specifico.</span><span class="sxs-lookup"><span data-stu-id="6d875-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="6d875-164">Nel file XML aggiornare i valori dei metadati come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6d875-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="6d875-165">Impostare `<Item Key="METADATA">` su `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, dove `yourAzureADtenant` è il nome del tenant di Azure AD, ad esempio, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6d875-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="6d875-166">Aprire il browser e passare all'URL `METADATA` appena aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6d875-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="6d875-167">Nel browser cercare l'oggetto "emittente" e copiarne il valore.</span><span class="sxs-lookup"><span data-stu-id="6d875-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="6d875-168">L'aspetto dovrebbe essere simile al seguente: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="6d875-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="6d875-169">Incollare il valore per `<Item Key="ProviderName">` nel file XML.</span><span class="sxs-lookup"><span data-stu-id="6d875-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="6d875-170">Impostare `<Item Key="client_id">` sull'ID dell'applicazione al momento della registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6d875-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="6d875-171">Impostare `<Item Key="IdTokenAudience">` sull'ID dell'applicazione al momento della registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6d875-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="6d875-172">Assicurarsi che `<Item Key="response_types">` sia impostato su `id_token`.</span><span class="sxs-lookup"><span data-stu-id="6d875-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="6d875-173">Assicurarsi che `<Item Key="UsePolicyInRedirectUri">` sia impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="6d875-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="6d875-174">È anche necessario collegare il segreto di Azure AD registrato nel tenant di Azure AD B2C alle informazioni `<ClaimsProvider>` di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6d875-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="6d875-175">Nella sezione `<CryptographicKeys>` del file XML precedente, aggiornare il valore di `StorageReferenceId` all'ID di riferimento del segreto definito, ad esempio `ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="6d875-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="6d875-176">Caricare il file di estensione per la verifica</span><span class="sxs-lookup"><span data-stu-id="6d875-176">Upload the extension file for verification</span></span>

<span data-ttu-id="6d875-177">I criteri sono stati a questo punto configurati in modo che Azure AD B2C possa comunicare con la directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d875-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="6d875-178">Provare a caricare il file di estensione dei criteri per verificare che non siano presenti problemi.</span><span class="sxs-lookup"><span data-stu-id="6d875-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="6d875-179">A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="6d875-179">To do so:</span></span>

1. <span data-ttu-id="6d875-180">Aprire il pannello **Tutti i criteri** nel tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6d875-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="6d875-181">Selezionare la casella **Sovrascrivi il criterio se esistente**.</span><span class="sxs-lookup"><span data-stu-id="6d875-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="6d875-182">Caricare il file di estensione (TrustFrameworkExtensions.xml) e assicurarsi che non presenti errori di convalida.</span><span class="sxs-lookup"><span data-stu-id="6d875-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="6d875-183">Registrare il provider di attestazioni di Azure AD in un percorso utente</span><span class="sxs-lookup"><span data-stu-id="6d875-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="6d875-184">È ora necessario aggiungere il provider di identità Azure AD in uno dei percorsi utente.</span><span class="sxs-lookup"><span data-stu-id="6d875-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="6d875-185">Il provider di identità è a questo punto configurato, ma non è disponibile in alcuna delle schermate di iscrizione/accesso.</span><span class="sxs-lookup"><span data-stu-id="6d875-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="6d875-186">Perché diventi disponibile, occorre creare un duplicato di un percorso utente modello esistente e quindi modificarlo in modo che includa anche il provider di identità Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6d875-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="6d875-187">Aprire il file di base dei criteri, ad esempio TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="6d875-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="6d875-188">Trovare l'elemento `<UserJourneys>` e copiare l'intero nodo `<UserJourney>` che include `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="6d875-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="6d875-189">Aprire il file di estensione, ad esempio TrustFrameworkExtensions.xml, e trovare l'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="6d875-190">Se l'elemento non esiste, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="6d875-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="6d875-191">Incollare l'intero nodo `<UserJourney>` copiato come figlio dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="6d875-192">Rinominare l'ID del nuovo percorso utente (ad esempio, rinominare come `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="6d875-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="6d875-193">Visualizzare il "pulsante"</span><span class="sxs-lookup"><span data-stu-id="6d875-193">Display the "button"</span></span>

<span data-ttu-id="6d875-194">L'elemento `<ClaimsProviderSelection>` è analogo a un pulsante del provider di identità in una schermata di iscrizione/accesso.</span><span class="sxs-lookup"><span data-stu-id="6d875-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="6d875-195">Se si aggiunge un elemento `<ClaimsProviderSelection>` per Azure AD, verrà visualizzato un nuovo pulsante quando un utente apre la pagina.</span><span class="sxs-lookup"><span data-stu-id="6d875-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="6d875-196">Per aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="6d875-196">To add this element:</span></span>

1. <span data-ttu-id="6d875-197">Trovare il nodo `<OrchestrationStep>` che include `Order="1"` nel percorso utente appena creato.</span><span class="sxs-lookup"><span data-stu-id="6d875-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="6d875-198">Aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6d875-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="6d875-199">Impostare `TargetClaimsExchangeId` su un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="6d875-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="6d875-200">È consigliabile seguire la stessa convenzione degli altri: *\[NomeProviderAttestazioni\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="6d875-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="6d875-201">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="6d875-201">Link the button to an action</span></span>

<span data-ttu-id="6d875-202">Ora che il pulsante è stato posizionato, è necessario collegarlo a un'azione.</span><span class="sxs-lookup"><span data-stu-id="6d875-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="6d875-203">L'azione, in questo caso, consiste nel far comunicare Azure AD B2C con Azure AD per ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="6d875-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="6d875-204">È possibile farlo collegando il profilo tecnico per il provider di attestazioni di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6d875-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="6d875-205">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="6d875-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="6d875-206">Aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6d875-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="6d875-207">Aggiornare `Id` allo stesso valore di `TargetClaimsExchangeId` nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="6d875-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="6d875-208">Aggiornare `TechnicalProfileReferenceId` all'ID del profilo tecnico creato in precedenza, ad esempio ContosoProfile.</span><span class="sxs-lookup"><span data-stu-id="6d875-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="6d875-209">Caricare il file di estensione aggiornato</span><span class="sxs-lookup"><span data-stu-id="6d875-209">Upload the updated extension file</span></span>

<span data-ttu-id="6d875-210">La modifica del file di estensione è completata.</span><span class="sxs-lookup"><span data-stu-id="6d875-210">You are done modifying the extension file.</span></span> <span data-ttu-id="6d875-211">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="6d875-211">Save it.</span></span> <span data-ttu-id="6d875-212">Caricare il file e assicurarsi che tutte le convalide abbiano esito positivo.</span><span class="sxs-lookup"><span data-stu-id="6d875-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="6d875-213">Aggiornare il file RP</span><span class="sxs-lookup"><span data-stu-id="6d875-213">Update the RP file</span></span>

<span data-ttu-id="6d875-214">È ora necessario aggiornare il file della relying party (RP) che avvierà il percorso utente appena creato:</span><span class="sxs-lookup"><span data-stu-id="6d875-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="6d875-215">Creare una copia di SignUpOrSignIn.xml nella directory di lavoro e rinominarla, ad esempio in SignUpOrSignInWithAAD.xml.</span><span class="sxs-lookup"><span data-stu-id="6d875-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="6d875-216">Aprire il nuovo file e aggiornare l'attributo `PolicyId` per `<TrustFrameworkPolicy>` con un valore univoco, ad esempio SignUpOrSignInWithAAD,</span><span class="sxs-lookup"><span data-stu-id="6d875-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="6d875-217">che sarà il nome dei criteri, ad esempio B2C\_1A\_SignUpOrSignInWithAAD.</span><span class="sxs-lookup"><span data-stu-id="6d875-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="6d875-218">Modificare l'attributo `ReferenceId` in `<DefaultUserJourney>` in modo che corrisponda all'ID del nuovo percorso utente creato, ad esempio SignUpOrSignUsingContoso.</span><span class="sxs-lookup"><span data-stu-id="6d875-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="6d875-219">Salvare le modifiche e caricare il file.</span><span class="sxs-lookup"><span data-stu-id="6d875-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6d875-220">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6d875-220">Troubleshooting</span></span>

<span data-ttu-id="6d875-221">Testare i criteri personalizzati appena caricati aprendo il relativo pannello e facendo clic su **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="6d875-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="6d875-222">Per diagnosticare i problemi, leggere l'articolo relativo alla [risoluzione dei problemi](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6d875-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d875-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d875-223">Next steps</span></span>

<span data-ttu-id="6d875-224">Inviare commenti e suggerimenti all'indirizzo [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6d875-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
