---
title: 'Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e trasferimento MOVEit - integrazione di Azure AD.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="0086d-103">Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="0086d-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="0086d-104">In questa esercitazione, è illustrato come toointegrate MOVEit trasferimento - integrazione di Azure AD con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0086d-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0086d-105">L'integrazione di trasferimento MOVEit - integrazione di Azure AD con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0086d-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0086d-106">È possibile controllare in Azure AD che ha accesso tooMOVEit trasferimento - integrazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="0086d-107">È possibile abilitare l'utenti tooautomatically get connesso tooMOVEit trasferimento - integrazione di Azure AD (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0086d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0086d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0086d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0086d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0086d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0086d-110">Prerequisites</span></span>

<span data-ttu-id="0086d-111">tooconfigure integrazione di Azure AD con trasferimento MOVEit - integrazione di Azure AD, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0086d-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="0086d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0086d-113">Sottoscrizione di MOVEit Transfer - Azure AD integration abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0086d-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0086d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0086d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0086d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0086d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0086d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0086d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0086d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0086d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0086d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0086d-118">Scenario description</span></span>
<span data-ttu-id="0086d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0086d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0086d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0086d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0086d-121">Aggiunta di trasferimento MOVEit - integrazione di Azure AD dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0086d-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="0086d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0086d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="0086d-123">Aggiunta di trasferimento MOVEit - integrazione di Azure AD dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0086d-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="0086d-124">integrazione di hello tooconfigure di trasferimento MOVEit - integrazione di Azure AD in Azure AD, è necessario tooadd MOVEit trasferimento - integrazione di Azure AD dall'elenco di tooyour hello della raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0086d-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0086d-125">**tooadd MOVEit trasferimento - integrazione di Azure AD dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0086d-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0086d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0086d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="0086d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0086d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0086d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0086d-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="0086d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0086d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="0086d-133">Nella casella di ricerca hello, digitare **MOVEit trasferimento - integrazione di Azure AD**selezionare **MOVEit trasferimento - integrazione di Azure AD** dal pannello risultati quindi fare clic su **Aggiungi** hello tooadd pulsante applicazione.</span><span class="sxs-lookup"><span data-stu-id="0086d-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Trasferimento MOVEit - integrazione di Azure AD nell'elenco risultati hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0086d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0086d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0086d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con MOVEit Transfer - Azure AD integration usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0086d-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0086d-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello trasferimento MOVEit - integrazione di Azure AD è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="0086d-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in trasferimento MOVEit - integrazione di Azure AD deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0086d-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="0086d-139">Trasferimento MOVEit - integrazione di Azure AD, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0086d-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0086d-140">tooconfigure e prova AD Azure single sign-on con trasferimento MOVEit - integrazione di Azure AD, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0086d-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0086d-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0086d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0086d-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0086d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0086d-143">**[Creare un trasferimento MOVEit - utente test di integrazione di Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave un equivalente di Britta Simon MOVEit trasferimento - integrazione di Azure AD che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0086d-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0086d-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0086d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0086d-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0086d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0086d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0086d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0086d-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel trasferimento di MOVEit - applicazione di integrazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="0086d-148">**Azure AD tooconfigure single sign-on con trasferimento MOVEit - integrazione di Azure AD, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0086d-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="0086d-149">Nel portale di Azure su hello hello **MOVEit trasferimento - integrazione di Azure AD** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0086d-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="0086d-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0086d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="0086d-153">In hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0086d-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="0086d-155">a.</span><span class="sxs-lookup"><span data-stu-id="0086d-155">a.</span></span> <span data-ttu-id="0086d-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="0086d-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="0086d-157">b.</span><span class="sxs-lookup"><span data-stu-id="0086d-157">b.</span></span> <span data-ttu-id="0086d-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="0086d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="0086d-159">c.</span><span class="sxs-lookup"><span data-stu-id="0086d-159">c.</span></span> <span data-ttu-id="0086d-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="0086d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="0086d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0086d-161">These values are not real.</span></span> <span data-ttu-id="0086d-162">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0086d-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0086d-163">È possibile fare riferimento a questi valori in un secondo momento in **URL dei metadati del servizio Provider** sezione o un contatto [MOVEit trasferimento - team di supporto Client di integrazione di Azure AD](https://community.ipswitch.com/s/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="0086d-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="0086d-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0086d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="0086d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0086d-166">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0086d-168">Accesso tooyour MOVEit trasferimento tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0086d-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="0086d-169">Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0086d-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Sezione delle impostazioni sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="0086d-171">Fare clic sul collegamento **Single Signon** (Single Sign-On) in **Security Policies -> User Auth** (Criteri di sicurezza -> Autenticazione utente).</span><span class="sxs-lookup"><span data-stu-id="0086d-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Criteri di sicurezza sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="0086d-173">Fare clic su documento di metadati hello collegamento toodownload hello URL dei metadati.</span><span class="sxs-lookup"><span data-stu-id="0086d-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![URL dei metadati del provider di servizi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="0086d-175">Verificare **entityID** corrisponde **identificatore** in hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="0086d-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="0086d-176">Verificare **AssertionConsumerService** percorso URL corrisponde a **URL di risposta** in hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="0086d-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="0086d-178">Fare clic su **Add Identity Provider** pulsante tooadd un nuovo Provider di identità federata.</span><span class="sxs-lookup"><span data-stu-id="0086d-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Aggiungi provider di identità](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="0086d-180">Fare clic su **Sfoglia...**  tooselect hello file di metadati che è stato scaricato dal portale di Azure, quindi fare clic su **Add Identity Provider** hello tooupload download del file.</span><span class="sxs-lookup"><span data-stu-id="0086d-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Provider di identità SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="0086d-182">Selezionare "**Sì**" come **abilitato** in hello **Modifica impostazioni di Provider di identità federata...**  pagina e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="0086d-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Impostazioni provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="0086d-184">In hello **modifica Federated Identity Provider di impostazioni utente** eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="0086d-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Modifica delle impostazioni del provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="0086d-186">a.</span><span class="sxs-lookup"><span data-stu-id="0086d-186">a.</span></span> <span data-ttu-id="0086d-187">Selezionare **SAML NameID** (ID nome SAML) per **Login name** (Nome di accesso).</span><span class="sxs-lookup"><span data-stu-id="0086d-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="0086d-188">b.</span><span class="sxs-lookup"><span data-stu-id="0086d-188">b.</span></span> <span data-ttu-id="0086d-189">Selezionare **altri** come **nome completo** e hello **nome dell'attributo** casella di testo inserire il valore di hello: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="0086d-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="0086d-190">c.</span><span class="sxs-lookup"><span data-stu-id="0086d-190">c.</span></span> <span data-ttu-id="0086d-191">Selezionare **altri** come **posta elettronica** e hello **nome dell'attributo** casella di testo inserire il valore di hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0086d-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="0086d-192">d.</span><span class="sxs-lookup"><span data-stu-id="0086d-192">d.</span></span> <span data-ttu-id="0086d-193">Selezionare **Yes** (Sì) per **Auto-create account on signon** (Crea automaticamente account all'accesso).</span><span class="sxs-lookup"><span data-stu-id="0086d-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="0086d-194">e.</span><span class="sxs-lookup"><span data-stu-id="0086d-194">e.</span></span> <span data-ttu-id="0086d-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0086d-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="0086d-196">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0086d-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0086d-197">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0086d-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0086d-198">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0086d-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0086d-199">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0086d-199">Create an Azure AD test user</span></span>

<span data-ttu-id="0086d-200">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0086d-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="0086d-202">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0086d-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0086d-203">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0086d-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0086d-205">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0086d-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0086d-207">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0086d-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0086d-209">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0086d-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0086d-211">a.</span><span class="sxs-lookup"><span data-stu-id="0086d-211">a.</span></span> <span data-ttu-id="0086d-212">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0086d-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0086d-213">b.</span><span class="sxs-lookup"><span data-stu-id="0086d-213">b.</span></span> <span data-ttu-id="0086d-214">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0086d-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0086d-215">c.</span><span class="sxs-lookup"><span data-stu-id="0086d-215">c.</span></span> <span data-ttu-id="0086d-216">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="0086d-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0086d-217">d.</span><span class="sxs-lookup"><span data-stu-id="0086d-217">d.</span></span> <span data-ttu-id="0086d-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0086d-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="0086d-219">Creare un utente di test di MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="0086d-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="0086d-220">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon MOVEit trasferimento - integrazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="0086d-221">MOVEit Transfer - Azure AD integration supporta il provisioning JIT, che è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="0086d-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="0086d-222">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0086d-222">There is no action item for you in this section.</span></span> <span data-ttu-id="0086d-223">Durante un tooaccess tentativo di trasferimento MOVEit - integrazione di Azure AD se non esiste ancora, viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="0086d-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="0086d-224">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [MOVEit trasferimento - team di supporto Client di integrazione di Azure AD](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="0086d-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0086d-225">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0086d-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0086d-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMOVEit trasferimento - integrazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="0086d-228">**tooassign Britta Simon tooMOVEit trasferimento - integrazione di Azure AD, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0086d-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="0086d-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0086d-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0086d-231">Nell'elenco di applicazioni hello, selezionare **MOVEit trasferimento - integrazione di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="0086d-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![integrazione di Azure AD di Hello MOVEit trasferimento - collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="0086d-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0086d-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="0086d-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0086d-235">Click **Add** button.</span></span> <span data-ttu-id="0086d-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0086d-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="0086d-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0086d-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0086d-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0086d-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0086d-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0086d-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0086d-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0086d-241">Test single sign-on</span></span>

<span data-ttu-id="0086d-242">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0086d-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0086d-243">Quando si fa clic su hello MOVEit trasferimento - riquadro integrazione di Azure AD in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour MOVEit trasferimento - applicazione di integrazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0086d-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0086d-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0086d-244">Additional resources</span></span>

* [<span data-ttu-id="0086d-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0086d-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0086d-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0086d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

