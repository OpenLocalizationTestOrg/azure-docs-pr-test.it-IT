---
title: 'Azure Active Directory B2C: aggiunta di un provider SAML Salesforce usando i criteri personalizzati | Microsoft Docs'
description: Informazioni su come creare e gestire i criteri personalizzati di Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="692b7-103">Azure Active Directory B2C: eseguire l'accesso con account Salesforce tramite SAML</span><span class="sxs-lookup"><span data-stu-id="692b7-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="692b7-104">Questo articolo illustra come usare i [criteri personalizzati](active-directory-b2c-overview-custom.md) per impostare l'accesso per gli utenti da un'organizzazione Salesforce specifica.</span><span class="sxs-lookup"><span data-stu-id="692b7-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="692b7-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="692b7-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="692b7-106">Configurazione di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="692b7-106">Azure AD B2C setup</span></span>

<span data-ttu-id="692b7-107">Assicurarsi di avere completato tutti i passaggi di [introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C),</span><span class="sxs-lookup"><span data-stu-id="692b7-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="692b7-108">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="692b7-108">These include:</span></span>

* <span data-ttu-id="692b7-109">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="692b7-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="692b7-110">Creare un'applicazione Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="692b7-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="692b7-111">Registrare due applicazioni con motore di criteri.</span><span class="sxs-lookup"><span data-stu-id="692b7-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="692b7-112">Impostare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="692b7-112">Set up keys.</span></span>
* <span data-ttu-id="692b7-113">installare il pacchetto Starter.</span><span class="sxs-lookup"><span data-stu-id="692b7-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="692b7-114">Configurazione di Salesforce</span><span class="sxs-lookup"><span data-stu-id="692b7-114">Salesforce setup</span></span>

