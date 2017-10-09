---
title: 'Esercitazione: integrazione di Azure Active Directory con Lynda.com | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="f6936-103">Esercitazione: Integrazione di Azure Active Directory con Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f6936-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="f6936-104">In questa esercitazione, è illustrato come toointegrate Lynda.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6936-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6936-105">Integrazione di Lynda.com con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f6936-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6936-106">È possibile controllare in Azure AD che ha accesso tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="f6936-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="f6936-107">È possibile abilitare l'utenti tooautomatically get connesso tooLynda.com (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6936-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f6936-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6936-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6936-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6936-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6936-110">Prerequisites</span></span>

<span data-ttu-id="f6936-111">integrazione di Azure AD con Lynda.com tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f6936-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="f6936-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6936-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6936-113">Sottoscrizione di Lynda.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f6936-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6936-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f6936-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6936-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f6936-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6936-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f6936-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6936-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6936-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6936-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f6936-118">Scenario description</span></span>
<span data-ttu-id="f6936-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f6936-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6936-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f6936-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6936-121">Aggiunta di Lynda.com dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f6936-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="f6936-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="f6936-123">Aggiunta di Lynda.com dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f6936-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="f6936-124">integrazione hello tooconfigure di Lynda.com in Azure AD, è necessario tooadd Lynda.com dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f6936-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6936-125">**tooadd Lynda.com dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6936-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6936-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f6936-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6936-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f6936-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6936-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f6936-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f6936-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f6936-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f6936-133">Nella casella di ricerca hello, digitare **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f6936-133">In hello search box, type **Lynda.com**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="f6936-135">Nel riquadro dei risultati hello, selezionare **Lynda.com**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6936-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6936-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6936-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lynda.com usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6936-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f6936-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Lynda.com è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6936-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="f6936-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Lynda.com deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f6936-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="f6936-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f6936-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="f6936-142">tooconfigure e test Azure single sign-on AD con Lynda.com, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f6936-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6936-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6936-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6936-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6936-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6936-145">**[Creazione di un utente test Lynda.com](#creating-a-lyndacom-test-user)**  -toohave un equivalente di Britta Simon in Lynda.com che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f6936-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6936-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f6936-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6936-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f6936-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6936-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6936-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f6936-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="f6936-150">**Azure AD tooconfigure single sign-on con Lynda.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6936-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6936-151">Nel portale di Azure su hello hello **Lynda.com** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f6936-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f6936-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f6936-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="f6936-155">In hello **Lynda.com dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6936-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="f6936-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="f6936-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6936-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f6936-158">This value is not real.</span></span> <span data-ttu-id="f6936-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f6936-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f6936-160">Contatto [team di supporto di Lynda.com Client](https://www.linkedin.com/help/lynda/ask) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f6936-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="f6936-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f6936-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="f6936-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f6936-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6936-165">tooconfigure single sign-on sul **Lynda.com** lato, è necessario hello toosend scaricato **Metadata XML** [il supporto di Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="f6936-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6936-166">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6936-167">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f6936-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f6936-169">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6936-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6936-170">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f6936-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6936-172">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f6936-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6936-174">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f6936-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6936-176">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6936-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6936-178">a.</span><span class="sxs-lookup"><span data-stu-id="f6936-178">a.</span></span> <span data-ttu-id="f6936-179">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6936-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6936-180">b.</span><span class="sxs-lookup"><span data-stu-id="f6936-180">b.</span></span> <span data-ttu-id="f6936-181">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6936-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6936-182">c.</span><span class="sxs-lookup"><span data-stu-id="f6936-182">c.</span></span> <span data-ttu-id="f6936-183">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f6936-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6936-184">d.</span><span class="sxs-lookup"><span data-stu-id="f6936-184">d.</span></span> <span data-ttu-id="f6936-185">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f6936-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="f6936-186">Creazione di un utente test di Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f6936-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="f6936-187">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="f6936-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="f6936-188">Quando un utente assegnato tenta toolog in tooLynda.com mediante il pannello di accesso di hello, Lynda.com verifica se hello utente esiste.</span><span class="sxs-lookup"><span data-stu-id="f6936-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="f6936-189">Se l’account utente non è ancora disponibile, viene creato automaticamente da Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f6936-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="f6936-190">È possibile usare qualsiasi altro Lynda.com utente account strumento di creazione o le API fornite da Lynda.com tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="f6936-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6936-191">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6936-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6936-192">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="f6936-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f6936-194">**tooassign Britta Simon tooLynda.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6936-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6936-195">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f6936-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f6936-197">Nell'elenco di applicazioni hello, selezionare **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f6936-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="f6936-199">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f6936-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f6936-201">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f6936-201">Click **Add** button.</span></span> <span data-ttu-id="f6936-202">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f6936-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f6936-204">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f6936-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6936-205">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f6936-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6936-206">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f6936-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6936-207">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f6936-207">Testing single sign-on</span></span>

<span data-ttu-id="f6936-208">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f6936-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f6936-209">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6936-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f6936-210">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f6936-210">Additional resources</span></span>

* [<span data-ttu-id="f6936-211">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6936-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6936-212">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6936-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

