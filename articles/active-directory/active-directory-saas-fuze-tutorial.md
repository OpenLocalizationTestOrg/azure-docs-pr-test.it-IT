---
title: 'Esercitazione: Integrazione di Azure Active Directory con Fuze | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e catena pirotecnica.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="bd0d6-103">Esercitazione: Integrazione di Azure Active Directory con Fuze</span><span class="sxs-lookup"><span data-stu-id="bd0d6-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="bd0d6-104">In questa esercitazione, è illustrato come catena pirotecnica toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd0d6-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd0d6-105">Integrazione di catena pirotecnica con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd0d6-106">È possibile controllare in Azure AD che ha accesso tooFuze</span><span class="sxs-lookup"><span data-stu-id="bd0d6-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="bd0d6-107">È possibile abilitare l'utenti tooautomatically get connesso tooFuze (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd0d6-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="bd0d6-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="bd0d6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd0d6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd0d6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd0d6-110">Prerequisites</span></span>

<span data-ttu-id="bd0d6-111">integrazione di Azure AD con catena pirotecnica tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="bd0d6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd0d6-113">Sottoscrizione di Domo abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd0d6-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="bd0d6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="bd0d6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd0d6-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bd0d6-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd0d6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="bd0d6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bd0d6-118">Scenario description</span></span>
<span data-ttu-id="bd0d6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd0d6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd0d6-121">Aggiunta di catena pirotecnica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd0d6-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="bd0d6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="bd0d6-123">Aggiunta di catena pirotecnica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd0d6-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="bd0d6-124">integrazione hello tooconfigure di catena pirotecnica in Azure AD, è necessario tooadd catena pirotecnica dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd0d6-125">**tooadd catena pirotecnica dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd0d6-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0d6-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd0d6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd0d6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="bd0d6-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="bd0d6-133">Nella casella di ricerca hello, digitare **catena pirotecnica**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-133">In hello search box, type **Fuze**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="bd0d6-135">Nel riquadro dei risultati hello, selezionare **catena pirotecnica**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd0d6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd0d6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Fuze in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bd0d6-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd0d6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella catena pirotecnica è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="bd0d6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nella catena pirotecnica deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="bd0d6-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nella catena pirotecnica.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="bd0d6-142">tooconfigure e prova AD Azure single sign-on con catena pirotecnica, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd0d6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd0d6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd0d6-145">**[Creazione di un utente test catena pirotecnica](#creating-a-fuze-test-user)**  -toohave un equivalente di Britta Simon nella catena pirotecnica toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="bd0d6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd0d6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd0d6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd0d6-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione catena pirotecnica.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="bd0d6-150">**Azure AD tooconfigure single sign-on con catena pirotecnica, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd0d6-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0d6-151">Nel portale di gestione di Azure hello in hello **catena pirotecnica** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="bd0d6-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="bd0d6-155">In hello **catena pirotecnica dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="bd0d6-157">In hello **URL di accesso** casella di testo, digitare l'URL hello Sign-on come:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="bd0d6-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="bd0d6-158">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bd0d6-158">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="bd0d6-160">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file xml hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="bd0d6-162">tooconfigure single sign-on sul **catena pirotecnica** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di catena pirotecnica](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="bd0d6-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="bd0d6-163">Verrà impostata questa in hello toohave ordine connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd0d6-164">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd0d6-165">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="bd0d6-167">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd0d6-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0d6-168">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd0d6-170">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd0d6-172">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd0d6-174">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bd0d6-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd0d6-176">a.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-176">a.</span></span> <span data-ttu-id="bd0d6-177">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd0d6-178">b.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-178">b.</span></span> <span data-ttu-id="bd0d6-179">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd0d6-180">c.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-180">c.</span></span> <span data-ttu-id="bd0d6-181">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd0d6-182">d.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-182">d.</span></span> <span data-ttu-id="bd0d6-183">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="bd0d6-184">Creazione di un utente test di Fuze</span><span class="sxs-lookup"><span data-stu-id="bd0d6-184">Creating a Fuze test user</span></span>

<span data-ttu-id="bd0d6-185">L’applicazione Fuze supporta il provisioning just-in-time completo degli utenti che possono quindi essere creati automaticamente al momento dell’accesso.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="bd0d6-186">Per eventuali altri dettagli, contattare il [supporto](https://www.fuze.com/support) di Fuze.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd0d6-187">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0d6-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd0d6-188">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooFuze proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Assegna utente][200] 

<span data-ttu-id="bd0d6-190">**tooassign Britta Simon tooFuze, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd0d6-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0d6-191">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bd0d6-193">Nell'elenco di applicazioni hello, selezionare **catena pirotecnica**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-193">In hello applications list, select **Fuze**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="bd0d6-195">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="bd0d6-197">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-197">Click **Add** button.</span></span> <span data-ttu-id="bd0d6-198">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="bd0d6-200">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd0d6-201">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd0d6-202">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="bd0d6-203">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd0d6-203">Testing single sign-on</span></span>

<span data-ttu-id="bd0d6-204">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd0d6-205">Quando si fa clic su riquadro catena pirotecnica hello in hello Pannello di accesso, è necessario ottenere applicazione catena pirotecnica tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="bd0d6-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bd0d6-206">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bd0d6-206">Additional resources</span></span>

* [<span data-ttu-id="bd0d6-207">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd0d6-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd0d6-208">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd0d6-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png