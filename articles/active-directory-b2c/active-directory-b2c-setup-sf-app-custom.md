---
title: 'Azure Active Directory B2C: aggiunta di un provider SAML Salesforce usando i criteri personalizzati | Microsoft Docs'
description: Per ulteriori informazioni vedere toocreate e gestire i criteri personalizzati di Azure Active Directory B2C.
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
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="8a4a6-103">Azure Active Directory B2C: eseguire l'accesso con account Salesforce tramite SAML</span><span class="sxs-lookup"><span data-stu-id="8a4a6-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="8a4a6-104">In questo articolo illustra come toouse [criteri personalizzati](active-directory-b2c-overview-custom.md) tooset backup Accedi per gli utenti da un'organizzazione Salesforce specifico.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a4a6-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8a4a6-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="8a4a6-106">Configurazione di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8a4a6-106">Azure AD B2C setup</span></span>

<span data-ttu-id="8a4a6-107">Assicurarsi di aver completato tutti i passaggi di hello che mostrano come troppo[Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="8a4a6-108">incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-108">These include:</span></span>

* <span data-ttu-id="8a4a6-109">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8a4a6-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="8a4a6-110">Creare un'applicazione Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8a4a6-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="8a4a6-111">Registrare due applicazioni con motore di criteri.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="8a4a6-112">Impostare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-112">Set up keys.</span></span>
* <span data-ttu-id="8a4a6-113">Impostare il pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="8a4a6-114">Configurazione di Salesforce</span><span class="sxs-lookup"><span data-stu-id="8a4a6-114">Salesforce setup</span></span>

<span data-ttu-id="8a4a6-115">In questo articolo si presuppone di aver già eseguito seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="8a4a6-116">Iscrizione a un account Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="8a4a6-117">È possibile iscriversi per ottenere un [account Developer Edition gratuito](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="8a4a6-118">[Configurazione di un dominio personale](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) per la propria organizzazione Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="8a4a6-119">Configurare Salesforce in modo che gli utenti possano eseguire la federazione</span><span class="sxs-lookup"><span data-stu-id="8a4a6-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="8a4a6-120">toohelp Azure Active Directory B2C comunicare con Salesforce, è necessario l'URL dei metadati di tooget hello Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="8a4a6-121">Configurare Salesforce come provider di identità</span><span class="sxs-lookup"><span data-stu-id="8a4a6-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="8a4a6-122">Questo articolo presuppone che si stia usando [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="8a4a6-123">[Accedi tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="8a4a6-124">Nella hello sinistra dal menu in **impostazioni**, espandere **identità**, quindi fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="8a4a6-125">Fare clic su **Enable Identity Provider** (Abilita provider di identità).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="8a4a6-126">In **certificato selezionare hello**, selezionare il certificato di hello desiderato toocommunicate toouse Salesforce con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="8a4a6-127">(È possibile utilizzare certificato predefinito hello). Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="8a4a6-128">Creare un'app connessa in Salesforce</span><span class="sxs-lookup"><span data-stu-id="8a4a6-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="8a4a6-129">In hello **Provider di identità** pagina, andare troppo**i provider di servizi**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="8a4a6-130">Fare clic su **Service Providers are now created via Connected Apps. Click here** (I provider di servizi vengono ora creati tramite app connesse. Fare clic qui).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="8a4a6-131">In **le informazioni di base**, immettere i valori hello necessario per l'app connessa.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="8a4a6-132">In **impostazioni App Web**selezionare hello **Enable SAML** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="8a4a6-133">In hello **ID entità** immettere l'URL seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="8a4a6-134">Assicurarsi di sostituire il valore di hello per `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="8a4a6-135">In hello **URL ACS** immettere l'URL seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="8a4a6-136">Assicurarsi di sostituire il valore di hello per `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="8a4a6-137">Lasciare i valori predefiniti di hello per tutte le altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="8a4a6-138">Scorrere fino alla fine di toohello dell'elenco di hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="8a4a6-139">Ottenere l'URL dei metadati hello</span><span class="sxs-lookup"><span data-stu-id="8a4a6-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="8a4a6-140">Nella pagina di panoramica hello dell'app connessa, fare clic su **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="8a4a6-141">Copiare il valore di hello per **Endpoint di individuazione dei metadati**, quindi salvarlo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="8a4a6-142">Questo valore sarà usato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="8a4a6-143">Impostare toofederate agli utenti di Salesforce</span><span class="sxs-lookup"><span data-stu-id="8a4a6-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="8a4a6-144">In hello **Gestisci** pagina dell'app connessa, andare troppo**profili**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="8a4a6-145">Fare clic su **Manage Profiles** (Gestisci profili).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="8a4a6-146">Selezionare i profili di hello (o gruppi di utenti) che si desidera toofederate con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="8a4a6-147">Come amministratore di sistema, selezionare hello **amministratore di sistema** casella di controllo in modo che è possibile attuare la federazione usando l'account di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="8a4a6-148">Generare un certificato di firma per Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8a4a6-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="8a4a6-149">Le richieste inviate tooSalesforce necessità toobe firmato da Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="8a4a6-150">toogenerate un certificato di firma, aprire Azure PowerShell e quindi eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="8a4a6-151">Assicurarsi di aggiornare il nome di tenant hello e una password in due linee superiore hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="8a4a6-152">Aggiungere hello SAML firma certificato tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8a4a6-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="8a4a6-153">Caricare hello tenant di Azure Active Directory B2C tooyour certificato di firma:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="8a4a6-154">Passare il tenant di Azure Active Directory B2C tooyour.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="8a4a6-155">Fare clic su **Impostazioni** > **Framework dell'esperienza di gestione delle identità** > **Chiavi dei criteri**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="8a4a6-156">Fare clic su **+Aggiungi** e quindi eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="8a4a6-157">Fare clic su **Opzioni** > **Carica**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="8a4a6-158">Immettere un **Nome**, ad esempio SAMLSigningCert.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="8a4a6-159">prefisso Hello *B2C_1A_* viene aggiunto automaticamente toohello nome della chiave.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="8a4a6-160">tooselect il certificato, seleziona **file controllo caricamento**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="8a4a6-161">Immettere la password del certificato hello impostati nello script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="8a4a6-162">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-162">Click **Create**.</span></span>
4. <span data-ttu-id="8a4a6-163">Verificare di avere creato una chiave, ad esempio B2C_1A_SAMLSigningCert.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="8a4a6-164">Prendere nota del nome completo di hello (inclusi *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="8a4a6-165">Si farà riferimento toothis chiave in un secondo momento nei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="8a4a6-166">Creare provider di attestazioni SAML Salesforce hello nei criteri di base</span><span class="sxs-lookup"><span data-stu-id="8a4a6-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="8a4a6-167">Consentire agli utenti di accedere con Salesforce, è necessario toodefine Salesforce come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="8a4a6-168">In altre parole, è necessario endpoint hello toospecify comunicare con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="8a4a6-169">endpoint Hello verrà *fornire* un set di *attestazioni* che Azure Active Directory B2C utilizza tooverify che ha autenticato un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="8a4a6-170">toodo, aggiungere un `<ClaimsProvider>` per Salesforce nel file di estensione hello dei criteri:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="8a4a6-171">Nella directory di lavoro, aprire il file di estensione hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="8a4a6-172">Trovare hello `<ClaimsProviders>` sezione.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="8a4a6-173">Se non esiste, crearla nel nodo radice hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="8a4a6-174">Aggiungere un nuovo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="8a4a6-175">In hello `<ClaimsProvider>` nodo:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="8a4a6-176">Modificare il valore di hello per `<Domain>` tooa un valore univoco che distingue `<ClaimsProvider>` da altri provider di identità.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="8a4a6-177">Aggiornare il valore di hello per `<DisplayName>` tooa nome visualizzato hello provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="8a4a6-178">Questo valore non viene usato attualmente.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="8a4a6-179">Aggiornare il profilo tecnico hello</span><span class="sxs-lookup"><span data-stu-id="8a4a6-179">Update hello technical profile</span></span>

<span data-ttu-id="8a4a6-180">tooget un token SAML da Salesforce, definire i protocolli di hello che Azure Active Directory B2C utilizzerà toocommunicate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8a4a6-181">Eseguire questa operazione in hello `<TechnicalProfile>` elemento `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="8a4a6-182">Aggiornare l'ID di hello di hello `<TechnicalProfile>` nodo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="8a4a6-183">Questo ID è utilizzato toorefer toothis profilo tecnica da altre parti del criterio hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="8a4a6-184">Aggiornare il valore di hello per `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="8a4a6-185">Questo valore viene visualizzato sul pulsante Accedi hello nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="8a4a6-186">Aggiornare il valore di hello per `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="8a4a6-187">Salesforce utilizza il protocollo di hello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="8a4a6-188">Verificare che tale valore hello per `<Protocol>` è **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="8a4a6-189">Hello aggiornamento `<Metadata>` sezione hello precedenti impostazioni di hello tooreflect XML per l'account di Salesforce specifico.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="8a4a6-190">Nel XML hello, aggiornare i valori dei metadati hello:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="8a4a6-191">Aggiornare il valore di hello di `<Item Key="PartnerEntity">` con l'URL dei metadati di Salesforce hello copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="8a4a6-192">Dispone di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="8a4a6-193">In hello `<CryptographicKeys>` sezione aggiornamento hello valore per entrambe le istanze di `StorageReferenceId` toohello nome della chiave di hello del certificato di firma (ad esempio, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="8a4a6-194">Caricare il file di estensione hello per verifica</span><span class="sxs-lookup"><span data-stu-id="8a4a6-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="8a4a6-195">Il criterio è ora configurato in modo che Azure Active Directory B2C sa come toocommunicate con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="8a4a6-196">Provare a caricare il file di estensione hello dei criteri, che non vi siano problemi finora tooverify.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="8a4a6-197">file di estensione hello tooupload dei criteri:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="8a4a6-198">Nel tenant di Azure Active Directory B2C, visitare toohello **tutti i criteri** blade.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="8a4a6-199">Seleziona hello **sovrascrivere i criteri di hello eventuale** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="8a4a6-200">Caricare il file di estensione hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="8a4a6-201">Verificare che la relativa convalida abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="8a4a6-202">Registrare hello viaggio di Salesforce SAML attestazioni provider tooa utente</span><span class="sxs-lookup"><span data-stu-id="8a4a6-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="8a4a6-203">Successivamente, aggiungere hello tooone di provider di identità SAML Salesforce di viaggi l'utente.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="8a4a6-204">A questo punto, il provider di identità hello è stato impostato, ma non è disponibile in uno qualsiasi di pagine di iscrizione o accesso utente hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="8a4a6-205">tooadd hello identity provider tooa pagina di accesso, creare innanzitutto un duplicato di un proprio processo utente di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="8a4a6-206">Quindi, modificare il modello di hello in modo che include anche i provider di identità hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="8a4a6-207">Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="8a4a6-208">Trovare hello `<UserJourneys>` elemento, quindi hello copia intera `<UserJourney>` valore, inclusi Id = "SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="8a4a6-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="8a4a6-209">Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="8a4a6-210">Trovare hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="8a4a6-211">Se l'elemento hello non esiste, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="8a4a6-212">Intero hello Incolla copiato `<UserJourney>` come figlio di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="8a4a6-213">Rinominare ID hello di hello nuova `<UserJourney>` (ad esempio, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="8a4a6-214">Pulsante di visualizzazione hello identity provider</span><span class="sxs-lookup"><span data-stu-id="8a4a6-214">Display hello identity provider button</span></span>

<span data-ttu-id="8a4a6-215">Hello `<ClaimsProviderSelection>` elemento è di pulsante di provider di identità tooan analoghi in una pagina di iscrizione o accesso.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="8a4a6-216">Aggiungendo un `<ClaimsProviderSelection>` viene visualizzato un pulsante nuovo elemento per Salesforce, quando un utente passa alla pagina toothis.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="8a4a6-217">pulsante del provider toodisplay hello identità:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="8a4a6-218">In hello `<UserJourney>` creato, trovare hello `<OrchestrationStep>` con `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="8a4a6-219">Aggiungere hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="8a4a6-220">Impostare `TargetClaimsExchangeId` valore logico tooa.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="8a4a6-221">È consigliabile seguente hello stessa convenzione di altri utenti (ad esempio,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="8a4a6-222">Azione del collegamento hello identity provider pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="8a4a6-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="8a4a6-223">Ora che si dispone di un pulsante di provider di identità, collegarlo tooan azione.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="8a4a6-224">In questo caso, l'azione di hello è per Azure Active Directory B2C toocommunicate con Salesforce tooreceive un token SAML.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="8a4a6-225">È possibile farlo mediante il collegamento profilo tecniche hello per le SAML Salesforce provider di attestazioni:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="8a4a6-226">In hello `<UserJourney>` nodo, hello trova `<OrchestrationStep>` con `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="8a4a6-227">Aggiungere hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="8a4a6-228">Aggiornamento `Id` toohello stesso valore che è stato utilizzato in precedenza per `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="8a4a6-229">Aggiornamento `TechnicalProfileReferenceId` toohello `Id` di hello tecnica profilo creato in precedenza (ad esempio, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="8a4a6-230">Caricare il file di estensione aggiornata hello</span><span class="sxs-lookup"><span data-stu-id="8a4a6-230">Upload hello updated extension file</span></span>

<span data-ttu-id="8a4a6-231">La modifica dei file di estensione hello termine.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="8a4a6-232">Salvare e caricare il file.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-232">Save and upload this file.</span></span> <span data-ttu-id="8a4a6-233">Verificare che tutte le convalide abbiano esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="8a4a6-234">Aggiornare il file di hello relying party</span><span class="sxs-lookup"><span data-stu-id="8a4a6-234">Update hello relying party file</span></span>

<span data-ttu-id="8a4a6-235">Successivamente, aggiornare hello relying party (RP) file che avvia viaggio utente hello creato:</span><span class="sxs-lookup"><span data-stu-id="8a4a6-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="8a4a6-236">Creare una copia di SignUpOrSignIn.xml nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="8a4a6-237">Rinominare quindi il file, ad esempio SignUpOrSignInWithAAD.xml.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="8a4a6-238">Hello di file e aggiornamento nuovo hello aprire `PolicyId` attributo per `<TrustFrameworkPolicy>` con un valore univoco.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="8a4a6-239">Questo è il nome di hello dei criteri (ad esempio, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="8a4a6-240">Modificare hello `ReferenceId` attributo `<DefaultUserJourney>` toomatch hello `Id` del viaggio utente nuovo hello creato (ad esempio, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="8a4a6-241">Salvare le modifiche e quindi caricare il file hello.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="8a4a6-242">Testare e risolvere i problemi</span><span class="sxs-lookup"><span data-stu-id="8a4a6-242">Test and troubleshoot</span></span>

<span data-ttu-id="8a4a6-243">andare a pannello criteri toohello, tootest hello criteri personalizzati appena caricato, nel portale di Azure, hello e quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="8a4a6-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="8a4a6-244">Se i test hanno esito negativo, vedere l'articolo sulla [risoluzione dei problemi relativi a criteri personalizzati](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a4a6-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a4a6-245">Next steps</span></span>

<span data-ttu-id="8a4a6-246">Fornire commenti e suggerimenti troppo[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8a4a6-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
