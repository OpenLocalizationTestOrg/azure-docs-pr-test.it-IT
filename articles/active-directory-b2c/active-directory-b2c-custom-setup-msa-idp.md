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
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="6519b-103">Azure Active Directory B2C: Aggiungere un account Microsoft come provider di identità tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="6519b-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6519b-104">Questo articolo illustra come tooenable Accedi per gli utenti dall'account Microsoft (MSA) tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6519b-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6519b-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6519b-105">Prerequisites</span></span>
<span data-ttu-id="6519b-106">Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6519b-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="6519b-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6519b-107">These steps include:</span></span>

1.  <span data-ttu-id="6519b-108">Creazione di un'applicazione di account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6519b-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="6519b-109">Aggiunta di hello Microsoft account applicazione chiave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6519b-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="6519b-110">Aggiunta di criteri tooa provider di attestazioni</span><span class="sxs-lookup"><span data-stu-id="6519b-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="6519b-111">Registrazione di viaggio di hello Account Microsoft attestazioni provider tooa utente</span><span class="sxs-lookup"><span data-stu-id="6519b-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="6519b-112">Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="6519b-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="6519b-113">Creare un'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="6519b-113">Create a Microsoft account application</span></span>
<span data-ttu-id="6519b-114">toouse Microsoft account come un provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di account Microsoft e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="6519b-115">È necessario un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6519b-115">You need a Microsoft account.</span></span> <span data-ttu-id="6519b-116">Se non si ha un account, visitare il sito [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="6519b-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="6519b-117">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali dell'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6519b-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="6519b-118">Fare clic su **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="6519b-118">Click **Add an app**.</span></span>

    ![Account Microsoft - Aggiungere un'app](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="6519b-120">Specificare un **Nome** per l'applicazione e un **Indirizzo di posta elettronica di contatto**, deselezionare l'opzione **Informazioni per l'utilizzo iniziale** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6519b-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Account Microsoft - Registrare l'applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="6519b-122">Copiare il valore di hello di **Id applicazione**. È necessario tooconfigure account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="6519b-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Account Microsoft - valore hello copia dell'Id applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="6519b-124">Fare clic su **Aggiungi piattaforma**</span><span class="sxs-lookup"><span data-stu-id="6519b-124">Click on **Add platform**</span></span>

    ![Account Microsoft - Aggiungi piattaforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="6519b-126">Selezionare dall'elenco piattaforma hello **Web**.</span><span class="sxs-lookup"><span data-stu-id="6519b-126">From hello platform list, choose **Web**.</span></span>

    ![Account Microsoft - dall'elenco delle piattaforme hello scegliere Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="6519b-128">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** campo.</span><span class="sxs-lookup"><span data-stu-id="6519b-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="6519b-129">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6519b-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Account Microsoft - Impostare gli URL di reindirizzamento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="6519b-131">Fare clic su **generare una nuova Password** in hello **applicazione segreti** sezione.</span><span class="sxs-lookup"><span data-stu-id="6519b-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="6519b-132">Copia hello nuova password visualizzata sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="6519b-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="6519b-133">È necessario tooconfigure account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="6519b-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="6519b-134">La password è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="6519b-134">This password is an important security credential.</span></span>

    ![Account Microsoft - Genera nuova password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Account Microsoft - nuova password di copia hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="6519b-137">Casella di controllo hello indicante **il supporto di Live SDK** in hello **opzioni avanzate** sezione.</span><span class="sxs-lookup"><span data-stu-id="6519b-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="6519b-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6519b-138">Click **Save**.</span></span>

    ![Account Microsoft - Supporto Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="6519b-140">Aggiungere hello Microsoft account applicazione chiave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6519b-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="6519b-141">La federazione con l'account di Microsoft richiede un segreto client per tootrust di account di Microsoft Azure AD B2C per conto di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="6519b-142">È necessario toostore il secert di applicazione Microsoft account nel tenant di Azure Active Directory B2C:</span><span class="sxs-lookup"><span data-stu-id="6519b-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="6519b-143">Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**</span><span class="sxs-lookup"><span data-stu-id="6519b-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="6519b-144">Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="6519b-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="6519b-145">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6519b-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="6519b-146">Per **Opzioni** usare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="6519b-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="6519b-147">Per **Nome** usare `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="6519b-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="6519b-148">prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6519b-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="6519b-149">In hello **Secret** , immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6519b-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="6519b-150">Per **Uso chiave** usare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="6519b-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="6519b-151">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="6519b-151">Click **Create**</span></span>
9.  <span data-ttu-id="6519b-152">Verificare di aver creato la chiave hello `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="6519b-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="6519b-153">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="6519b-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="6519b-154">Se si desidera toosign gli utenti utilizzando l'Account Microsoft, è necessario toodefine Account Microsoft come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="6519b-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="6519b-155">In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica.</span><span class="sxs-lookup"><span data-stu-id="6519b-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="6519b-156">endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="6519b-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="6519b-157">Definire l'account Microsoft come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="6519b-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="6519b-158">Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6519b-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="6519b-159">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="6519b-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="6519b-160">Trovare hello `<ClaimsProviders>` sezione</span><span class="sxs-lookup"><span data-stu-id="6519b-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="6519b-161">Aggiungere il seguente frammento di codice XML in hello `ClaimsProviders` elemento:</span><span class="sxs-lookup"><span data-stu-id="6519b-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="6519b-162">Sostituire il valore `client_id` con l'ID client dell'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="6519b-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="6519b-163">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="6519b-164">Registrare hello Account Microsoft attestazioni provider tooSign backup oppure accedi viaggio utente</span><span class="sxs-lookup"><span data-stu-id="6519b-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="6519b-165">A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="6519b-166">Ora è necessario tooadd hello Account Microsoft identity provider tooyour utente `SignUpOrSignIn` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="6519b-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="6519b-167">toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="6519b-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="6519b-168">È quindi possibile aggiungere provider di identità Account Microsoft hello:</span><span class="sxs-lookup"><span data-stu-id="6519b-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="6519b-169">Se è stato copiato in precedenza hello `<UserJourneys>` elemento dal file di base del file di estensione di criteri toohello `TrustFrameworkExtensions.xml`, è possibile ignorare la sezione toothis.</span><span class="sxs-lookup"><span data-stu-id="6519b-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="6519b-170">Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="6519b-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="6519b-171">Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.</span><span class="sxs-lookup"><span data-stu-id="6519b-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="6519b-172">Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6519b-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="6519b-173">Se non esiste l'elemento hello, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="6519b-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="6519b-174">Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6519b-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="6519b-175">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="6519b-175">Display hello button</span></span>
<span data-ttu-id="6519b-176">Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="6519b-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="6519b-177">`<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi.</span><span class="sxs-lookup"><span data-stu-id="6519b-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="6519b-178">Se si aggiunge un `<ClaimsProviderSelection>` elemento per l'account Microsoft, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="6519b-179">tooadd questo elemento:</span><span class="sxs-lookup"><span data-stu-id="6519b-179">tooadd this element:</span></span>

1.  <span data-ttu-id="6519b-180">Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="6519b-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="6519b-181">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="6519b-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="6519b-182">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="6519b-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="6519b-183">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="6519b-183">Link hello button tooan action</span></span>
<span data-ttu-id="6519b-184">Ora che si dispone di un pulsante, è necessario toolink è tooan azione.</span><span class="sxs-lookup"><span data-stu-id="6519b-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="6519b-185">azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Account Microsoft tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="6519b-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="6519b-186">Collegamento azione tooan di hello pulsante profilo tecniche hello il collegamento per il provider di attestazioni di Account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6519b-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="6519b-187">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="6519b-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="6519b-188">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="6519b-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="6519b-189">Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello</span><span class="sxs-lookup"><span data-stu-id="6519b-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="6519b-190">Verificare `TechnicalProfileReferenceId` impostare l'ID profilo di tecniche toohello creato precedenti (MSA OIDC).</span><span class="sxs-lookup"><span data-stu-id="6519b-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="6519b-191">Caricare tenant tooyour di hello criteri</span><span class="sxs-lookup"><span data-stu-id="6519b-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="6519b-192">In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="6519b-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="6519b-193">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="6519b-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="6519b-194">Aprire hello **tutti i criteri** blade.</span><span class="sxs-lookup"><span data-stu-id="6519b-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="6519b-195">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="6519b-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="6519b-196">Controllare **sovrascrivere i criteri di hello eventuale** casella.</span><span class="sxs-lookup"><span data-stu-id="6519b-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="6519b-197">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello</span><span class="sxs-lookup"><span data-stu-id="6519b-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="6519b-198">Test dei criteri personalizzati di hello tramite Esegui</span><span class="sxs-lookup"><span data-stu-id="6519b-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="6519b-199">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="6519b-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="6519b-200">**Esegui ora** richiede almeno un'applicazione toobe preregistrate tenant hello.</span><span class="sxs-lookup"><span data-stu-id="6519b-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="6519b-201">toolearn tooregister applicazioni, vedere hello Azure Active Directory B2C [iniziare](active-directory-b2c-get-started.md) articolo o hello [registrazione dell'applicazione](active-directory-b2c-app-registration.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6519b-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="6519b-202">Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="6519b-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="6519b-203">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="6519b-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="6519b-204">È necessario essere in grado di toosign con account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6519b-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="6519b-205">[Facoltativo] Registrare il viaggio utente tooProfile Modifica provider di hello Account Microsoft attestazioni</span><span class="sxs-lookup"><span data-stu-id="6519b-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="6519b-206">È consigliabile provider di identità Account Microsoft hello tooadd anche tooyour utente `ProfileEdit` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="6519b-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="6519b-207">toomake è disponibile, si ripete hello ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="6519b-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="6519b-208">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="6519b-208">Display hello button</span></span>
1.  <span data-ttu-id="6519b-209">Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="6519b-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="6519b-210">Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="6519b-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="6519b-211">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="6519b-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="6519b-212">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="6519b-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="6519b-213">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="6519b-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="6519b-214">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="6519b-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="6519b-215">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="6519b-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="6519b-216">Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui</span><span class="sxs-lookup"><span data-stu-id="6519b-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="6519b-217">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="6519b-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="6519b-218">Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="6519b-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="6519b-219">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="6519b-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="6519b-220">È necessario essere in grado di toosign con account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6519b-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="6519b-221">Scaricare i file di criteri completa hello</span><span class="sxs-lookup"><span data-stu-id="6519b-221">Download hello complete policy files</span></span>
<span data-ttu-id="6519b-222">Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato hello Introduzione a criteri personalizzati analizzerà anziché utilizzare questi file di esempio.</span><span class="sxs-lookup"><span data-stu-id="6519b-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="6519b-223">File dei criteri di esempio di riferimento</span><span class="sxs-lookup"><span data-stu-id="6519b-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
