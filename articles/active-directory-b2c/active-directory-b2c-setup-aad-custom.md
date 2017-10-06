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
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="33b3f-103">Azure Active Directory B2C: accedere usando account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="33b3f-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="33b3f-104">Questo articolo illustra come tooenable Accedi per gli utenti da un'organizzazione di Azure Active Directory (Azure AD) specifico tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="33b3f-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33b3f-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33b3f-105">Prerequisites</span></span>

<span data-ttu-id="33b3f-106">Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="33b3f-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="33b3f-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="33b3f-107">These steps include:</span></span>

1. <span data-ttu-id="33b3f-108">Creazione di un tenant di Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="33b3f-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="33b3f-109">Creazione di un'applicazione Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="33b3f-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="33b3f-110">Registrazione di due applicazioni del motore di criteri.</span><span class="sxs-lookup"><span data-stu-id="33b3f-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="33b3f-111">Configurazione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="33b3f-111">Setting up keys.</span></span>
5. <span data-ttu-id="33b3f-112">Configurazione di pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="33b3f-113">Creare un'app di Azure AD</span><span class="sxs-lookup"><span data-stu-id="33b3f-113">Create an Azure AD app</span></span>

<span data-ttu-id="33b3f-114">tooenable Accedi per gli utenti da uno specifico dell'organizzazione di Azure AD, è necessario tooregister un'applicazione nel tenant di hello Azure AD dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="33b3f-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="33b3f-115">Utilizziamo "contoso.com" per il tenant di Azure AD dell'organizzazione hello e "fabrikamb2c.onmicrosoft.com" come tenant di Azure Active Directory B2C hello in hello attenendosi alle istruzioni.</span><span class="sxs-lookup"><span data-stu-id="33b3f-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="33b3f-116">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33b3f-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="33b3f-117">Nella barra superiore hello, selezionare l'account.</span><span class="sxs-lookup"><span data-stu-id="33b3f-117">On hello top bar, select your account.</span></span> <span data-ttu-id="33b3f-118">Da hello **Directory** scegliere tenant hello Azure AD dell'organizzazione in cui si desidera tooregister dell'applicazione (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="33b3f-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="33b3f-119">Selezionare **più servizi** nel riquadro sinistro di hello e cercare "Registrazioni di App".</span><span class="sxs-lookup"><span data-stu-id="33b3f-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="33b3f-120">Selezionare **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="33b3f-121">Immettere un nome per l'applicazione, ad esempio `Azure AD B2C App`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="33b3f-122">Selezionare **app Web / API** per il tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="33b3f-123">Per **Sign-on URL**, immettere hello seguente URL, in cui `yourtenant` viene sostituito dal nome hello del tenant di Azure Active Directory B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="33b3f-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="33b3f-124">Salvare l'ID applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-124">Save hello application ID.</span></span>
1. <span data-ttu-id="33b3f-125">Selezionare un'applicazione hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="33b3f-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="33b3f-126">In hello **impostazioni** pannello seleziona **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="33b3f-127">Creare una nuova chiave e salvarla.</span><span class="sxs-lookup"><span data-stu-id="33b3f-127">Create a new key, and save it.</span></span> <span data-ttu-id="33b3f-128">Verrà utilizzato nei passaggi hello nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="33b3f-129">Aggiungere tooAzure chiave hello AD Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="33b3f-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="33b3f-130">È necessario toostore chiave dell'applicazione hello contoso.com nel tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="33b3f-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="33b3f-131">toodo questo:</span><span class="sxs-lookup"><span data-stu-id="33b3f-131">toodo this:</span></span>
1. <span data-ttu-id="33b3f-132">Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **identità esperienza Framework** > **chiavi dei criteri**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="33b3f-133">Selezionare **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-133">Select **+Add**.</span></span>
1. <span data-ttu-id="33b3f-134">Selezionare o immettere queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="33b3f-134">Select or enter these options:</span></span>
   * <span data-ttu-id="33b3f-135">Selezionare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-135">Select **Manual**.</span></span>
   * <span data-ttu-id="33b3f-136">Per **Nome** scegliere un nome che corrisponda al nome del tenant di Azure AD, ad esempio `ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="33b3f-137">prefisso Hello `B2C_1A_` viene aggiunto automaticamente toohello nome della chiave.</span><span class="sxs-lookup"><span data-stu-id="33b3f-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="33b3f-138">Incollare la chiave applicazione hello **Secret** casella.</span><span class="sxs-lookup"><span data-stu-id="33b3f-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="33b3f-139">Selezionare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-139">Select **Signature**.</span></span>
1. <span data-ttu-id="33b3f-140">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-140">Select **Create**.</span></span>
1. <span data-ttu-id="33b3f-141">Verificare di aver creato la chiave hello `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="33b3f-142">Aggiungere un provider di attestazioni nel criterio di base</span><span class="sxs-lookup"><span data-stu-id="33b3f-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="33b3f-143">Se si desidera toosign gli utenti grazie ad Azure AD, è necessario toodefine Azure AD come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="33b3f-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="33b3f-144">In altre parole, è necessario un endpoint di Azure Active Directory B2C con cui comunicherà toospecify.</span><span class="sxs-lookup"><span data-stu-id="33b3f-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="33b3f-145">endpoint Hello fornirà un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="33b3f-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="33b3f-146">È possibile definire Azure AD come provider di attestazioni tramite l'aggiunta di Azure AD toohello `<ClaimsProvider>` nodo nel file di estensione hello dei criteri:</span><span class="sxs-lookup"><span data-stu-id="33b3f-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="33b3f-147">Aprire il file di estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="33b3f-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="33b3f-148">Trovare hello `<ClaimsProviders>` sezione.</span><span class="sxs-lookup"><span data-stu-id="33b3f-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="33b3f-149">Se non esiste, aggiungerla nel nodo radice hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="33b3f-150">Aggiungere un nuovo nodo `<ClaimsProvider>` come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="33b3f-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="33b3f-151">In hello `<ClaimsProvider>` valore hello di aggiornamento per nodo `<Domain>` tooa un valore univoco che può essere toodistinguish utilizzato da altri provider di identità.</span><span class="sxs-lookup"><span data-stu-id="33b3f-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="33b3f-152">In hello `<ClaimsProvider>` valore hello di aggiornamento per nodo `<DisplayName>` tooa nome descrittivo per hello provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="33b3f-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="33b3f-153">Questo valore non è attualmente usato.</span><span class="sxs-lookup"><span data-stu-id="33b3f-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="33b3f-154">Aggiornare il profilo tecnico hello</span><span class="sxs-lookup"><span data-stu-id="33b3f-154">Update hello technical profile</span></span>

