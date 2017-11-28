---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="baccf-103">Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="baccf-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="baccf-104">In questa esercitazione, è illustrato come toointegrate Dropbox for Business con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="baccf-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="baccf-105">Integrazione di Dropbox for Business con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="baccf-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="baccf-106">È possibile controllare in Azure AD che ha accesso tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="baccf-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="baccf-107">È possibile abilitare il get tooautomatically utenti connesso tooDropbox for Business (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="baccf-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="baccf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="baccf-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="baccf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baccf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="baccf-110">Prerequisites</span></span>

<span data-ttu-id="baccf-111">tooconfigure integrazione di Azure AD con Dropbox for Business, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="baccf-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="baccf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baccf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="baccf-113">Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="baccf-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="baccf-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="baccf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="baccf-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="baccf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="baccf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="baccf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="baccf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baccf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="baccf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="baccf-118">Scenario description</span></span>
<span data-ttu-id="baccf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="baccf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="baccf-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="baccf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="baccf-121">Aggiunta di Dropbox for Business dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="baccf-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="baccf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="baccf-123">Aggiunta di Dropbox for Business dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="baccf-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="baccf-124">integrazione di hello tooconfigure di Dropbox for Business in Azure AD, è necessario tooadd Dropbox for Business dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="baccf-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="baccf-125">**tooadd Dropbox for Business dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="baccf-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="baccf-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="baccf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="baccf-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="baccf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="baccf-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="baccf-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="baccf-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="baccf-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="baccf-133">Nella casella di ricerca hello, digitare **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="baccf-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="baccf-135">Nel riquadro dei risultati hello, selezionare **Dropbox for Business**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="baccf-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="baccf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="baccf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Dropbox for Business con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="baccf-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="baccf-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Dropbox for Business è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baccf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="baccf-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Dropbox for Business deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="baccf-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="baccf-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="baccf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="baccf-142">tooconfigure e test Azure single sign-on AD con Dropbox for Business, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="baccf-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="baccf-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="baccf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="baccf-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="baccf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="baccf-145">**[Creazione di una raccolta per l'utente test Business](#creating-a-dropbox-for-business-test-user)**  -toohave un equivalente di Britta Simon in Dropbox for Business che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="baccf-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="baccf-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="baccf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="baccf-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="baccf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="baccf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="baccf-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in Dropbox per applicazioni aziendali.</span><span class="sxs-lookup"><span data-stu-id="baccf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="baccf-150">**Azure AD tooconfigure single sign-on con Dropbox for Business, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="baccf-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="baccf-151">Nel portale di Azure su hello hello **Dropbox for Business** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="baccf-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="baccf-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="baccf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="baccf-155">In hello **Dropbox per il dominio di Business e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="baccf-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="baccf-156">a.</span><span class="sxs-lookup"><span data-stu-id="baccf-156">a.</span></span> <span data-ttu-id="baccf-157">Accesso tooyour Dropbox per il tenant di business.</span><span class="sxs-lookup"><span data-stu-id="baccf-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="baccf-158">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="baccf-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="baccf-159">b.</span><span class="sxs-lookup"><span data-stu-id="baccf-159">b.</span></span> <span data-ttu-id="baccf-160">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **Console di amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="baccf-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="baccf-161">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="baccf-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="baccf-162">c.</span><span class="sxs-lookup"><span data-stu-id="baccf-162">c.</span></span> <span data-ttu-id="baccf-163">In hello **Console di amministrazione**, fare clic su **autenticazione** nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="baccf-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="baccf-164">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="baccf-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="baccf-165">d.</span><span class="sxs-lookup"><span data-stu-id="baccf-165">d.</span></span> <span data-ttu-id="baccf-166">In hello **Single sign-on** selezionare **abilitare single sign-on**, quindi fare clic su **più** tooexpand in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="baccf-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="baccf-167">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="baccf-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="baccf-168">e.</span><span class="sxs-lookup"><span data-stu-id="baccf-168">e.</span></span> <span data-ttu-id="baccf-169">Copia URL hello accanto troppo**gli utenti possono accedere immettendo l'indirizzo di posta elettronica oppure possono passare direttamente a**.</span><span class="sxs-lookup"><span data-stu-id="baccf-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="baccf-171">f.</span><span class="sxs-lookup"><span data-stu-id="baccf-171">f.</span></span> <span data-ttu-id="baccf-172">Nel portale di Azure in hello hello **Sign-on URL** casella di testo, incollare hello URL.</span><span class="sxs-lookup"><span data-stu-id="baccf-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="baccf-174">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="baccf-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="baccf-175">Poiché il valore non è reale,</span><span class="sxs-lookup"><span data-stu-id="baccf-175">This value is not real value.</span></span> <span data-ttu-id="baccf-176">Aggiornare il valore di hello con hello Sign-on URL effettivo è ottenere dalla sezione Single sign-on.</span><span class="sxs-lookup"><span data-stu-id="baccf-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="baccf-177">Contatto [Dropbox per il team di supporto Client di Business](https://www.dropbox.com/business/contact) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="baccf-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="baccf-178">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="baccf-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="baccf-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="baccf-180">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="baccf-182">In hello **Dropbox for Business configurazione** fare clic su **configurare Dropbox for Business** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="baccf-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="baccf-183">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="baccf-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="baccf-185">tooconfigure single sign-on sul **Dropbox for Business** sul lato, andare il tenant Dropbox for Business, in hello **Single sign-on** sezione di hello **autenticazione** pagina eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="baccf-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="baccf-186">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="baccf-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="baccf-187">a.</span><span class="sxs-lookup"><span data-stu-id="baccf-187">a.</span></span> <span data-ttu-id="baccf-188">Fare clic su **Required**.</span><span class="sxs-lookup"><span data-stu-id="baccf-188">Click **Required**.</span></span>
   
    <span data-ttu-id="baccf-189">b.</span><span class="sxs-lookup"><span data-stu-id="baccf-189">b.</span></span> <span data-ttu-id="baccf-190">Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="baccf-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="baccf-191">c.</span><span class="sxs-lookup"><span data-stu-id="baccf-191">c.</span></span> <span data-ttu-id="baccf-192">Fare clic su **Seleziona certificato**, quindi selezionare tooyour **file di certificato con codifica Base64**.</span><span class="sxs-lookup"><span data-stu-id="baccf-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="baccf-193">d.</span><span class="sxs-lookup"><span data-stu-id="baccf-193">d.</span></span> <span data-ttu-id="baccf-194">Fare clic su **salvare modifiche** toocomplete configurazione hello del tenant DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="baccf-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="baccf-195">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="baccf-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="baccf-196">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="baccf-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="baccf-197">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="baccf-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="baccf-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="baccf-199">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="baccf-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="baccf-201">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="baccf-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="baccf-202">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="baccf-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="baccf-204">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="baccf-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="baccf-206">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="baccf-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="baccf-208">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="baccf-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="baccf-210">a.</span><span class="sxs-lookup"><span data-stu-id="baccf-210">a.</span></span> <span data-ttu-id="baccf-211">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="baccf-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="baccf-212">b.</span><span class="sxs-lookup"><span data-stu-id="baccf-212">b.</span></span> <span data-ttu-id="baccf-213">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="baccf-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="baccf-214">c.</span><span class="sxs-lookup"><span data-stu-id="baccf-214">c.</span></span> <span data-ttu-id="baccf-215">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="baccf-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="baccf-216">d.</span><span class="sxs-lookup"><span data-stu-id="baccf-216">d.</span></span> <span data-ttu-id="baccf-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="baccf-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="baccf-218">Creazione di un utente test di Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="baccf-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="baccf-219">In questa sezione viene creato un utente di nome Britta Simon in Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="baccf-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="baccf-220">Dropbox for Business supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="baccf-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="baccf-221">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="baccf-221">There is no action item for you in this section.</span></span> <span data-ttu-id="baccf-222">Se un utente non esiste già in Dropbox for Business, viene creato uno nuovo quando si tenta di tooaccess Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="baccf-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="baccf-223">Se è necessario toocreate manualmente, contattare l'utente [Dropbox per il team di supporto Client di Business](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="baccf-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="baccf-224">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="baccf-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="baccf-225">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="baccf-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Assegna utente][200] 

<span data-ttu-id="baccf-227">**tooassign tooDropbox Britta Simon for Business, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="baccf-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="baccf-228">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="baccf-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="baccf-230">Nell'elenco di applicazioni hello, selezionare **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="baccf-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="baccf-232">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="baccf-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="baccf-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="baccf-234">Click **Add** button.</span></span> <span data-ttu-id="baccf-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="baccf-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="baccf-237">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="baccf-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="baccf-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="baccf-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="baccf-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="baccf-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="baccf-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="baccf-240">Testing single sign-on</span></span>

<span data-ttu-id="baccf-241">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="baccf-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="baccf-242">Quando si fa clic hello Dropbox per il riquadro di Business nel Pannello di accesso hello, è necessario ottenere la pagina di accesso di Dropbox per applicazioni aziendali.</span><span class="sxs-lookup"><span data-stu-id="baccf-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="baccf-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="baccf-243">Additional resources</span></span>

* [<span data-ttu-id="baccf-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baccf-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="baccf-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baccf-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="baccf-246">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="baccf-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