<span data-ttu-id="692b7-115">In questo articolo si presuppone che siano già state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="692b7-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="692b7-116">Iscrizione a un account Salesforce.</span><span class="sxs-lookup"><span data-stu-id="692b7-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="692b7-117">È possibile iscriversi per ottenere un [account Developer Edition gratuito](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="692b7-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="692b7-118">[Configurazione di un dominio personale](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) per la propria organizzazione Salesforce.</span><span class="sxs-lookup"><span data-stu-id="692b7-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="692b7-119">Configurare Salesforce in modo che gli utenti possano eseguire la federazione</span><span class="sxs-lookup"><span data-stu-id="692b7-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="692b7-120">Per agevolare la comunicazione tra Azure AD B2C e Salesforce, è necessario ottenere l'URL dei metadati di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="692b7-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="692b7-121">Configurare Salesforce come provider di identità</span><span class="sxs-lookup"><span data-stu-id="692b7-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="692b7-122">Questo articolo presuppone che si stia usando [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="692b7-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="692b7-123">[Eseguire l'accesso a Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="692b7-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="692b7-124">In **Settings** (Impostazioni) nel menu di sinistra espandere **Identity** (Identità) e quindi fare clic su **Identity Provider** (Provider di identità).</span><span class="sxs-lookup"><span data-stu-id="692b7-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="692b7-125">Fare clic su **Enable Identity Provider** (Abilita provider di identità).</span><span class="sxs-lookup"><span data-stu-id="692b7-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="692b7-126">In **Select the certificate** (Selezionare il certificato) selezionare il certificato che si desidera venga usato da Salesforce per comunicare con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="692b7-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="692b7-127">È possibile usare il certificato predefinito. Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="692b7-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="692b7-128">Creare un'app connessa in Salesforce</span><span class="sxs-lookup"><span data-stu-id="692b7-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="692b7-129">Nella pagina **Identity Provider** (Provider di identità) passare a **Service Providers** (Provider di servizi).</span><span class="sxs-lookup"><span data-stu-id="692b7-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="692b7-130">Fare clic su **Service Providers are now created via Connected Apps. Click here** (I provider di servizi vengono ora creati tramite app connesse. Fare clic qui).</span><span class="sxs-lookup"><span data-stu-id="692b7-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="692b7-131">In **Basic Information** (Informazioni di base) immettere i valori richiesti per l'app connessa.</span><span class="sxs-lookup"><span data-stu-id="692b7-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="692b7-132">In **Web App Settings** (Impostazioni app Web), selezionare la casella di controllo **Enable SAML** (Abilita SAML).</span><span class="sxs-lookup"><span data-stu-id="692b7-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="692b7-133">Nel campo **Entity ID** (ID entità) immettere l'URL seguente.</span><span class="sxs-lookup"><span data-stu-id="692b7-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="692b7-134">Assicurarsi di sostituire il valore per `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="692b7-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="692b7-135">Nel campo **ACS URL** (URL ACS) immettere l'URL seguente.</span><span class="sxs-lookup"><span data-stu-id="692b7-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="692b7-136">Assicurarsi di sostituire il valore per `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="692b7-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="692b7-137">Lasciare i valori predefiniti per le altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="692b7-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="692b7-138">Scorrere l'elenco fino alla fine e quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="692b7-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="692b7-139">Ottenere l'URL dei metadati</span><span class="sxs-lookup"><span data-stu-id="692b7-139">Get the metadata URL</span></span>

1. <span data-ttu-id="692b7-140">Nella pagina di panoramica dell'app connessa fare clic su **Manage** (Gestisci).</span><span class="sxs-lookup"><span data-stu-id="692b7-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="692b7-141">Copiare il valore per **Metadata Discovery Endpoint** (Endpoint di individuazione dei metadati) e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="692b7-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="692b7-142">Questo valore sarà usato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="692b7-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="692b7-143">Configurare gli utenti di Salesforce per la federazione</span><span class="sxs-lookup"><span data-stu-id="692b7-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="692b7-144">Nella pagina **Manage** (Gestisci) dell'app connessa passare a **Profiles** (Profili).</span><span class="sxs-lookup"><span data-stu-id="692b7-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="692b7-145">Fare clic su **Manage Profiles** (Gestisci profili).</span><span class="sxs-lookup"><span data-stu-id="692b7-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="692b7-146">Selezionare i profili (o gruppi di utenti) di cui si intende eseguire la federazione con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="692b7-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="692b7-147">Come amministratore di sistema, è necessario selezionare la casella per **System Administrator** (Amministratore di sistema) in modo che sia possibile eseguire la federazione con l'account di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="692b7-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="692b7-148">Generare un certificato di firma per Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="692b7-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="692b7-149">Le richieste inviate a Salesforce devono essere firmate da Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="692b7-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="692b7-150">Per generare un certificato di firma, aprire Azure PowerShell ed eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="692b7-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="692b7-151">Assicurarsi di aggiornare il nome del tenant e la password nelle prime due righe.</span><span class="sxs-lookup"><span data-stu-id="692b7-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="692b7-152">Aggiungere un certificato di firma SAML ad Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="692b7-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="692b7-153">Caricare il certificato di firma nel tenant di Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="692b7-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="692b7-154">Passare al tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="692b7-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="692b7-155">Fare clic su **Impostazioni** > **Framework dell'esperienza di gestione delle identità** > **Chiavi dei criteri**.</span><span class="sxs-lookup"><span data-stu-id="692b7-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="692b7-156">Fare clic su **+Aggiungi** e quindi eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="692b7-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="692b7-157">Fare clic su **Opzioni** > **Carica**.</span><span class="sxs-lookup"><span data-stu-id="692b7-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="692b7-158">Immettere un **Nome**, ad esempio SAMLSigningCert.</span><span class="sxs-lookup"><span data-stu-id="692b7-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="692b7-159">Verrà automaticamente aggiunto il prefisso *B2C_1A_* al nome della chiave.</span><span class="sxs-lookup"><span data-stu-id="692b7-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="692b7-160">Per selezionare il certificato, selezionare **upload file control** (controllo carica file).</span><span class="sxs-lookup"><span data-stu-id="692b7-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="692b7-161">Immettere la password del certificato impostato nello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="692b7-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="692b7-162">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="692b7-162">Click **Create**.</span></span>
4. <span data-ttu-id="692b7-163">Verificare di avere creato una chiave, ad esempio B2C_1A_SAMLSigningCert.</span><span class="sxs-lookup"><span data-stu-id="692b7-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="692b7-164">Prendere nota del nome completo, incluso *B2C_1A_*.</span><span class="sxs-lookup"><span data-stu-id="692b7-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="692b7-165">Si farà riferimento a questa chiave in un secondo momento nei criteri.</span><span class="sxs-lookup"><span data-stu-id="692b7-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="692b7-166">Creare il provider di attestazioni SAML Salesforce nei criteri di base</span><span class="sxs-lookup"><span data-stu-id="692b7-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="692b7-167">Per consentire agli utenti di accedere usando Salesforce, è necessario definire Salesforce come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="692b7-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="692b7-168">In altri termini, è necessario specificare l'endpoint con cui comunicherà Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="692b7-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="692b7-169">L'endpoint *offrirà* un set di *attestazioni* che Azure AD B2C userà per verificare se un utente specifico è stato autenticato.</span><span class="sxs-lookup"><span data-stu-id="692b7-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="692b7-170">È possibile a tale scopo aggiungere un nodo `<ClaimsProvider>` per Salesforce nel file di estensione dei criteri:</span><span class="sxs-lookup"><span data-stu-id="692b7-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="692b7-171">Nella directory di lavoro aprire il file di estensione (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="692b7-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="692b7-172">Trovare la sezione `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="692b7-173">Se non esiste, crearla nel nodo radice.</span><span class="sxs-lookup"><span data-stu-id="692b7-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="692b7-174">Aggiungere un nuovo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="692b7-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="692b7-175">Nel nodo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="692b7-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="692b7-176">Modificare il valore per `<Domain>` in un valore univoco che distingua `<ClaimsProvider>` dagli altri provider di identità.</span><span class="sxs-lookup"><span data-stu-id="692b7-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="692b7-177">Aggiornare il valore per `<DisplayName>` con un nome visualizzato per il provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="692b7-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="692b7-178">Questo valore non viene usato attualmente.</span><span class="sxs-lookup"><span data-stu-id="692b7-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="692b7-179">Aggiornare il profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="692b7-179">Update the technical profile</span></span>

<span data-ttu-id="692b7-180">Per ottenere un token SAML da Salesforce, è necessario definire i protocolli che Azure AD B2C userà per comunicare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="692b7-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="692b7-181">Nell'elemento `<TechnicalProfile>` di `<ClaimsProvider>` eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="692b7-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="692b7-182">Aggiornare l'ID del nodo `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="692b7-183">Questo ID viene usato per fare riferimento al profilo tecnico da altre parti dei criteri.</span><span class="sxs-lookup"><span data-stu-id="692b7-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="692b7-184">Aggiornare il valore di `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="692b7-185">Questo valore verrà visualizzato sul pulsante di accesso nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="692b7-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="692b7-186">Aggiornare il valore di `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="692b7-187">Salesforce usa il protocollo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="692b7-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="692b7-188">Assicurarsi che il valore per `<Protocol>` sia **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="692b7-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="692b7-189">Aggiornare la sezione `<Metadata>` nel file XML precedente in modo da riflettere le impostazioni per l'account di Salesforce specifico.</span><span class="sxs-lookup"><span data-stu-id="692b7-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="692b7-190">Nel codice XML aggiornare i valori di metadati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="692b7-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="692b7-191">Aggiornare il valore di `<Item Key="PartnerEntity">` con l'URL dei metadati di Salesforce copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="692b7-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="692b7-192">L'URL si presenta nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="692b7-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="692b7-193">Nella sezione `<CryptographicKeys>` aggiornare il valore per entrambe le istanze di `StorageReferenceId` al nome della chiave del certificato di firma, ad esempio B2C_1A_SAMLSigningCert.</span><span class="sxs-lookup"><span data-stu-id="692b7-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="692b7-194">Caricare il file di estensione per la verifica</span><span class="sxs-lookup"><span data-stu-id="692b7-194">Upload the extension file for verification</span></span>

<span data-ttu-id="692b7-195">I criteri sono a questo punto configurati in modo che Azure AD B2C possa comunicare con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="692b7-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="692b7-196">Provare a caricare il file di estensione dei criteri per verificare che non vi siano problemi.</span><span class="sxs-lookup"><span data-stu-id="692b7-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="692b7-197">Per caricare il file di estensione dei criteri:</span><span class="sxs-lookup"><span data-stu-id="692b7-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="692b7-198">Nel tenant di Azure AD B2C passare al pannello **Tutti i criteri**.</span><span class="sxs-lookup"><span data-stu-id="692b7-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="692b7-199">Selezionare la casella di controllo **Sovrascrivi il criterio se esistente**.</span><span class="sxs-lookup"><span data-stu-id="692b7-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="692b7-200">Caricare il file di estensione (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="692b7-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="692b7-201">Verificare che la relativa convalida abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="692b7-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="692b7-202">Registrare il provider di attestazioni SAML Salesforce in un percorso utente</span><span class="sxs-lookup"><span data-stu-id="692b7-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="692b7-203">È ora necessario aggiungere il provider di identità SAML Salesforce in uno dei percorsi utente.</span><span class="sxs-lookup"><span data-stu-id="692b7-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="692b7-204">Il provider di identità è a questo punto configurato, ma non è disponibile in alcuna delle pagine di iscrizione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="692b7-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="692b7-205">Per aggiungere il provider di identità a una pagina di accesso, creare prima di tutto un duplicato di un percorso utente di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="692b7-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="692b7-206">Modificare quindi il modello in modo che includa anche il provider di identità di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692b7-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="692b7-207">Aprire il file di base dei criteri, ad esempio TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="692b7-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="692b7-208">Individuare l'elemento `<UserJourneys>` e quindi copiare l'intero valore `<UserJourney>`, incluso Id=”SignUpOrSignIn”.</span><span class="sxs-lookup"><span data-stu-id="692b7-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="692b7-209">Aprire il file di estensione, ad esempio TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="692b7-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="692b7-210">Trovare l'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="692b7-211">Se l'elemento non esiste, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="692b7-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="692b7-212">Incollare l'intero `<UserJourney>` copiato come figlio dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="692b7-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="692b7-213">Rinominare l'ID del nuovo `<UserJourney>`, ad esempio, SignUpOrSignUsingContoso.</span><span class="sxs-lookup"><span data-stu-id="692b7-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="692b7-214">Visualizzare il pulsante del provider di identità</span><span class="sxs-lookup"><span data-stu-id="692b7-214">Display the identity provider button</span></span>

<span data-ttu-id="692b7-215">L'elemento `<ClaimsProviderSelection>` è analogo a un pulsante di provider di identità in una pagina di iscrizione o accesso.</span><span class="sxs-lookup"><span data-stu-id="692b7-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="692b7-216">Se si aggiunge un elemento `<ClaimsProviderSelection>` per Salesforce, viene visualizzato un nuovo pulsante quando l'utente accede alla pagina.</span><span class="sxs-lookup"><span data-stu-id="692b7-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="692b7-217">Per visualizzare il pulsante del provider di identità:</span><span class="sxs-lookup"><span data-stu-id="692b7-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="692b7-218">Nell'elemento `<UserJourney>` creato trovare l'elemento `<OrchestrationStep>` con `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="692b7-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="692b7-219">Aggiungere il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="692b7-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="692b7-220">Impostare `TargetClaimsExchangeId` su un valore logico.</span><span class="sxs-lookup"><span data-stu-id="692b7-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="692b7-221">È consigliabile seguire la stessa convenzione degli altri, ad esempio *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="692b7-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="692b7-222">Collegare il pulsante del provider di identità a un'azione:</span><span class="sxs-lookup"><span data-stu-id="692b7-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="692b7-223">Il pulsante è a questo punto posizionato ed è necessario collegarlo a un'azione.</span><span class="sxs-lookup"><span data-stu-id="692b7-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="692b7-224">L'azione in questo caso riguarda la possibilità da parte di Azure AD B2C di comunicare con Salesforce per ricevere un token SAML.</span><span class="sxs-lookup"><span data-stu-id="692b7-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="692b7-225">Collegare a tal fine il profilo tecnico per il provider di attestazioni SAML Salesforce:</span><span class="sxs-lookup"><span data-stu-id="692b7-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="692b7-226">Nel nodo `<UserJourney>` trovare l'elemento `<OrchestrationStep>` con `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="692b7-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="692b7-227">Aggiungere il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="692b7-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="692b7-228">Aggiornare l'elemento `Id` allo stesso valore usato in precedenza per `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="692b7-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="692b7-229">Aggiornare `TechnicalProfileReferenceId` all'elemento `Id` del profilo tecnico creato in precedenza, ad esempio ContosoProfile.</span><span class="sxs-lookup"><span data-stu-id="692b7-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="692b7-230">Caricare il file di estensione aggiornato</span><span class="sxs-lookup"><span data-stu-id="692b7-230">Upload the updated extension file</span></span>

<span data-ttu-id="692b7-231">La modifica del file di estensione è completata.</span><span class="sxs-lookup"><span data-stu-id="692b7-231">You are done modifying the extension file.</span></span> <span data-ttu-id="692b7-232">Salvare e caricare il file.</span><span class="sxs-lookup"><span data-stu-id="692b7-232">Save and upload this file.</span></span> <span data-ttu-id="692b7-233">Verificare che tutte le convalide abbiano esito positivo.</span><span class="sxs-lookup"><span data-stu-id="692b7-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="692b7-234">Aggiornare il file della relying party</span><span class="sxs-lookup"><span data-stu-id="692b7-234">Update the relying party file</span></span>

<span data-ttu-id="692b7-235">È ora necessario aggiornare il file della relying party (RP) che avvierà il percorso utente appena creato:</span><span class="sxs-lookup"><span data-stu-id="692b7-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="692b7-236">Creare una copia di SignUpOrSignIn.xml nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="692b7-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="692b7-237">Rinominare quindi il file, ad esempio SignUpOrSignInWithAAD.xml.</span><span class="sxs-lookup"><span data-stu-id="692b7-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="692b7-238">Aprire il nuovo file e aggiornare l'attributo `PolicyId` per `<TrustFrameworkPolicy>` con un valore univoco,</span><span class="sxs-lookup"><span data-stu-id="692b7-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="692b7-239">che sarà il nome dei criteri, ad esempio SignUpOrSignInWithAAD.</span><span class="sxs-lookup"><span data-stu-id="692b7-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="692b7-240">Modificare l'attributo `ReferenceId` in `<DefaultUserJourney>` in modo che corrisponda all'elemento `Id` del nuovo percorso utente creato, ad esempio SignUpOrSignUsingContoso.</span><span class="sxs-lookup"><span data-stu-id="692b7-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="692b7-241">Salvare le modifiche e caricare il file.</span><span class="sxs-lookup"><span data-stu-id="692b7-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="692b7-242">Testare e risolvere i problemi</span><span class="sxs-lookup"><span data-stu-id="692b7-242">Test and troubleshoot</span></span>

<span data-ttu-id="692b7-243">Per testare i criteri personalizzati appena caricati, nel portale di Azure passare al pannello dei criteri e quindi fare clic su **Esegui ora**.</span><span class="sxs-lookup"><span data-stu-id="692b7-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="692b7-244">Se i test hanno esito negativo, vedere l'articolo sulla [risoluzione dei problemi relativi a criteri personalizzati](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="692b7-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="692b7-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="692b7-245">Next steps</span></span>

<span data-ttu-id="692b7-246">Inviare commenti e suggerimenti all'indirizzo [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="692b7-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