<span data-ttu-id="33b3f-155">un token dall'endpoint di Azure AD hello tooget, è necessario protocolli hello toodefine che Azure Active Directory B2C deve utilizzare toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b3f-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="33b3f-156">Questa operazione viene eseguita all'interno di hello `<TechnicalProfile>` elemento `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="33b3f-157">Aggiornare l'ID di hello di hello `<TechnicalProfile>` nodo.</span><span class="sxs-lookup"><span data-stu-id="33b3f-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="33b3f-158">Questo ID è utilizzato toorefer toothis profilo tecnica da altre parti del criterio hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="33b3f-159">Aggiornare il valore di hello per `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="33b3f-160">Questo valore verrà visualizzato sul pulsante Accedi hello sullo schermo Accedi.</span><span class="sxs-lookup"><span data-stu-id="33b3f-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="33b3f-161">Aggiornare il valore di hello per `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="33b3f-162">Azure AD Usa protocollo OpenID Connect hello, verificare il valore di hello per `<Protocol>` è `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="33b3f-163">È necessario tooupdate hello `<Metadata>` sezione nel file XML di hello cui le impostazioni di configurazione tooearlier tooreflect hello per specifico tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b3f-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="33b3f-164">Nel file XML di hello, aggiornare i valori dei metadati hello come segue:</span><span class="sxs-lookup"><span data-stu-id="33b3f-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="33b3f-165">Impostare `<Item Key="METADATA">` troppo`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, dove `yourAzureADtenant` è il nome di tenant di Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="33b3f-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="33b3f-166">Aprire il toohello browser e andare `METADATA` URL che hai appena aggiornato.</span><span class="sxs-lookup"><span data-stu-id="33b3f-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="33b3f-167">Nel browser hello, cercare l'oggetto 'issuer' hello e copiare il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="33b3f-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="33b3f-168">Dovrebbe essere simile al seguente hello: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="33b3f-169">Incollare il valore di hello per `<Item Key="ProviderName">` nel file XML di hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="33b3f-170">Impostare `<Item Key="client_id">` ID applicazione toohello dalla registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="33b3f-171">Impostare `<Item Key="IdTokenAudience">` ID applicazione toohello dalla registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="33b3f-172">Verificare che `<Item Key="response_types">` è troppo`id_token`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="33b3f-173">Verificare che `<Item Key="UsePolicyInRedirectUri">` è troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="33b3f-174">È inoltre necessario segreto hello Azure AD toolink registrate nel toohello di tenant Azure AD di Azure Active Directory B2C `<ClaimsProvider>` informazioni:</span><span class="sxs-lookup"><span data-stu-id="33b3f-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="33b3f-175">In hello `<CryptographicKeys>` sezione hello precedente file XML, aggiornare il valore di hello per `StorageReferenceId` toohello ID di riferimento del segreto hello è definito (ad esempio, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="33b3f-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="33b3f-176">Caricare il file di estensione hello per verifica</span><span class="sxs-lookup"><span data-stu-id="33b3f-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="33b3f-177">A questo punto, sono stati configurati i criteri in modo che Azure Active Directory B2C sa come toocommunicate con la directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b3f-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="33b3f-178">Provare a caricare il file di estensione hello di tooconfirm di solo i criteri che non vi siano finora eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="33b3f-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="33b3f-179">toodo in modo:</span><span class="sxs-lookup"><span data-stu-id="33b3f-179">toodo so:</span></span>

1. <span data-ttu-id="33b3f-180">Aprire hello **tutti i criteri** pannello nel tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="33b3f-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="33b3f-181">Controllare hello **sovrascrivere i criteri di hello eventuale** casella.</span><span class="sxs-lookup"><span data-stu-id="33b3f-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="33b3f-182">Caricare il file di estensione hello (TrustFrameworkExtensions.xml) e assicurarsi che non riuscire convalida hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="33b3f-183">Registrare il viaggio utente tooa provider di hello Azure AD attestazioni</span><span class="sxs-lookup"><span data-stu-id="33b3f-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="33b3f-184">È ora necessario tooadd hello Azure AD identity provider tooone di viaggi l'utente.</span><span class="sxs-lookup"><span data-stu-id="33b3f-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="33b3f-185">A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="33b3f-186">toomake è disponibile, verrà creato un duplicato di un proprio processo utente di modello esistente e quindi modificarlo in modo che include anche i provider di identità hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="33b3f-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="33b3f-187">Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="33b3f-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="33b3f-188">Trovare hello `<UserJourneys>` elemento e copia hello intero `<UserJourney>` nodo che include `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="33b3f-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="33b3f-189">Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="33b3f-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="33b3f-190">Se non esiste l'elemento hello, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="33b3f-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="33b3f-191">Hello Incolla intero `<UserJourney>` nodo copiato come figlio di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="33b3f-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="33b3f-192">Rinominare ID hello del viaggio di hello nuovo utente (ad esempio, rinominare come `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="33b3f-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="33b3f-193">Hello visualizzato "pulsante"</span><span class="sxs-lookup"><span data-stu-id="33b3f-193">Display hello "button"</span></span>

