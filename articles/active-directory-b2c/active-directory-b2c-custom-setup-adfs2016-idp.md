---
title: "Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati"
description: Un tooarticle procedura su come configurare ADFS 2016 utilizzando il protocollo SAML e i criteri personalizzati
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="5f278-103">Azure Active Directory B2C: Aggiungere AD FS come provider di identità SAML tramite criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="5f278-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5f278-104">Questo articolo illustra come tooenable Accedi per gli utenti dall'account ADFS tramite l'utilizzo di hello di [criteri personalizzati](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5f278-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f278-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f278-105">Prerequisites</span></span>

<span data-ttu-id="5f278-106">Hello completato i passaggi in hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="5f278-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="5f278-107">La procedura include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5f278-107">These steps include:</span></span>

1.  <span data-ttu-id="5f278-108">Creazione di un trust della relying party di AD FS.</span><span class="sxs-lookup"><span data-stu-id="5f278-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="5f278-109">Aggiunta di hello ADFS Trust della Relying Party certificato tooAzure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5f278-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="5f278-110">Aggiunta di criteri tooa di provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="5f278-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="5f278-111">Account di ad FS hello registrazione viaggio utente tooa di provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="5f278-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="5f278-112">Caricamento tooan criteri hello Azure Active Directory B2C tenant ed eseguirne il test.</span><span class="sxs-lookup"><span data-stu-id="5f278-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="5f278-113">toocreate un Trust della Relying Party grado di riconoscere attestazioni</span><span class="sxs-lookup"><span data-stu-id="5f278-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="5f278-114">toouse ADFS come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un ADFS Trust della Relying Party e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="5f278-115">tooadd nuovo relying party trust tramite lo snap-in Gestione ADFS hello Active Directory e configurare manualmente le impostazioni di hello, eseguire hello seguente procedura in un server federativo.</span><span class="sxs-lookup"><span data-stu-id="5f278-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="5f278-116">L'appartenenza a **amministratori**, o equivalente nel computer locale hello toocomplete necessari minimo hello questa procedura.</span><span class="sxs-lookup"><span data-stu-id="5f278-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="5f278-117">Altre informazioni sull'uso degli account appropriati hello e appartenenze a [dominio gruppi predefiniti locali e](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="5f278-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="5f278-118">In Server Manager selezionare **Strumenti** e quindi **Gestione AD FS**.</span><span class="sxs-lookup"><span data-stu-id="5f278-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="5f278-119">Fare clic su **Aggiungi attendibilità componente**.</span><span class="sxs-lookup"><span data-stu-id="5f278-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="5f278-120">![Aggiungi attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="5f278-121">In hello **iniziale** pagina, scegliere **grado di riconoscere attestazioni** e fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="5f278-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="5f278-122">![Nella pagina di benvenuto hello, scegliere il grado di riconoscere attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="5f278-123">In hello **Seleziona origine dati** pagina, fare clic su **immettere manualmente i dati sulla relying party di hello**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f278-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="5f278-124">![Immettere i dati sulla relying party di hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="5f278-125">In hello **Specifica nome visualizzato** , digitare un nome in **nome visualizzato**in **note** digitare una descrizione per questo trust della relying party e quindi fare clic su **successivo** .</span><span class="sxs-lookup"><span data-stu-id="5f278-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="5f278-126">![Specificare il nome visualizzato e le note](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="5f278-127">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="5f278-127">Optional.</span></span> <span data-ttu-id="5f278-128">Se sono presenti un certificato di crittografia token facoltativa, quindi hello **Configura certificato** pagina, fare clic su **Sfoglia** toolocate il file di certificato e quindi fare clic su **Avanti** .</span><span class="sxs-lookup"><span data-stu-id="5f278-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="5f278-129">![Configura certificato](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="5f278-130">In hello **Configura URL** pagina, seleziona hello **abilitare il supporto per il protocollo SAML 2.0 WebSSO hello** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="5f278-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="5f278-131">In **Relying party SAML 2.0 SSO service URL**, digitare l'URL dell'endpoint del servizio hello Security Assertion Markup Language (SAML) per questo trust della relying party e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f278-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="5f278-132">Per hello **Relying party SAML 2.0 SSO service URL**, incollare hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="5f278-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="5f278-133">Sostituire {tenant} con il nome del tenant (ad esempio, contosob2c.onmicrosoft.com) e sostituire hello {criteri} con il nome del criterio estensioni (ad esempio, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="5f278-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="5f278-134">nome del criterio Hello è hello uno da cui eredita criteri signup_or_signin, in questo caso è: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="5f278-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="5f278-135">Ad esempio in cui potrebbe essere URL hello: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="5f278-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Componente URL del servizio SAML 2.0 SSO](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="5f278-137">In hello **Configura identificatori** specificare hello stesso URL come passaggio precedente hello, fare clic su **Aggiungi** tooadd li toohello elenco e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f278-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="5f278-138">![Identificatori dell'attendibilità componente](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="5f278-139">In hello **scegliere Criteri di controllo di accesso** selezionare un criterio e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f278-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="5f278-140">![Scegli criteri di controllo di accesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="5f278-141">In hello **pronto tooAdd Trust** pagina, rivedere le impostazioni di hello e quindi fare clic su **Avanti** toosave la relying party trust informazioni.</span><span class="sxs-lookup"><span data-stu-id="5f278-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="5f278-142">![Salvare le informazioni sul trust della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="5f278-143">In hello **fine** pagina, fare clic su **Chiudi**, questa azione consente di visualizzare automaticamente hello **Modifica regole attestazione** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5f278-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="5f278-144">Selezionare ![Modifica regole attestazione](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="5f278-145">Fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="5f278-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="5f278-146">![Aggiungi nuova regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="5f278-147">In **Modello di regola attestazione** selezionare **Inviare attributi LDAP come attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="5f278-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="5f278-148">![Selezionare la regola modello Inviare attributi LDAP come attestazioni](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="5f278-149">Specificare **Nome regola attestazione**.</span><span class="sxs-lookup"><span data-stu-id="5f278-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="5f278-150">Per hello **archivio attributi** selezionare **selezionare Active Directory** aggiungere hello seguendo le attestazioni, quindi fare clic su **fine** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f278-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="5f278-151">![Impostare le proprietà di regola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="5f278-152">In Server Manager, selezionare **Relying Party Trusts** selezionare hello trust della relying party è stato creato, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5f278-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="5f278-153">![Proprietà di modifica della relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="5f278-154">Uno hello relying party trust (B2C Demo) finestra Proprietà selezionare **firma** scheda e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5f278-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="5f278-155">![Imposta firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="5f278-156">Aggiungere il certificato di firma (file con estensione CERT, senza chiave privata).</span><span class="sxs-lookup"><span data-stu-id="5f278-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Aggiungere il certificato di firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="5f278-158">Nella finestra dei comandi di hello relying party trust (B2C Demo) fare clic su **avanzate** scheda e modificare hello **algoritmo hash protetto** troppo**SHA-1**, fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="5f278-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="5f278-159">![Impostare l'algoritmo di hash protetto tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="5f278-160">Aggiungere hello ADFS account applicazione chiave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5f278-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="5f278-161">Federazione con l'account ADFS richiede un segreto client per ad FS tootrust di account Azure Active Directory B2C per conto di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="5f278-162">È necessario un certificato ADFS toostore nel tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5f278-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="5f278-163">Tenant di Azure Active Directory B2C tooyour scegliere **impostazioni B2C** > **Framework esperienza di identità**</span><span class="sxs-lookup"><span data-stu-id="5f278-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="5f278-164">Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.</span><span class="sxs-lookup"><span data-stu-id="5f278-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="5f278-165">Fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5f278-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="5f278-166">Per **Opzioni** usare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="5f278-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="5f278-167">Per **Nome** usare `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5f278-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="5f278-168">prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f278-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="5f278-169">Nel caricamento del File hello, * * selezionare il file pfx del certificato con chiave privata.</span><span class="sxs-lookup"><span data-stu-id="5f278-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="5f278-170">Nota: questo certificato (con la chiave privata hello) deve essere identico a quello che emesso e utilizzato per relying party ADFS hello hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="5f278-171">![Carica chiave criteri](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="5f278-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="5f278-172">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="5f278-172">Click **Create**</span></span>
8.  <span data-ttu-id="5f278-173">Verificare di aver creato la chiave hello `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5f278-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="5f278-174">Aggiungere un provider di attestazioni nei criteri di estensione</span><span class="sxs-lookup"><span data-stu-id="5f278-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="5f278-175">Se si desidera toosign gli utenti utilizzando l'account ADFS, è necessario account ADFS toodefine come provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="5f278-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="5f278-176">In altre parole, è necessario toospecify un endpoint di Azure Active Directory B2C con cui comunica.</span><span class="sxs-lookup"><span data-stu-id="5f278-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="5f278-177">endpoint Hello fornisce un set di attestazioni che vengono utilizzati da Azure AD B2C tooverify che ha autenticato un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="5f278-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="5f278-178">Definire AD FS come provider di attestazioni aggiungendo il nodo `<ClaimsProvider>` nel file dei criteri di estensione:</span><span class="sxs-lookup"><span data-stu-id="5f278-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="5f278-179">Aprire i file dei criteri estensione hello (TrustFrameworkExtensions.xml) dalla directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5f278-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="5f278-180">Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.</span><span class="sxs-lookup"><span data-stu-id="5f278-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="5f278-181">Trovare hello `<ClaimsProviders>` sezione</span><span class="sxs-lookup"><span data-stu-id="5f278-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="5f278-182">Aggiungere hello seguente frammento di codice XML in hello `ClaimsProviders` elemento e sostituire `identityProvider` con il server DNS (valore arbitrario che indica il dominio), quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="5f278-183">Registrare hello ADFS account attestazioni provider tooSign backup o accedere al proprio processo utente</span><span class="sxs-lookup"><span data-stu-id="5f278-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="5f278-184">A questo punto, il provider di identità hello è stato impostato.</span><span class="sxs-lookup"><span data-stu-id="5f278-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="5f278-185">Non è tuttavia disponibile in una qualsiasi delle schermate di sign-configurazione/Accedi hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="5f278-186">È possibile procedere tooadd hello ADFS account identity provider tooyour utente `SignUpOrSignIn` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="5f278-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="5f278-187">toomake disponibili, si crea un duplicato di un proprio processo utente di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="5f278-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="5f278-188">Quindi, abbiamo modificarlo in modo da includere il provider di identità ADFS hello:</span><span class="sxs-lookup"><span data-stu-id="5f278-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="5f278-189">Aprire il file di base hello dei criteri (ad esempio, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="5f278-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="5f278-190">Trovare hello `<UserJourneys>` elemento e copia hello intero contenuto di `<UserJourneys>` nodo.</span><span class="sxs-lookup"><span data-stu-id="5f278-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="5f278-191">Aprire il file di estensione hello (ad esempio, TrustFrameworkExtensions.xml) e individuare hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="5f278-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="5f278-192">Se non esiste l'elemento hello, aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="5f278-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="5f278-193">Incollare l'intero contenuto di hello di `<UserJournesy>` nodo copiato come figlio di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="5f278-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="5f278-194">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="5f278-194">Display hello button</span></span>
<span data-ttu-id="5f278-195">Hello `<ClaimsProviderSelections>` elemento definisce l'elenco di hello di opzioni di selezione del provider di attestazioni e il relativo ordine.</span><span class="sxs-lookup"><span data-stu-id="5f278-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="5f278-196">`<ClaimsProviderSelection>`elemento è di tipo pulsante di provider di identità di tooan analoghi in una pagina sign-configurazione/Accedi.</span><span class="sxs-lookup"><span data-stu-id="5f278-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="5f278-197">Se si aggiunge un `<ClaimsProviderSelection>` elemento per conto ADFS, un nuovo pulsante viene visualizzato quando un utente inserita nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="5f278-198">tooadd questo elemento:</span><span class="sxs-lookup"><span data-stu-id="5f278-198">tooadd this element:</span></span>

1.  <span data-ttu-id="5f278-199">Trovare hello `<UserJourney>` nodo che include `Id="SignUpOrSignIn"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="5f278-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="5f278-200">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5f278-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="5f278-201">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="5f278-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="5f278-202">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="5f278-202">Link hello button tooan action</span></span>

<span data-ttu-id="5f278-203">Ora che si dispone di un pulsante, è necessario toolink è tooan azione.</span><span class="sxs-lookup"><span data-stu-id="5f278-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="5f278-204">azione di Hello, in questo caso, è per Azure Active Directory B2C toocommunicate con ADFS account tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="5f278-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="5f278-205">Collegamento azione pulsante di hello tooan collegando profilo tecniche hello per il provider di attestazioni ADFS account:</span><span class="sxs-lookup"><span data-stu-id="5f278-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="5f278-206">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="5f278-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5f278-207">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="5f278-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="5f278-208">Assicurarsi di hello `Id` ha lo stesso valore di hello `TargetClaimsExchangeId` nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="5f278-209">Verificare `TechnicalProfileReferenceId` è impostare il profilo di tecniche toohello precedenti (Contoso-SAML2) è stato creato.</span><span class="sxs-lookup"><span data-stu-id="5f278-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="5f278-210">Caricare tenant tooyour di hello criteri</span><span class="sxs-lookup"><span data-stu-id="5f278-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="5f278-211">In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="5f278-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="5f278-212">Fare clic su **Framework dell'esperienza di gestione delle identità**.</span><span class="sxs-lookup"><span data-stu-id="5f278-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="5f278-213">Aprire hello **tutti i criteri** blade.</span><span class="sxs-lookup"><span data-stu-id="5f278-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="5f278-214">Selezionare **Carica criteri**.</span><span class="sxs-lookup"><span data-stu-id="5f278-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="5f278-215">Controllare **sovrascrivere i criteri di hello eventuale** casella.</span><span class="sxs-lookup"><span data-stu-id="5f278-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="5f278-216">**Caricare** TrustFrameworkExtensions.xml e assicurarsi che non riuscire convalida hello</span><span class="sxs-lookup"><span data-stu-id="5f278-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="5f278-217">Test dei criteri personalizzati di hello tramite Esegui</span><span class="sxs-lookup"><span data-stu-id="5f278-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="5f278-218">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="5f278-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5f278-219">Aprire **B2C_1A_signup_signin**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="5f278-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5f278-220">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="5f278-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="5f278-221">È necessario essere in grado di toosign con account ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f278-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="5f278-222">[Facoltativo] Registrare viaggio di hello ADFS account attestazioni provider tooProfile modifica utente</span><span class="sxs-lookup"><span data-stu-id="5f278-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="5f278-223">È consigliabile provider di identità account ADFS hello tooadd anche tooyour utente `ProfileEdit` viaggio utente.</span><span class="sxs-lookup"><span data-stu-id="5f278-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="5f278-224">toomake è disponibile, si ripete hello ultimi due passaggi:</span><span class="sxs-lookup"><span data-stu-id="5f278-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="5f278-225">Pulsante di visualizzazione hello</span><span class="sxs-lookup"><span data-stu-id="5f278-225">Display hello button</span></span>
1.  <span data-ttu-id="5f278-226">Aprire il file di estensione hello dei criteri (ad esempio, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="5f278-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="5f278-227">Trovare hello `<UserJourney>` nodo che include `Id="ProfileEdit"` in viaggio utente hello copiato.</span><span class="sxs-lookup"><span data-stu-id="5f278-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="5f278-228">Individuare hello `<OrchestrationStep>` nodo che include`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5f278-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="5f278-229">Aggiungere il frammento XML seguente nel nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="5f278-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="5f278-230">Azione di collegamento hello pulsante tooan</span><span class="sxs-lookup"><span data-stu-id="5f278-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="5f278-231">Trovare hello `<OrchestrationStep>` che include `Order="2"` in hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="5f278-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5f278-232">Aggiungere il frammento XML seguente nel nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="5f278-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="5f278-233">Testare il criterio Modifica profilo personalizzato di hello utilizzando Esegui</span><span class="sxs-lookup"><span data-stu-id="5f278-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="5f278-234">Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.</span><span class="sxs-lookup"><span data-stu-id="5f278-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5f278-235">Aprire **B2C_1A_ProfileEdit**, hello criteri personalizzati di relying party (RP) che è stata caricata.</span><span class="sxs-lookup"><span data-stu-id="5f278-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5f278-236">Selezionare **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="5f278-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="5f278-237">È necessario essere in grado di toosign con account ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f278-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="5f278-238">Scaricare i file di criteri completa hello</span><span class="sxs-lookup"><span data-stu-id="5f278-238">Download hello complete policy files</span></span>
<span data-ttu-id="5f278-239">Facoltativo: È consigliabile che compilare lo scenario utilizzando i file di criteri personalizzata dopo aver completato l'introduzione a criteri personalizzati analizzerà hello.</span><span class="sxs-lookup"><span data-stu-id="5f278-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="5f278-240">File dei criteri di esempio solo per riferimento</span><span class="sxs-lookup"><span data-stu-id="5f278-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
