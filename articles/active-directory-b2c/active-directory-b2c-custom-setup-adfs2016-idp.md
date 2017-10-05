---
title: "Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati"
description: Articolo sulle procedure per configurare AD FS 2016 tramite il protocollo SAML e criteri personalizzati
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
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="8260c-103">Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="8260c-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="8260c-104">Questo articolo illustra come consentire agli utenti di accedere da un account AD FS tramite l'utilizzo di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8260c-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8260c-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8260c-105">Prerequisites</span></span>

<span data-ttu-id="8260c-106">Completare la procedura descritta nell'articolo [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8260c-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="8260c-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8260c-107">These steps include:</span></span>

1.  <span data-ttu-id="8260c-108">Creazione di un trust della relying party di AD FS.</span><span class="sxs-lookup"><span data-stu-id="8260c-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="8260c-109">Aggiunta del certificato di trust della relying party di AD FS in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8260c-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="8260c-110">Aggiunta di un provider di attestazioni nei criteri.</span><span class="sxs-lookup"><span data-stu-id="8260c-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="8260c-111">Registrazione del provider di attestazioni dell'account AD FS in un percorso utente.</span><span class="sxs-lookup"><span data-stu-id="8260c-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="8260c-112">Caricamento dei criteri in un tenant di Azure AD B2C e test dei criteri.</span><span class="sxs-lookup"><span data-stu-id="8260c-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="8260c-113">Per creare un trust della relying party in grado di riconoscere attestazioni</span><span class="sxs-lookup"><span data-stu-id="8260c-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="8260c-114">Per usare AD FS come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un trust della relying party di AD FS e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="8260c-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="8260c-115">Per aggiungere un nuovo trust della relying party usando lo snap-in di gestione di AD FS e configurare manualmente le impostazioni, eseguire la procedura seguente in un server federativo.</span><span class="sxs-lookup"><span data-stu-id="8260c-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="8260c-116">L'appartenenza al gruppo **Amministratori** o a un gruppo equivalente nel computer locale è il requisito minimo necessario per completare questa procedura.</span><span class="sxs-lookup"><span data-stu-id="8260c-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="8260c-117">Informazioni dettagliate sull'utilizzo delle appartenenze ai gruppi e degli account appropriati sono disponibili in [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477) (Gruppi predefiniti locali e di dominio).</span><span class="sxs-lookup"><span data-stu-id="8260c-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="8260c-118">In Server Manager selezionare **Strumenti** e quindi **Gestione AD FS**.</span><span class="sxs-lookup"><span data-stu-id="8260c-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="8260c-119">Fare clic su **Aggiungi attendibilità componente**.</span><span class="sxs-lookup"><span data-stu-id="8260c-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="8260c-120">![Aggiungi attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="8260c-121">Nella pagina **iniziale** scegliere **In grado di riconoscere attestazioni** e fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="8260c-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="8260c-122">![Nella pagina iniziale scegliere In grado di riconoscere attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="8260c-123">Nella pagina **Seleziona origine dati** fare clic su **Immetti dati sul componente manualmente** e quindi su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="8260c-124">![Immetti dati sul componente manualmente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="8260c-125">Nella pagina **Specifica nome visualizzato** digitare un nome in **Nome visualizzato**, in **Note** digitare una descrizione del trust della relying party e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="8260c-126">![Specificare il nome visualizzato e le note](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="8260c-127">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="8260c-127">Optional.</span></span> <span data-ttu-id="8260c-128">Se si ha un certificato di crittografia di token facoltativo, nella pagina **Configura certificato** fare clic su **Sfoglia** per trovare il file del certificato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="8260c-129">![Configura certificato](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="8260c-130">Nella pagina **Configura URL** selezionare la casella di controllo **Abilita supporto del protocollo SAML 2.0 WebSSO**.</span><span class="sxs-lookup"><span data-stu-id="8260c-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="8260c-131">In **Componente URL del servizio SAML 2.0 SSO** digitare l'URL dell'endpoint di servizio SALM (Security Assertion Markup Language) per questo trust della relying party e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="8260c-132">In **Componente URL del servizio SAML 2.0 SSO** incollare `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="8260c-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="8260c-133">Sostituire {tenant} con il nome del tenant (ad esempio, contosob2c.onmicrosoft.com) e sostituire i {criteri} con il nome dei criteri di estensione (ad esempio, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="8260c-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="8260c-134">Il nome dei criteri è quello da cui ereditano i criteri signup_or_signin, in questo caso: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="8260c-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="8260c-135">L'URL, ad esempio, può essere: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="8260c-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Componente URL del servizio SAML 2.0 SSO](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="8260c-137">Nella pagina **Configura identificatori** specificare lo stesso URL del passaggio precedente, fare clic su **Aggiungi** per aggiungerlo all'elenco e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="8260c-138">![Identificatori dell'attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="8260c-139">Nella pagina **Scegli criteri di controllo di accesso** scegliere i criteri desiderati e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8260c-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="8260c-140">![Scegli criteri di controllo di accesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="8260c-141">Nella pagina **Aggiunta attendibilità** rivedere le impostazioni e quindi fare clic su **Avanti** per salvare le informazioni sul trust della relying party.</span><span class="sxs-lookup"><span data-stu-id="8260c-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="8260c-142">![Salvare le informazioni sul trust della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="8260c-143">Nella pagina **Fine** fare clic su **Chiudi**. Viene automaticamente visualizzata la finestra di dialogo **Modifica regole attestazione**.</span><span class="sxs-lookup"><span data-stu-id="8260c-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="8260c-144">Selezionare ![Modifica regole attestazione](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="8260c-145">Fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="8260c-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="8260c-146">![Aggiungi nuova regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="8260c-147">In **Modello di regola attestazione** selezionare **Inviare attributi LDAP come attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="8260c-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="8260c-148">![Selezionare la regola modello Inviare attributi LDAP come attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="8260c-149">Specificare **Nome regola attestazione**.</span><span class="sxs-lookup"><span data-stu-id="8260c-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="8260c-150">Per **Archivio attributi** selezionare **Select Active Directory** (Seleziona Active Directory), aggiungere le attestazioni seguenti e quindi fare clic su **Fine** e su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8260c-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="8260c-151">![Impostare le proprietà di regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="8260c-152">In Server Manager selezionare **Attendibilità componente**, selezionare il trust della relying party creato e quindi fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="8260c-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="8260c-153">![Proprietà di modifica della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="8260c-154">Nella finestra delle proprietà del trust della relying party (B2C Demo) fare clic sulla scheda **Firma** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8260c-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="8260c-155">![Imposta firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="8260c-156">Aggiungere il certificato di firma (file con estensione CERT, senza chiave privata).</span><span class="sxs-lookup"><span data-stu-id="8260c-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Aggiungere il certificato di firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="8260c-158">Nella finestra delle proprietà del trust della relying party (B2C Demo) fare clic sulla scheda **Avanzate** e impostare **Algoritmo hash sicuro** su **SHA-1**. Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8260c-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="8260c-159">![Impostare l'algoritmo hash sicuro su SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="8260c-160">Aggiungere la chiave dell'applicazione di account AD FS in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8260c-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="8260c-161">La federazione con account AD FS richiede un segreto client per consentire all'account AD FS di considerare attendibile Azure AD B2C per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8260c-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="8260c-162">È necessario quindi archiviare il certificato AD FS nel tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8260c-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="8260c-163">Passare al tenant di Azure AD B2C e selezionare **B2C Settings** (Impostazioni B2C) > **Framework dell'esperienza di gestione delle identità**</span><span class="sxs-lookup"><span data-stu-id="8260c-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="8260c-164">Selezionare **Chiavi dei criteri** per visualizzare le chiavi disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="8260c-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="8260c-165">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8260c-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="8260c-166">Per **Opzioni** usare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="8260c-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="8260c-167">Per **Nome** usare `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="8260c-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="8260c-168">È possibile che il prefisso `B2C_1A_` venga aggiunto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8260c-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="8260c-169">In Caricamento file selezionare il file del certificato con estensione PFX, con la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="8260c-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="8260c-170">Nota: questo certificato (con la chiave privata) deve essere lo stesso rilasciato e usato per la relying party di AD FS.</span><span class="sxs-lookup"><span data-stu-id="8260c-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="8260c-171">![Carica chiave criteri](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="8260c-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="8260c-172">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="8260c-172">Click **Create**</span></span>
8.  <span data-ttu-id="8260c-173">Confermare di avere creato la chiave `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="8260c-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="8260c-174">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="8260c-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="8260c-175">Per consentire agli utenti di accedere con un account AD FS, è necessario definire l'account AD FS come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="8260c-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="8260c-176">In altre parole, è necessario specificare un endpoint con cui comunichi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8260c-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="8260c-177">L'endpoint offre un set di attestazioni che vengono usate da Azure AD B2C per verificare se un utente specifico è stato autenticato.</span><span class="sxs-lookup"><span data-stu-id="8260c-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="8260c-178">Definire AD FS come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="8260c-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="8260c-179">Aprire il file dei criteri di estensione (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8260c-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="8260c-180">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="8260c-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="8260c-181">Trovare la sezione `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="8260c-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="8260c-182">Aggiungere il seguente frammento XML nell'elemento `ClaimsProviders` e sostituire `identityProvider` con il DNS (valore arbitrario che indica il dominio personale) e quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="8260c-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="8260c-183">Registrare il provider di attestazioni dell'account AD FS in un percorso utente di registrazione o di accesso</span><span class="sxs-lookup"><span data-stu-id="8260c-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="8260c-184">A questo punto, il provider di identità è stato configurato,</span><span class="sxs-lookup"><span data-stu-id="8260c-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="8260c-185">ma non è disponibile in nessuna delle schermate di registrazione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="8260c-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="8260c-186">È necessario ora aggiungere il provider di identità dell'account AD FS al percorso utente `SignUpOrSignIn` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8260c-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="8260c-187">Per renderlo disponibile, si crea un duplicato di un modello di processo utente esistente</span><span class="sxs-lookup"><span data-stu-id="8260c-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="8260c-188">e lo si modifica in modo che contenga il provider di identità AD FS:</span><span class="sxs-lookup"><span data-stu-id="8260c-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="8260c-189">Aprire il file di base dei criteri, ad esempio TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="8260c-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="8260c-190">Trovare l'elemento `<UserJourneys>` e copiare l'intero contenuto del nodo `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="8260c-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="8260c-191">Aprire il file di estensione, ad esempio TrustFrameworkExtensions.xml, e trovare l'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="8260c-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="8260c-192">Se l'elemento non esiste, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="8260c-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="8260c-193">Incollare l'intero contenuto del nodo `<UserJournesy>` copiato come figlio dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="8260c-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="8260c-194">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="8260c-194">Display the button</span></span>
<span data-ttu-id="8260c-195">L'elemento `<ClaimsProviderSelections>` definisce l'elenco delle opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="8260c-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="8260c-196">L'elemento `<ClaimsProviderSelection>` è analogo a un pulsante del provider di identità in una pagina di registrazione/accesso.</span><span class="sxs-lookup"><span data-stu-id="8260c-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="8260c-197">Se si aggiunge un elemento `<ClaimsProviderSelection>` per l'account AD FS, viene visualizzato un nuovo pulsante quando un utente apre la pagina.</span><span class="sxs-lookup"><span data-stu-id="8260c-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="8260c-198">Per aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="8260c-198">To add this element:</span></span>

1.  <span data-ttu-id="8260c-199">Trovare il nodo `<UserJourney>` che include `Id="SignUpOrSignIn"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="8260c-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="8260c-200">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="8260c-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="8260c-201">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="8260c-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="8260c-202">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="8260c-202">Link the button to an action</span></span>

<span data-ttu-id="8260c-203">Ora che il pulsante è stato posizionato, è necessario collegarlo a un'azione.</span><span class="sxs-lookup"><span data-stu-id="8260c-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="8260c-204">L'azione, in questo caso, consiste nel far comunicare Azure AD B2C con l'account AD FS per ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="8260c-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="8260c-205">È possibile farlo collegando il profilo tecnico per il provider di attestazioni dell'account AD FS:</span><span class="sxs-lookup"><span data-stu-id="8260c-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="8260c-206">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="8260c-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="8260c-207">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="8260c-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="8260c-208">Verificare che `Id` sia impostato sullo stesso valore di `TargetClaimsExchangeId` riportato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="8260c-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="8260c-209">Verificare che `TechnicalProfileReferenceId` sia impostato sul profilo tecnico creato in precedenza (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="8260c-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="8260c-210">Caricare i criteri nel tenant</span><span class="sxs-lookup"><span data-stu-id="8260c-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="8260c-211">Nel [portale di Azure](https://portal.azure.com) passare al [contesto del tenant di Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e aprire il pannello **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="8260c-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="8260c-212">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="8260c-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="8260c-213">Aprire il pannello **Tutti i criteri**.</span><span class="sxs-lookup"><span data-stu-id="8260c-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="8260c-214">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="8260c-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="8260c-215">Selezionare la casella **Sovrascrivi il criterio se esistente**.</span><span class="sxs-lookup"><span data-stu-id="8260c-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="8260c-216">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non presenti errori di convalida</span><span class="sxs-lookup"><span data-stu-id="8260c-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="8260c-217">Testare i criteri personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="8260c-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="8260c-218">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="8260c-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="8260c-219">Aprire **B2C_1A_signup_signin**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8260c-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="8260c-220">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="8260c-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="8260c-221">Dovrebbe essere possibile accedere usando un account AD FS.</span><span class="sxs-lookup"><span data-stu-id="8260c-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="8260c-222">[Facoltativo] Registrare il provider di attestazioni dell'account AD FS nel percorso utente Profile-Edit</span><span class="sxs-lookup"><span data-stu-id="8260c-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="8260c-223">È possibile aggiungere il provider di identità dell'account AD FS anche al percorso utente `ProfileEdit` dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8260c-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="8260c-224">Per renderlo disponibile, ripetere gli ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="8260c-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="8260c-225">Visualizzare il pulsante</span><span class="sxs-lookup"><span data-stu-id="8260c-225">Display the button</span></span>
1.  <span data-ttu-id="8260c-226">Aprire il file di estensione dei criteri, ad esempio TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="8260c-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="8260c-227">Trovare il nodo `<UserJourney>` che include `Id="ProfileEdit"` nel percorso utente appena copiato.</span><span class="sxs-lookup"><span data-stu-id="8260c-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="8260c-228">Passare al nodo `<OrchestrationStep>` che include `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="8260c-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="8260c-229">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="8260c-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="8260c-230">Collegare il pulsante a un'azione</span><span class="sxs-lookup"><span data-stu-id="8260c-230">Link the button to an action</span></span>
1.  <span data-ttu-id="8260c-231">Trovare l'oggetto `<OrchestrationStep>` che include `Order="2"` nel nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="8260c-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="8260c-232">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="8260c-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="8260c-233">Testare i criteri Profile-Edit personalizzati tramite Esegui adesso</span><span class="sxs-lookup"><span data-stu-id="8260c-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="8260c-234">Aprire **Impostazioni di Azure AD B2C** e passare a **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="8260c-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="8260c-235">Aprire **B2C_1A_ProfileEdit**, i criteri personalizzati dalla relying party caricati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8260c-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="8260c-236">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="8260c-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="8260c-237">Dovrebbe essere possibile accedere usando un account AD FS.</span><span class="sxs-lookup"><span data-stu-id="8260c-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="8260c-238">Scaricare i file dei criteri completi</span><span class="sxs-lookup"><span data-stu-id="8260c-238">Download the complete policy files</span></span>
<span data-ttu-id="8260c-239">Facoltativo: per creare lo scenario è consigliabile usare file di criteri personalizzati dopo aver completato la procedura Introduzione ai criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8260c-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="8260c-240">File dei criteri di esempio solo per riferimento</span><span class="sxs-lookup"><span data-stu-id="8260c-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
