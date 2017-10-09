---
title: 'Esercitazione: Integrazione di Azure Active Directory con TigerText Secure Messenger | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TigerText Secure Messenger.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="749c8-103">Esercitazione: Integrazione di Azure Active Directory con TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="749c8-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="749c8-104">In questa esercitazione, è illustrato come toointegrate TigerText sicura Messenger con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="749c8-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="749c8-105">Integrazione di Messenger Secure TigerText con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="749c8-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="749c8-106">È possibile controllare in Azure AD che ha accesso tooTigerText Messenger sicura</span><span class="sxs-lookup"><span data-stu-id="749c8-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="749c8-107">È possibile abilitare il get tooautomatically utenti connesso tooTigerText Secure Messenger (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="749c8-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="749c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="749c8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="749c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="749c8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="749c8-110">Prerequisites</span></span>

<span data-ttu-id="749c8-111">integrazione di Azure AD con Messenger Secure TigerText tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="749c8-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="749c8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="749c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="749c8-113">Sottoscrizione di TigerText Secure Messenger abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="749c8-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="749c8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="749c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="749c8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="749c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="749c8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="749c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="749c8-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="749c8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="749c8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="749c8-118">Scenario description</span></span>
<span data-ttu-id="749c8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="749c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="749c8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="749c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="749c8-121">Aggiungere TigerText Secure Messenger dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="749c8-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="749c8-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="749c8-123">Aggiungere TigerText Secure Messenger dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="749c8-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="749c8-124">integrazione hello tooconfigure di Messenger Secure TigerText in Azure AD, è necessario tooadd TigerText Secure Messenger dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="749c8-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="749c8-125">**tooadd TigerText Secure Messenger dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="749c8-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="749c8-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="749c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="749c8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="749c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="749c8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="749c8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="749c8-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="749c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="749c8-133">Nella casella di ricerca hello, digitare **TigerText Secure Messenger**selezionare **TigerText Secure Messenger** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="749c8-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="749c8-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="749c8-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TigerText Secure Messenger usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="749c8-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="749c8-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Messenger Secure TigerText è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="749c8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="749c8-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello TigerText Secure Messenger deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="749c8-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="749c8-139">TigerText Secure Messenger, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="749c8-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="749c8-140">tooconfigure e prova AD Azure single sign-on con TigerText Secure Messenger, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="749c8-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="749c8-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="749c8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="749c8-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="749c8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="749c8-143">**[Creare un utente test Messenger Secure TigerText](#create-a-tigertext-secure-messenger-test-user)**  -toohave un equivalente di Britta Simon TigerText Secure Messenger che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="749c8-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="749c8-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="749c8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="749c8-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="749c8-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="749c8-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="749c8-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="749c8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="749c8-148">**tooconfigure AD Azure single sign-on con TigerText Secure Messenger, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="749c8-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="749c8-149">Nel portale di Azure su hello hello **TigerText Secure Messenger** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="749c8-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="749c8-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="749c8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="749c8-153">In hello **TigerText Secure Messenger dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="749c8-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Sezione URL e dominio TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="749c8-155">a.</span><span class="sxs-lookup"><span data-stu-id="749c8-155">a.</span></span> <span data-ttu-id="749c8-156">In hello **Sign-on URL** casella di testo, digitare l'URL come:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="749c8-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="749c8-157">b.</span><span class="sxs-lookup"><span data-stu-id="749c8-157">b.</span></span> <span data-ttu-id="749c8-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="749c8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="749c8-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="749c8-159">This value is not real.</span></span> <span data-ttu-id="749c8-160">Aggiorna il valore con hello identificatore effettivo.</span><span class="sxs-lookup"><span data-stu-id="749c8-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="749c8-161">Contatto [team di supporto Client di Messaggistica sicura TigerText](mailTo:prosupport@tigertext.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="749c8-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="749c8-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="749c8-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="749c8-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="749c8-164">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="749c8-166">tooget accesso single sign-on configurato per l'applicazione, contattare [team di supporto di Messenger Secure TigerText](mailTo:prosupport@tigertext.com) e fornire loro hello **metadati scaricati**.</span><span class="sxs-lookup"><span data-stu-id="749c8-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="749c8-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="749c8-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="749c8-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="749c8-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="749c8-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="749c8-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="749c8-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-170">Create an Azure AD test user</span></span>
<span data-ttu-id="749c8-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="749c8-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="749c8-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="749c8-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="749c8-174">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="749c8-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="749c8-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="749c8-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="749c8-178">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="749c8-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="749c8-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="749c8-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Finestra di dialogo utente](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="749c8-182">a.</span><span class="sxs-lookup"><span data-stu-id="749c8-182">a.</span></span> <span data-ttu-id="749c8-183">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="749c8-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="749c8-184">b.</span><span class="sxs-lookup"><span data-stu-id="749c8-184">b.</span></span> <span data-ttu-id="749c8-185">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="749c8-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="749c8-186">c.</span><span class="sxs-lookup"><span data-stu-id="749c8-186">c.</span></span> <span data-ttu-id="749c8-187">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="749c8-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="749c8-188">d.</span><span class="sxs-lookup"><span data-stu-id="749c8-188">d.</span></span> <span data-ttu-id="749c8-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="749c8-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="749c8-190">Creare un utente di test di TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="749c8-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="749c8-191">In questa sezione viene creato un utente di nome Britta Simon in TigerText.</span><span class="sxs-lookup"><span data-stu-id="749c8-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="749c8-192">Per raggiungere troppo[team di supporto Client di Messaggistica sicura TigerText](mailTo:prosupport@tigertext.com) utenti hello tooadd nella piattaforma TigerText hello.</span><span class="sxs-lookup"><span data-stu-id="749c8-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="749c8-193">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="749c8-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="749c8-194">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso tooTigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="749c8-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Assegna utente][200] 

<span data-ttu-id="749c8-196">**tooassign Britta Simon tooTigerText Messenger Secure, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="749c8-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="749c8-197">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="749c8-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="749c8-199">Nell'elenco di applicazioni hello, selezionare **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="749c8-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger nell'elenco delle app](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="749c8-201">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="749c8-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="749c8-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="749c8-203">Click **Add** button.</span></span> <span data-ttu-id="749c8-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="749c8-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="749c8-206">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="749c8-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="749c8-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="749c8-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="749c8-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="749c8-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="749c8-209">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="749c8-209">Test single sign-on</span></span>

<span data-ttu-id="749c8-210">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="749c8-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="749c8-211">Quando si fa clic su riquadro TigerText hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour TigerText applicazione.</span><span class="sxs-lookup"><span data-stu-id="749c8-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="749c8-212">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="749c8-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="749c8-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="749c8-213">Additional resources</span></span>

* [<span data-ttu-id="749c8-214">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="749c8-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="749c8-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="749c8-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

