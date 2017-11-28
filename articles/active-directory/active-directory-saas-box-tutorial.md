---
title: 'Esercitazione: Integrazione di Azure Active Directory con Box | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Box.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="fbb46-103">Esercitazione: Integrazione di Azure Active Directory con Box</span><span class="sxs-lookup"><span data-stu-id="fbb46-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="fbb46-104">In questa esercitazione, è illustrato come toointegrate casella con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbb46-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbb46-105">Casella di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fbb46-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbb46-106">È possibile controllare in Azure AD che ha accesso tooBox</span><span class="sxs-lookup"><span data-stu-id="fbb46-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="fbb46-107">È possibile abilitare l'utenti tooautomatically get connesso tooBox (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbb46-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fbb46-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbb46-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbb46-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbb46-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fbb46-110">Prerequisites</span></span>

<span data-ttu-id="fbb46-111">integrazione di Azure AD con Box tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fbb46-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="fbb46-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbb46-113">Sottoscrizione di Box abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fbb46-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbb46-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fbb46-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbb46-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fbb46-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbb46-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fbb46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbb46-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbb46-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbb46-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fbb46-118">Scenario description</span></span>
<span data-ttu-id="fbb46-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fbb46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbb46-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fbb46-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbb46-121">Aggiunta di casella dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fbb46-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="fbb46-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="fbb46-123">Aggiunta di casella dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fbb46-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="fbb46-124">integrazione hello tooconfigure della casella in Azure AD, è necessario tooadd casella dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fbb46-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbb46-125">**tooadd casella dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbb46-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbb46-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fbb46-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbb46-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbb46-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fbb46-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fbb46-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fbb46-133">Nella casella di ricerca hello, digitare **casella**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-133">In hello search box, type **Box**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="fbb46-135">Nel riquadro dei risultati hello, selezionare **casella**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fbb46-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbb46-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbb46-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Box in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fbb46-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbb46-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella casella è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb46-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="fbb46-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nella casella deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fbb46-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="fbb46-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nella casella.</span><span class="sxs-lookup"><span data-stu-id="fbb46-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="fbb46-142">tooconfigure e prova AD Azure single sign-on con casella, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fbb46-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbb46-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fbb46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbb46-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbb46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbb46-145">**[Creazione di un utente test casella](#creating-a-box-test-user)**  -toohave un equivalente di Britta Simon nella casella che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fbb46-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbb46-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbb46-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbb46-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fbb46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbb46-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbb46-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione casella.</span><span class="sxs-lookup"><span data-stu-id="fbb46-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="fbb46-150">**Azure AD tooconfigure single sign-on con casella eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbb46-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbb46-151">Nel portale di Azure su hello hello **casella** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fbb46-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbb46-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="fbb46-155">In hello **casella dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fbb46-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="fbb46-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="fbb46-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbb46-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="fbb46-158">This value is not real.</span></span> <span data-ttu-id="fbb46-159">Aggiornare il valore di hello con URL hello effettivo Sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbb46-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="fbb46-160">Contatto [team di supporto Client casella](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="fbb46-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="fbb46-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fbb46-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="fbb46-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fbb46-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbb46-165">tooget SSO configurato per l'applicazione, contattare [team di supporto Client casella](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) e fornire loro file XML di hello scaricato.</span><span class="sxs-lookup"><span data-stu-id="fbb46-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="fbb46-166">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fbb46-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbb46-167">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fbb46-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbb46-168">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbb46-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbb46-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbb46-170">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fbb46-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fbb46-172">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbb46-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbb46-173">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fbb46-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbb46-175">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbb46-177">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fbb46-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbb46-179">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fbb46-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbb46-181">a.</span><span class="sxs-lookup"><span data-stu-id="fbb46-181">a.</span></span> <span data-ttu-id="fbb46-182">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbb46-183">b.</span><span class="sxs-lookup"><span data-stu-id="fbb46-183">b.</span></span> <span data-ttu-id="fbb46-184">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbb46-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbb46-185">c.</span><span class="sxs-lookup"><span data-stu-id="fbb46-185">c.</span></span> <span data-ttu-id="fbb46-186">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbb46-187">d.</span><span class="sxs-lookup"><span data-stu-id="fbb46-187">d.</span></span> <span data-ttu-id="fbb46-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="fbb46-189">Creazione di un utente test di Box</span><span class="sxs-lookup"><span data-stu-id="fbb46-189">Creating a Box test user</span></span>

<span data-ttu-id="fbb46-190">In questa sezione si crea un utente di nome Britta Simon in Box.</span><span class="sxs-lookup"><span data-stu-id="fbb46-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="fbb46-191">Box supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fbb46-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="fbb46-192">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fbb46-192">There is no action item for you in this section.</span></span> <span data-ttu-id="fbb46-193">Se un utente non esiste già nella casella, viene creato uno nuovo quando si tenta di tooaccess casella.</span><span class="sxs-lookup"><span data-stu-id="fbb46-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbb46-194">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb46-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbb46-195">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBox.</span><span class="sxs-lookup"><span data-stu-id="fbb46-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fbb46-197">**tooassign Britta Simon tooBox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbb46-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbb46-198">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fbb46-200">Nell'elenco di applicazioni hello, selezionare **casella**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-200">In hello applications list, select **Box**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="fbb46-202">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fbb46-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-204">Click **Add** button.</span></span> <span data-ttu-id="fbb46-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fbb46-207">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fbb46-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbb46-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbb46-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fbb46-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbb46-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fbb46-210">Testing single sign-on</span></span>

<span data-ttu-id="fbb46-211">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fbb46-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbb46-212">Quando si fa clic su riquadro casella hello in hello Pannello di accesso, è necessario ottenere l'account di accesso pagina tooget connesso tooyour applicazione casella.</span><span class="sxs-lookup"><span data-stu-id="fbb46-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbb46-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fbb46-213">Additional resources</span></span>

* [<span data-ttu-id="fbb46-214">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbb46-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbb46-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbb46-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fbb46-216">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fbb46-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

