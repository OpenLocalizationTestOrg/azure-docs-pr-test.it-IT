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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="64707-103">Azure Active Directory B2C: Aggiungere Google+ come provider di identità OAuth2 tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="64707-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="64707-104">Questa guida viene spiegato come tooenable Accedi per gli utenti da Google + account tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="64707-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64707-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="64707-105">Prerequisites</span></span>

<span data-ttu-id="64707-106">Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="64707-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="64707-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="64707-107">These steps include:</span></span>

1.  <span data-ttu-id="64707-108">Creazione di un'applicazione di account Google+.</span><span class="sxs-lookup"><span data-stu-id="64707-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="64707-109">Aggiunta di hello Google + account applicazione chiave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="64707-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="64707-110">Aggiunta di criteri tooa provider di attestazioni</span><span class="sxs-lookup"><span data-stu-id="64707-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="64707-111">Registrazione hello Google + account attestazioni provider tooa utente viaggio</span><span class="sxs-lookup"><span data-stu-id="64707-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="64707-112">Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="64707-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="64707-113">Creare un'applicazione di account Google+</span><span class="sxs-lookup"><span data-stu-id="64707-113">Create a Google+ account application</span></span>
<span data-ttu-id="64707-114">toouse Google + come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Google + e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="64707-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="64707-115">È possibile registrare un'applicazione Google+ qui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="64707-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="64707-116">Passare toohello [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google +.</span><span class="sxs-lookup"><span data-stu-id="64707-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="64707-117">Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="64707-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="64707-118">Fare clic su hello **menu progetti**.</span><span class="sxs-lookup"><span data-stu-id="64707-118">Click on hello **Projects menu**.</span></span>

    ![Account Google+ - Selezionare il progetto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="64707-120">Fare clic su hello  **+**  pulsante.</span><span class="sxs-lookup"><span data-stu-id="64707-120">Click on hello **+** button.</span></span>

    ![Account Google+ - Creare un nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="64707-122">Fare clic su un **Nome progetto** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="64707-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Account Google+ - Nuovo progetto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="64707-124">Attendere che il progetto hello è pronto e fare clic su hello **menu progetti**.</span><span class="sxs-lookup"><span data-stu-id="64707-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Account di Google + - attendere il nuovo progetto toouse pronto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="64707-126">Fare clic sul nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="64707-126">Click on your project name.</span></span>

    ![Account di Google + - nuovo progetto selezionare hello](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="64707-128">Fare clic su **API Manager** e quindi fare clic su **credenziali** nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="64707-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="64707-129">Fare clic su hello **schermata consenso OAuth** scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="64707-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Account Google+ - Impostare la schermata del consenso OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="64707-131">Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="64707-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="64707-133">Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="64707-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - Creare nuove credenziali dell'applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="64707-135">In **Tipo di applicazione** selezionare **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="64707-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Selezionare il tipo di applicazione](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="64707-137">Fornire un **nome** per l'applicazione, immettere `https://login.microsoftonline.com` in hello **autorizzato JavaScript origins** , campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URI**campo.</span><span class="sxs-lookup"><span data-stu-id="64707-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="64707-138">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="64707-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="64707-139">Hello **{tenant}** valore è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="64707-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="64707-140">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="64707-140">Click **Create**.</span></span>

    ![Google+ - Specificare le origini JavaScript autorizzate e gli URI di reindirizzamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="64707-142">Copiare i valori hello di **Id Client** e **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="64707-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="64707-143">È necessario Google + entrambi tooconfigure come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="64707-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="64707-144">**Segreto client** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="64707-144">**Client secret** is an important security credential.</span></span>

    ![Google + - valori hello copia della chiave privata Client e l'Id client](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="64707-146">Aggiungere hello Google + account applicazione chiave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="64707-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="64707-147">La federazione con Google + account richiede un segreto client per Google + account tootrust Azure Active Directory B2C per conto di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="64707-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="64707-148">È necessario toostore il segreto dell'applicazione Google + nel tenant di Azure Active Directory B2C:</span><span class="sxs-lookup"><span data-stu-id="64707-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="64707-149">Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**</span><span class="sxs-lookup"><span data-stu-id="64707-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="64707-150">Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="64707-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="64707-151">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="64707-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="64707-152">Per **Opzioni** usare **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="64707-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="64707-153">Per **Nome** usare `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="64707-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="64707-154">prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="64707-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="64707-155">In hello **Secret** , immettere il segreto dell'applicazione Microsoft da https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="64707-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="64707-156">Per **Uso chiave** usare **Firma**.</span><span class="sxs-lookup"><span data-stu-id="64707-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="64707-157">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="64707-157">Click **Create**</span></span>
9.  <span data-ttu-id="64707-158">Verificare di aver creato la chiave hello `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="64707-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="64707-159">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="64707-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="64707-160">Se si desidera toosign gli utenti utilizzando account di Google +, è necessario toodefine Google + account come un provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="64707-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="64707-161">In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica.</span><span class="sxs-lookup"><span data-stu-id="64707-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="64707-162">endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="64707-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="64707-163">Definire l'account Google+ come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="64707-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="64707-164">Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="64707-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="64707-165">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="64707-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="64707-166">Trovare hello `<ClaimsProviders>` sezione</span><span class="sxs-lookup"><span data-stu-id="64707-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="64707-167">Aggiungere hello seguente frammento di codice XML in hello `ClaimsProviders` elemento e sostituire `client_id` valore con Google + ID account personale dell'applicazione client prima di salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="64707-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

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
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="64707-168">Registrare hello Google + account attestazioni provider tooSign backup o accedere al proprio processo utente</span><span class="sxs-lookup"><span data-stu-id="64707-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="64707-169">configurare il provider di identità Hello.</span><span class="sxs-lookup"><span data-stu-id="64707-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="64707-170">Non è tuttavia disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello.</span><span class="sxs-lookup"><span data-stu-id="64707-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="64707-171">Aggiungere hello Google + account identità tooyour utente del provider `SignUpOrSignIn` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="64707-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="64707-172">toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="64707-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="64707-173">È quindi possibile aggiungere hello Google + account provider di identità:</span><span class="sxs-lookup"><span data-stu-id="64707-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="64707-174">Se è stato copiato hello `<UserJourneys>` elemento dal file di base del file di estensione di criteri toohello (TrustFrameworkExtensions.xml), è possibile ignorare la sezione toothis.</span><span class="sxs-lookup"><span data-stu-id="64707-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="64707-175">Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="64707-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="64707-176">Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.</span><span class="sxs-lookup"><span data-stu-id="64707-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="64707-177">Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="64707-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="64707-178">Se non esiste l'elemento hello, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="64707-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="64707-179">Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="64707-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="64707-180">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="64707-180">Display hello button</span></span>
<span data-ttu-id="64707-181">Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="64707-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="64707-182">`<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi.</span><span class="sxs-lookup"><span data-stu-id="64707-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="64707-183">Se si aggiunge un `<ClaimsProviderSelection>` elemento per account di Google +, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="64707-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="64707-184">tooadd questo elemento:</span><span class="sxs-lookup"><span data-stu-id="64707-184">tooadd this element:</span></span>

1.  <span data-ttu-id="64707-185">Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="64707-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="64707-186">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="64707-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="64707-187">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="64707-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="64707-188">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="64707-188">Link hello button tooan action</span></span>
<span data-ttu-id="64707-189">Ora che si dispone di un pulsante, è necessario toolink è tooan azione.</span><span class="sxs-lookup"><span data-stu-id="64707-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="64707-190">azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con Google + account tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="64707-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="64707-191">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="64707-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="64707-192">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="64707-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="64707-193">Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello</span><span class="sxs-lookup"><span data-stu-id="64707-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="64707-194">Verificare `TechnicalProfileReferenceId` impostare l'ID del profilo di tecniche toohello precedenti (Google OAUTH) è stato creato.</span><span class="sxs-lookup"><span data-stu-id="64707-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="64707-195">Caricare tenant tooyour di hello criteri</span><span class="sxs-lookup"><span data-stu-id="64707-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="64707-196">In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="64707-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="64707-197">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="64707-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="64707-198">Aprire hello **tutti i criteri** blade.</span><span class="sxs-lookup"><span data-stu-id="64707-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="64707-199">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="64707-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="64707-200">Controllare **sovrascrivere i criteri di hello eventuale** casella.</span><span class="sxs-lookup"><span data-stu-id="64707-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="64707-201">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello</span><span class="sxs-lookup"><span data-stu-id="64707-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="64707-202">Test dei criteri personalizzati di hello tramite Esegui</span><span class="sxs-lookup"><span data-stu-id="64707-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="64707-203">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="64707-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="64707-204">**Esegui ora** richiede almeno un'applicazione toobe preregistrate tenant hello.</span><span class="sxs-lookup"><span data-stu-id="64707-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="64707-205">toolearn tooregister applicazioni, vedere hello Azure Active Directory B2C [iniziare](active-directory-b2c-get-started.md) articolo o hello [registrazione dell'applicazione](active-directory-b2c-app-registration.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="64707-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="64707-206">Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="64707-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="64707-207">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="64707-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="64707-208">È necessario essere in grado di toosign con Google + account.</span><span class="sxs-lookup"><span data-stu-id="64707-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="64707-209">[Facoltativo] Registrare hello Google + account attestazioni provider tooProfile modifica utente viaggio</span><span class="sxs-lookup"><span data-stu-id="64707-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="64707-210">È consigliabile tooadd hello Google + account provider di identità anche tooyour utente `ProfileEdit` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="64707-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="64707-211">toomake è disponibile, si ripete hello ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="64707-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="64707-212">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="64707-212">Display hello button</span></span>
1.  <span data-ttu-id="64707-213">Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="64707-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="64707-214">Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="64707-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="64707-215">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="64707-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="64707-216">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="64707-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="64707-217">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="64707-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="64707-218">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="64707-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="64707-219">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="64707-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="64707-220">Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui</span><span class="sxs-lookup"><span data-stu-id="64707-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="64707-221">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="64707-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="64707-222">Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="64707-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="64707-223">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="64707-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="64707-224">È necessario essere in grado di toosign con Google + account.</span><span class="sxs-lookup"><span data-stu-id="64707-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="64707-225">Scaricare i file di criteri completa hello</span><span class="sxs-lookup"><span data-stu-id="64707-225">Download hello complete policy files</span></span>
<span data-ttu-id="64707-226">Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato hello Introduzione a criteri personalizzati analizzerà anziché utilizzare questi file di esempio.</span><span class="sxs-lookup"><span data-stu-id="64707-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="64707-227">File dei criteri di esempio di riferimento</span><span class="sxs-lookup"><span data-stu-id="64707-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