<span data-ttu-id="33b3f-194">Hello `<ClaimsProviderSelection>` elemento è di pulsante di provider di identità tooan analoghi in una schermata di sign-configurazione/Accedi.</span><span class="sxs-lookup"><span data-stu-id="33b3f-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="33b3f-195">Se si aggiunge un `<ClaimsProviderSelection>` elemento per Azure AD, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="33b3f-196">tooadd questo elemento:</span><span class="sxs-lookup"><span data-stu-id="33b3f-196">tooadd this element:</span></span>

1. <span data-ttu-id="33b3f-197">Trovare hello `<OrchestrationStep>` nodo che include `Order="1"` in viaggio utente hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="33b3f-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="33b3f-198">Aggiungere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="33b3f-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="33b3f-199">Impostare `TargetClaimsExchangeId` tooan di valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="33b3f-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="33b3f-200">È consigliabile seguente hello stessa convenzione come altri:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="33b3f-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="33b3f-201">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="33b3f-201">Link hello button tooan action</span></span>

<span data-ttu-id="33b3f-202">Ora che si dispone di un pulsante, è necessario toolink è tooan azione.</span><span class="sxs-lookup"><span data-stu-id="33b3f-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="33b3f-203">azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Azure AD tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="33b3f-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="33b3f-204">Collegamento azione pulsante di hello tooan collegando profilo tecniche hello per il provider di attestazioni di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="33b3f-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="33b3f-205">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="33b3f-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="33b3f-206">Aggiungere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="33b3f-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="33b3f-207">Aggiornamento `Id` toohello lo stesso valore di `TargetClaimsExchangeId` nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="33b3f-208">Aggiornamento `TechnicalProfileReferenceId` toohello ID di hello tecnica profilo creato in precedenza (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="33b3f-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="33b3f-209">Caricare il file di estensione aggiornata hello</span><span class="sxs-lookup"><span data-stu-id="33b3f-209">Upload hello updated extension file</span></span>

