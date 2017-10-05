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
ms.openlocfilehash: 8c981046ff41d3927ff60d6dc4f40366ae25ba74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="819fe-103">Azure Active Directory B2C: Aggiungere un account Microsoft come provider di identità tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="819fe-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="819fe-104">Questo articolo illustra come consentire agli utenti di accedere da un account Microsoft tramite l'utilizzo di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="819fe-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="819fe-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="819fe-105">Prerequisites</span></span>
<span data-ttu-id="819fe-106">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="819fe-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="819fe-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="819fe-107">These steps include:</span></span>

1.  <span data-ttu-id="819fe-108">Creazione di un'applicazione di account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="819fe-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="819fe-109">Aggiunta della chiave dell'applicazione di account Microsoft in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="819fe-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="819fe-110">Aggiunta di un provider di attestazioni nei criteri</span><span class="sxs-lookup"><span data-stu-id="819fe-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="819fe-111">Registrazione del provider di attestazioni dell'account Microsoft in un percorso utente</span><span class="sxs-lookup"><span data-stu-id="819fe-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="819fe-112">Caricamento dei criteri in un tenant di Azure AD B2C e test dei criteri</span><span class="sxs-lookup"><span data-stu-id="819fe-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="819fe-113">Creare un'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="819fe-113">Create a Microsoft account application</span></span>
<span data-ttu-id="819fe-114">Per usare un account Microsoft come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione di account Microsoft e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="819fe-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="819fe-115">È necessario un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="819fe-115">You need a Microsoft account.</span></span> <span data-ttu-id="819fe-116">Se non si ha un account, visitare il sito [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="819fe-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="819fe-117">Entrare nel [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali del proprio account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="819fe-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="819fe-118">Fare clic su **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="819fe-118">Click **Add an app**.</span></span>

    ![Account Microsoft - Aggiungere un'app](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="819fe-120">Specificare un **Nome** per l'applicazione e un **Indirizzo di posta elettronica di contatto**, deselezionare l'opzione **Informazioni per l'utilizzo iniziale** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="819fe-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Account Microsoft - Registrare l'applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="819fe-122">Copiare il valore di **ID applicazione**. È necessario per configurare un account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="819fe-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Account Microsoft - Copiare il valore di ID applicazione](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="819fe-124">Fare clic su **Aggiungi piattaforma**</span><span class="sxs-lookup"><span data-stu-id="819fe-124">Click on **Add platform**</span></span>

    ![Account Microsoft - Aggiungi piattaforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="819fe-126">Scegliere **Web** dall'elenco di piattaforme.</span><span class="sxs-lookup"><span data-stu-id="819fe-126">From the platform list, choose **Web**.</span></span>

    ![Account Microsoft - Scegliere Web dall'elenco di piattaforme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="819fe-128">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **URI di reindirizzamento** .</span><span class="sxs-lookup"><span data-stu-id="819fe-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="819fe-129">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="819fe-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Account Microsoft - Impostare gli URL di reindirizzamento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="819fe-131">Fare clic su **Genera nuova password** nella sezione **Segreti applicazione**.</span><span class="sxs-lookup"><span data-stu-id="819fe-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="819fe-132">Copiare la nuova password visualizzata sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="819fe-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="819fe-133">È necessario per configurare un account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="819fe-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="819fe-134">La password è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="819fe-134">This password is an important security credential.</span></span>

    ![Account Microsoft - Genera nuova password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Account Microsoft - Copiare la nuova password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="819fe-137">Selezionare la casella **Supporto Live SDK** nella sezione **Opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="819fe-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="819fe-138">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="819fe-138">Click **Save**.</span></span>

    ![Account Microsoft - Supporto Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="819fe-140">Aggiungere la chiave dell'applicazione di account Microsoft in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="819fe-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="819fe-141">La federazione con account Microsoft richiede un segreto client per consentire all'account Microsoft di considerare attendibile Azure AD B2C per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="819fe-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="819fe-142">È necessario archiviare il segreto dell'applicazione di account Microsoft nel tenant di Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="819fe-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="819fe-143">Passare al tenant di Azure AD B2C e selezionare **B2C Settings** (Impostazioni B2C) > **Framework dell'esperienza di gestione delle identità**</span><span class="sxs-lookup"><span data-stu-id="819fe-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="819fe-144">Selezionare **Chiavi dei criteri** per visualizzare le chiavi disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="819fe-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="819fe-145">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="819fe-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="819fe-146">Per **Opzioni** usare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="819fe-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="819fe-147">Per **Nome** usare `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="819fe-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="819fe-148">È possibile che il prefisso `B2C_1A_` venga aggiunto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="819fe-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="819fe-149">Nella casella **Segreto** immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="819fe-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="819fe-150">Per **Uso chiave** usare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="819fe-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="819fe-151">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="819fe-151">Click **Create**</span></span>
9.  <span data-ttu-id="819fe-152">Confermare di avere creato la chiave `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="819fe-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="819fe-153">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="819fe-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="819fe-154">Per consentire agli utenti di accedere con un account Microsoft, è necessario definire l'account Microsoft come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="819fe-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="819fe-155">In altre parole, è necessario specificare un endpoint con cui comunichi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="819fe-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="819fe-156">L'endpoint offre un set di attestazioni che vengono usate da Azure AD B2C per verificare se un utente specifico è stato autenticato.</span><span class="sxs-lookup"><span data-stu-id="819fe-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="819fe-157">Definire l'account Microsoft come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="819fe-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="819fe-158">Aprire il file dei criteri di estensione (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="819fe-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="819fe-159">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="819fe-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="819fe-160">Trovare la sezione `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="819fe-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="819fe-161">Aggiungere il frammento XML seguente nell'elemento `ClaimsProviders`:</span><span class="sxs-lookup"><span data-stu-id="819fe-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="819fe-162">Sostituire il valore `client_id` con l'ID client dell'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="819fe-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="819fe-163">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="819fe-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="819fe-164">Registrare il provider di attestazioni dell'account Microsoft in un percorso utente di registrazione o di accesso</span><span class="sxs-lookup"><span data-stu-id="819fe-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="819fe-165">Il provider di identità è a questo punto configurato, ma non è disponibile in alcuna delle schermate di iscrizione/accesso.</span><span class="sxs-lookup"><span data-stu-id="819fe-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="819fe-166">È necessario ora aggiungere il provider di identità dell'account Microsoft al percorso utente `SignUpOrSignIn` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="819fe-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="819fe-167">Per renderlo disponibile, si crea un duplicato di un modello di processo utente esistente</span><span class="sxs-lookup"><span data-stu-id="819fe-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="819fe-168">e si aggiunge il provider di identità dell'account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="819fe-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="819fe-169">Se in precedenza l'elemento `<UserJourneys>` è stato copiato dal file di base dei criteri al file di estensione `TrustFrameworkExtensions.xml`, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="819fe-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="819fe-170">Aprire il file di base dei criteri, ad esempio TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="819fe-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="819fe-171">Trovare l'elemento `<UserJourneys>` e copiare l'intero contenuto del nodo `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="819fe-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="819fe-172">Aprire il file di estensione, ad esempio TrustFrameworkExtensions.xml, e trovare l'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="819fe-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="819fe-173">Se l'elemento non esiste, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="819fe-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="819fe-174">Incollare l'intero contenuto del nodo `<UserJournesy>` copiato come figlio dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="819fe-174">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="819fe-175">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="819fe-175">Display the button</span></span>
<span data-ttu-id="819fe-176">L'elemento `<ClaimsProviderSelections>` definisce l'elenco delle opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="819fe-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="819fe-177">L'elemento `<ClaimsProviderSelection>` è analogo a un pulsante del provider di identità in una pagina di registrazione/accesso.</span><span class="sxs-lookup"><span data-stu-id="819fe-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="819fe-178">Se si aggiunge un elemento `<ClaimsProviderSelection>` per l'account Microsoft, viene visualizzato un nuovo pulsante quando un utente apre la pagina.</span><span class="sxs-lookup"><span data-stu-id="819fe-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="819fe-179">Per aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="819fe-179">To add this element:</span></span>

1.  <span data-ttu-id="819fe-180">Trovare il nodo `<UserJourney>` che include `Id="SignUpOrSignIn"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="819fe-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="819fe-181">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="819fe-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="819fe-182">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="819fe-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="819fe-183">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="819fe-183">Link the button to an action</span></span>
<span data-ttu-id="819fe-184">Ora che il pulsante è stato posizionato, è necessario collegarlo a un'azione.</span><span class="sxs-lookup"><span data-stu-id="819fe-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="819fe-185">L'azione, in questo caso, consiste nel far comunicare Azure AD B2C con l'account Microsoft per ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="819fe-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="819fe-186">È possibile farlo collegando il profilo tecnico per il provider di attestazioni dell'account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="819fe-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="819fe-187">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="819fe-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="819fe-188">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="819fe-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="819fe-189">Verificare che `Id` sia impostato sullo stesso valore di `TargetClaimsExchangeId` riportato nella sezione precedente</span><span class="sxs-lookup"><span data-stu-id="819fe-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="819fe-190">Verificare che l'ID `TechnicalProfileReferenceId` sia impostato sul profilo tecnico creato in precedenza (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="819fe-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="819fe-191">Caricare i criteri nel tenant</span><span class="sxs-lookup"><span data-stu-id="819fe-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="819fe-192">Nel [portale di Azure](https://portal.azure.com) passare al [contesto del tenant di Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e aprire il pannello **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="819fe-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="819fe-193">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="819fe-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="819fe-194">Aprire il pannello **Tutti i criteri**.</span><span class="sxs-lookup"><span data-stu-id="819fe-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="819fe-195">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="819fe-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="819fe-196">Selezionare la casella **Sovrascrivi il criterio se esistente**.</span><span class="sxs-lookup"><span data-stu-id="819fe-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="819fe-197">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non presenti errori di convalida</span><span class="sxs-lookup"><span data-stu-id="819fe-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="819fe-198">Testare i criteri personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="819fe-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="819fe-199">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="819fe-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="819fe-200">Il comando **Esegui adesso** richiede che nel tenant sia preregistrata almeno un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="819fe-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="819fe-201">Per informazioni su come registrare le applicazioni, vedere l'articolo di [introduzione](active-directory-b2c-get-started.md) ad Azure AD B2C o l'articolo relativo alla [registrazione delle applicazioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="819fe-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="819fe-202">Aprire **B2C_1A_signup_signin**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="819fe-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="819fe-203">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="819fe-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="819fe-204">Dovrebbe essere possibile accedere usando un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="819fe-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="819fe-205">[Facoltativo] Registrare il provider di attestazioni dell'account Microsoft nel percorso utente Profile-Edit</span><span class="sxs-lookup"><span data-stu-id="819fe-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="819fe-206">È possibile aggiungere il provider di identità dell'account Microsoft anche al percorso utente `ProfileEdit` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="819fe-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="819fe-207">Per renderlo disponibile, ripetere gli ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="819fe-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="819fe-208">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="819fe-208">Display the button</span></span>
1.  <span data-ttu-id="819fe-209">Aprire il file di estensione dei criteri, ad esempio TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="819fe-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="819fe-210">Trovare il nodo `<UserJourney>` che include `Id="ProfileEdit"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="819fe-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="819fe-211">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="819fe-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="819fe-212">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="819fe-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="819fe-213">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="819fe-213">Link the button to an action</span></span>
1.  <span data-ttu-id="819fe-214">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="819fe-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="819fe-215">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="819fe-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="819fe-216">Testare i criteri Profile-Edit personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="819fe-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="819fe-217">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="819fe-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="819fe-218">Aprire **B2C_1A_ProfileEdit**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="819fe-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="819fe-219">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="819fe-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="819fe-220">Dovrebbe essere possibile accedere usando un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="819fe-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="819fe-221">Scaricare i file dei criteri completi</span><span class="sxs-lookup"><span data-stu-id="819fe-221">Download the complete policy files</span></span>
<span data-ttu-id="819fe-222">Facoltativo: anziché usare i file di esempio, per creare lo scenario è consigliabile usare file di criteri personalizzati dopo aver completato la procedura Introduzione ai criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="819fe-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="819fe-223">File dei criteri di esempio di riferimento</span><span class="sxs-lookup"><span data-stu-id="819fe-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
