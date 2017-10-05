---
title: "Azure Active Directory B2C: Aggiungere Google+ come provider di identità OAuth2 tramite criteri personalizzati"
description: "Esempio di utilizzo di Google+ come provider di identità basato sul protocollo OAuth2"
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
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="80c66-103">Azure Active Directory B2C: Aggiungere Google+ come provider di identità OAuth2 tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="80c66-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="80c66-104">Questa guida illustra come consentire agli utenti di accedere da un account Google+ tramite l'utilizzo di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="80c66-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80c66-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="80c66-105">Prerequisites</span></span>

<span data-ttu-id="80c66-106">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="80c66-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="80c66-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="80c66-107">These steps include:</span></span>

1.  <span data-ttu-id="80c66-108">Creazione di un'applicazione di account Google+.</span><span class="sxs-lookup"><span data-stu-id="80c66-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="80c66-109">Aggiunta della chiave dell'applicazione di account Google+ in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="80c66-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="80c66-110">Aggiunta di un provider di attestazioni nei criteri</span><span class="sxs-lookup"><span data-stu-id="80c66-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="80c66-111">Registrazione del provider di attestazioni dell'account Google+ in un percorso utente</span><span class="sxs-lookup"><span data-stu-id="80c66-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="80c66-112">Caricamento dei criteri in un tenant di Azure AD B2C e test dei criteri</span><span class="sxs-lookup"><span data-stu-id="80c66-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="80c66-113">Creare un'applicazione di account Google+</span><span class="sxs-lookup"><span data-stu-id="80c66-113">Create a Google+ account application</span></span>
<span data-ttu-id="80c66-114">Per usare Google+ come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione Google+ e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="80c66-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="80c66-115">È possibile registrare un'applicazione Google+ qui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="80c66-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="80c66-116">Visitare [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google+.</span><span class="sxs-lookup"><span data-stu-id="80c66-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="80c66-117">Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="80c66-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="80c66-118">Fare clic sul **menu Progetti**.</span><span class="sxs-lookup"><span data-stu-id="80c66-118">Click on the **Projects menu**.</span></span>

    ![Account Google+ - Selezionare il progetto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="80c66-120">Fare clic sul pulsante **+**.</span><span class="sxs-lookup"><span data-stu-id="80c66-120">Click on the **+** button.</span></span>

    ![Account Google+ - Creare un nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="80c66-122">Fare clic su un **Nome progetto** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="80c66-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Account Google+ - Nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="80c66-124">Attendere che il progetto sia pronto e fare clic sul **menu Progetti**.</span><span class="sxs-lookup"><span data-stu-id="80c66-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Account Google+ - Attendere che il nuovo progetto sia pronto per l'utilizzo](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="80c66-126">Fare clic sul nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="80c66-126">Click on your project name.</span></span>

    ![Account Google+ - Selezionare il nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="80c66-128">Fare clic su **Gestione API** e su **Credenziali** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="80c66-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="80c66-129">Fare clic sulla scheda **Schermata consenso OAuth** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="80c66-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Account Google+ - Impostare la schermata del consenso OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="80c66-131">Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="80c66-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="80c66-133">Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="80c66-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - Creare nuove credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="80c66-135">In **Tipo di applicazione** selezionare **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="80c66-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Selezionare il tipo di applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="80c66-137">Fornire un **Nome** per l'applicazione, immettere `https://login.microsoftonline.com` nel campo **Origini JavaScript Autorizzate** e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **URI di reindirizzamento autorizzati**.</span><span class="sxs-lookup"><span data-stu-id="80c66-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="80c66-138">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="80c66-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="80c66-139">Il valore **{tenant}** distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="80c66-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="80c66-140">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="80c66-140">Click **Create**.</span></span>

    ![Google+ - Specificare le origini JavaScript autorizzate e gli URI di reindirizzamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="80c66-142">Copiare i valori **ID client** e **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="80c66-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="80c66-143">Sono entrambi necessari per configurare Google+ come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="80c66-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="80c66-144">**Segreto client** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="80c66-144">**Client secret** is an important security credential.</span></span>

    ![Google+ - Copiare i valori di ID client e Segreto client](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="80c66-146">Aggiungere la chiave dell'applicazione di account Google+ in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="80c66-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="80c66-147">La federazione con account Google+ richiede un segreto client per consentire all'account Google+ di considerare attendibile Azure AD B2C per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80c66-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="80c66-148">È necessario archiviare il segreto dell'applicazione Google+ nel tenant di Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="80c66-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="80c66-149">Passare al tenant di Azure AD B2C e selezionare **B2C Settings** (Impostazioni B2C) > **Framework dell'esperienza di gestione delle identità**</span><span class="sxs-lookup"><span data-stu-id="80c66-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="80c66-150">Selezionare **Chiavi dei criteri** per visualizzare le chiavi disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="80c66-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="80c66-151">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="80c66-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="80c66-152">Per **Opzioni** usare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="80c66-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="80c66-153">Per **Nome** usare `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="80c66-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="80c66-154">È possibile che il prefisso `B2C_1A_` venga aggiunto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="80c66-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="80c66-155">Nella casella **Segreto** immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="80c66-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="80c66-156">Per **Uso chiave** usare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="80c66-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="80c66-157">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="80c66-157">Click **Create**</span></span>
9.  <span data-ttu-id="80c66-158">Confermare di avere creato la chiave `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="80c66-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="80c66-159">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="80c66-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="80c66-160">Per consentire agli utenti di accedere con un account Google+, è necessario definire l'account Google+ come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="80c66-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="80c66-161">In altre parole, è necessario specificare un endpoint con cui comunichi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80c66-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="80c66-162">L'endpoint offre un set di attestazioni che vengono usate da Azure AD B2C per verificare se un utente specifico è stato autenticato.</span><span class="sxs-lookup"><span data-stu-id="80c66-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="80c66-163">Definire l'account Google+ come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="80c66-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="80c66-164">Aprire il file dei criteri di estensione (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="80c66-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="80c66-165">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="80c66-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="80c66-166">Trovare la sezione `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="80c66-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="80c66-167">Aggiungere il seguente frammento XML nell'elemento `ClaimsProviders` e sostituire il valore `client_id` con l'ID client dell'applicazione di account Google+ prima di salvare il file.</span><span class="sxs-lookup"><span data-stu-id="80c66-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="80c66-168">Registrare il provider di attestazioni dell'account Google+ in un percorso utente di registrazione o di accesso</span><span class="sxs-lookup"><span data-stu-id="80c66-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="80c66-169">Il provider di identità è stato configurato,</span><span class="sxs-lookup"><span data-stu-id="80c66-169">The identity provider has been set up.</span></span>  <span data-ttu-id="80c66-170">ma non è disponibile in nessuna delle schermate di registrazione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="80c66-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="80c66-171">Aggiungere il provider di identità dell'account Google+ al percorso utente `SignUpOrSignIn` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="80c66-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="80c66-172">Per renderlo disponibile, si crea un duplicato di un modello di processo utente esistente</span><span class="sxs-lookup"><span data-stu-id="80c66-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="80c66-173">e si aggiunge il provider di identità dell'account Google+:</span><span class="sxs-lookup"><span data-stu-id="80c66-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="80c66-174">Se l'elemento `<UserJourneys>` è stato copiato dal file di base dei criteri al file di estensione (TrustFrameworkExtensions.xml), è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="80c66-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="80c66-175">Aprire il file di base dei criteri, ad esempio TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="80c66-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="80c66-176">Trovare l'elemento `<UserJourneys>` e copiare l'intero contenuto del nodo `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="80c66-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="80c66-177">Aprire il file di estensione, ad esempio TrustFrameworkExtensions.xml, e trovare l'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="80c66-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="80c66-178">Se l'elemento non esiste, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="80c66-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="80c66-179">Incollare l'intero contenuto del nodo `<UserJournesy>` copiato come figlio dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="80c66-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="80c66-180">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="80c66-180">Display the button</span></span>
<span data-ttu-id="80c66-181">L'elemento `<ClaimsProviderSelections>` definisce l'elenco delle opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="80c66-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="80c66-182">L'elemento `<ClaimsProviderSelection>` è analogo a un pulsante del provider di identità in una pagina di registrazione/accesso.</span><span class="sxs-lookup"><span data-stu-id="80c66-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="80c66-183">Se si aggiunge un elemento `<ClaimsProviderSelection>` per l'account Google+, viene visualizzato un nuovo pulsante quando un utente apre la pagina.</span><span class="sxs-lookup"><span data-stu-id="80c66-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="80c66-184">Per aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="80c66-184">To add this element:</span></span>

1.  <span data-ttu-id="80c66-185">Trovare il nodo `<UserJourney>` che include `Id="SignUpOrSignIn"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="80c66-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="80c66-186">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="80c66-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="80c66-187">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="80c66-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="80c66-188">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="80c66-188">Link the button to an action</span></span>
<span data-ttu-id="80c66-189">Ora che il pulsante è stato posizionato, è necessario collegarlo a un'azione.</span><span class="sxs-lookup"><span data-stu-id="80c66-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="80c66-190">L'azione, in questo caso, consiste nel far comunicare Azure AD B2C con l'account Google+ per ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="80c66-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="80c66-191">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="80c66-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="80c66-192">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="80c66-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="80c66-193">Verificare che `Id` sia impostato sullo stesso valore di `TargetClaimsExchangeId` riportato nella sezione precedente</span><span class="sxs-lookup"><span data-stu-id="80c66-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="80c66-194">Verificare che l'ID `TechnicalProfileReferenceId` sia impostato sul profilo tecnico creato in precedenza (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="80c66-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="80c66-195">Caricare i criteri nel tenant</span><span class="sxs-lookup"><span data-stu-id="80c66-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="80c66-196">Nel [portale di Azure](https://portal.azure.com) passare al [contesto del tenant di Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e aprire il pannello **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="80c66-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="80c66-197">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="80c66-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="80c66-198">Aprire il pannello **Tutti i criteri**.</span><span class="sxs-lookup"><span data-stu-id="80c66-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="80c66-199">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="80c66-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="80c66-200">Selezionare la casella **Sovrascrivi il criterio se esistente**.</span><span class="sxs-lookup"><span data-stu-id="80c66-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="80c66-201">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non presenti errori di convalida</span><span class="sxs-lookup"><span data-stu-id="80c66-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="80c66-202">Testare i criteri personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="80c66-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="80c66-203">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="80c66-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="80c66-204">Il comando **Esegui adesso** richiede che nel tenant sia preregistrata almeno un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80c66-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="80c66-205">Per informazioni su come registrare le applicazioni, vedere l'articolo di [introduzione](active-directory-b2c-get-started.md) ad Azure AD B2C o l'articolo relativo alla [registrazione delle applicazioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="80c66-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="80c66-206">Aprire **B2C_1A_signup_signin**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="80c66-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="80c66-207">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="80c66-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="80c66-208">Dovrebbe essere possibile accedere usando un account Google+.</span><span class="sxs-lookup"><span data-stu-id="80c66-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="80c66-209">[Facoltativo] Registrare il provider di attestazioni dell'account Google+ nel percorso utente Profile-Edit</span><span class="sxs-lookup"><span data-stu-id="80c66-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="80c66-210">È possibile aggiungere il provider di identità dell'account Google+ anche al percorso utente `ProfileEdit` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="80c66-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="80c66-211">Per renderlo disponibile, ripetere gli ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="80c66-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="80c66-212">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="80c66-212">Display the button</span></span>
1.  <span data-ttu-id="80c66-213">Aprire il file di estensione dei criteri, ad esempio TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="80c66-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="80c66-214">Trovare il nodo `<UserJourney>` che include `Id="ProfileEdit"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="80c66-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="80c66-215">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="80c66-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="80c66-216">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="80c66-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="80c66-217">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="80c66-217">Link the button to an action</span></span>
1.  <span data-ttu-id="80c66-218">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="80c66-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="80c66-219">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="80c66-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="80c66-220">Testare i criteri Profile-Edit personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="80c66-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="80c66-221">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="80c66-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="80c66-222">Aprire **B2C_1A_ProfileEdit**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="80c66-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="80c66-223">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="80c66-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="80c66-224">Dovrebbe essere possibile accedere usando un account Google+.</span><span class="sxs-lookup"><span data-stu-id="80c66-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="80c66-225">Scaricare i file dei criteri completi</span><span class="sxs-lookup"><span data-stu-id="80c66-225">Download the complete policy files</span></span>
<span data-ttu-id="80c66-226">Facoltativo: anziché usare i file di esempio, per creare lo scenario è consigliabile usare file di criteri personalizzati dopo aver completato la procedura Introduzione ai criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="80c66-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="80c66-227">File dei criteri di esempio di riferimento</span><span class="sxs-lookup"><span data-stu-id="80c66-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