<span data-ttu-id="33b3f-210">La modifica dei file di estensione hello termine.</span><span class="sxs-lookup"><span data-stu-id="33b3f-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="33b3f-211">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="33b3f-211">Save it.</span></span> <span data-ttu-id="33b3f-212">Quindi caricare il file hello e assicurarsi che tutte le convalide esito positivo.</span><span class="sxs-lookup"><span data-stu-id="33b3f-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="33b3f-213">File di aggiornamento hello RP</span><span class="sxs-lookup"><span data-stu-id="33b3f-213">Update hello RP file</span></span>

<span data-ttu-id="33b3f-214">È ora necessario tooupdate hello relying party (RP) file avvierà viaggio utente hello appena creato:</span><span class="sxs-lookup"><span data-stu-id="33b3f-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="33b3f-215">Creare una copia di SignUpOrSignIn.xml nella directory di lavoro e rinominarlo (ad esempio, rinominarla tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="33b3f-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="33b3f-216">Hello di file e aggiornamento nuovo hello aprire `PolicyId` attributo per `<TrustFrameworkPolicy>` con un valore univoco (ad esempio, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="33b3f-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="33b3f-217">Questo sarà il nome di hello dei criteri (ad esempio, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="33b3f-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="33b3f-218">Modificare hello `ReferenceId` attributo `<DefaultUserJourney>` toomatch hello ID di hello nuovo utente proprio processo creato (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="33b3f-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="33b3f-219">Salvare le modifiche e caricare file hello.</span><span class="sxs-lookup"><span data-stu-id="33b3f-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="33b3f-220">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="33b3f-220">Troubleshooting</span></span>

<span data-ttu-id="33b3f-221">Testare i criteri personalizzati hello appena caricato il pannello e facendo clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="33b3f-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="33b3f-222">informazioni su problemi toodiagnose, [risoluzione dei problemi](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="33b3f-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33b3f-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33b3f-223">Next steps</span></span>

<span data-ttu-id="33b3f-224">Fornire commenti e suggerimenti troppo[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="33b3f-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
