---
title: 'Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e informazioni su Lavagna.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="32f5c-103">Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="32f5c-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="32f5c-104">In questa esercitazione, è illustrato come toointegrate Lavagna informazioni con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32f5c-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32f5c-105">Integrazione di informazioni su lavagna con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="32f5c-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32f5c-106">È possibile controllare in Azure AD che ha accesso tooBlackboard informazioni</span><span class="sxs-lookup"><span data-stu-id="32f5c-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="32f5c-107">È possibile abilitare l'utenti tooautomatically get connesso tooBlackboard informazioni (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32f5c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="32f5c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32f5c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32f5c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32f5c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32f5c-110">Prerequisites</span></span>

<span data-ttu-id="32f5c-111">integrazione di Azure AD con informazioni su Lavagna tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="32f5c-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="32f5c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32f5c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32f5c-113">Sottoscrizione di Blackboard Learn abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32f5c-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32f5c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="32f5c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32f5c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="32f5c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32f5c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="32f5c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32f5c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32f5c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32f5c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="32f5c-118">Scenario description</span></span>
<span data-ttu-id="32f5c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="32f5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32f5c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="32f5c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32f5c-121">Aggiunta di ulteriori Lavagna dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="32f5c-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="32f5c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="32f5c-123">Aggiunta di ulteriori Lavagna dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="32f5c-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="32f5c-124">integrazione hello tooconfigure di lavagna altre in Azure AD, è necessario tooadd Lavagna informazioni dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="32f5c-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32f5c-125">**tooadd Lavagna informazioni dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32f5c-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f5c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="32f5c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32f5c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32f5c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="32f5c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="32f5c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="32f5c-133">Nella casella di ricerca hello, digitare **Lavagna informazioni**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="32f5c-135">Nel riquadro dei risultati hello, selezionare **Lavagna informazioni**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32f5c-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32f5c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32f5c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Blackboard Learn usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32f5c-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32f5c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in altre lavagna è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32f5c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="32f5c-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e utente correlati hello informazioni Lavagna deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="32f5c-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="32f5c-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nella Lavagna informazioni.</span><span class="sxs-lookup"><span data-stu-id="32f5c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="32f5c-142">tooconfigure e prova AD Azure single sign-on con informazioni su Lavagna, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="32f5c-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32f5c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="32f5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32f5c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32f5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32f5c-145">**[Creazione di un utente test Lavagna informazioni](#creating-a-blackboard-learn-test-user)**  -toohave un equivalente di Britta Simon nella Lavagna informazioni che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="32f5c-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32f5c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32f5c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32f5c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="32f5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32f5c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32f5c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lavagna informazioni.</span><span class="sxs-lookup"><span data-stu-id="32f5c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="32f5c-150">**tooconfigure AD Azure single sign-on con informazioni su Lavagna, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32f5c-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f5c-151">Nel portale di Azure su hello hello **Lavagna informazioni** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="32f5c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32f5c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="32f5c-155">In hello **Lavagna informazioni dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32f5c-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="32f5c-157">a.</span><span class="sxs-lookup"><span data-stu-id="32f5c-157">a.</span></span> <span data-ttu-id="32f5c-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="32f5c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="32f5c-159">b.</span><span class="sxs-lookup"><span data-stu-id="32f5c-159">b.</span></span> <span data-ttu-id="32f5c-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="32f5c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="32f5c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="32f5c-161">These values are not real.</span></span> <span data-ttu-id="32f5c-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="32f5c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32f5c-163">Contatto [team di supporto Client di informazioni su Lavagna](https://www.blackboard.com/support/index.aspx) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="32f5c-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="32f5c-164">Applicazione di informazioni di lavagna prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="32f5c-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="32f5c-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="32f5c-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="32f5c-166">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32f5c-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="32f5c-167">Hello seguente schermata mostra un esempio su di esso.</span><span class="sxs-lookup"><span data-stu-id="32f5c-167">hello following screenshot shows an example about it.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="32f5c-169">In hello **gli attributi utente** sezione **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="32f5c-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="32f5c-170">È stato eseguito il mapping di hello Userprincipalname come attributo utente univoco hello ma è possibile eseguirne il mapping toohello valore appropriato, che distingue in modo univoco l'utente hello hello organizzazione e che esegue il mapping di campo del nome utente tooBlackboard informazioni.</span><span class="sxs-lookup"><span data-stu-id="32f5c-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="32f5c-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="32f5c-171">Attribute Name</span></span> | <span data-ttu-id="32f5c-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="32f5c-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="32f5c-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="32f5c-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="32f5c-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="32f5c-174">user.userprincipalname</span></span> |

    <span data-ttu-id="32f5c-175">a.</span><span class="sxs-lookup"><span data-stu-id="32f5c-175">a.</span></span> <span data-ttu-id="32f5c-176">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="32f5c-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="32f5c-179">b.</span><span class="sxs-lookup"><span data-stu-id="32f5c-179">b.</span></span> <span data-ttu-id="32f5c-180">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="32f5c-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="32f5c-181">c.</span><span class="sxs-lookup"><span data-stu-id="32f5c-181">c.</span></span> <span data-ttu-id="32f5c-182">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="32f5c-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="32f5c-183">d.</span><span class="sxs-lookup"><span data-stu-id="32f5c-183">d.</span></span> <span data-ttu-id="32f5c-184">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-184">Click **Ok**.</span></span>

4. <span data-ttu-id="32f5c-185">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="32f5c-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="32f5c-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="32f5c-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="32f5c-189">In hello **Lavagna informazioni su configurazione** fare clic su **configurare informazioni Lavagna** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="32f5c-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32f5c-190">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="32f5c-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="32f5c-192">tooconfigure single sign-on sul **Lavagna informazioni** lato, è necessario hello toosend scaricato **Metadata XML** e **ID entità SAML** troppo[informazioni Lavagna supporta](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="32f5c-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="32f5c-193">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="32f5c-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32f5c-194">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="32f5c-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32f5c-195">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32f5c-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32f5c-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="32f5c-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="32f5c-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="32f5c-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32f5c-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f5c-200">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="32f5c-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32f5c-202">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32f5c-204">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="32f5c-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32f5c-206">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32f5c-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32f5c-208">a.</span><span class="sxs-lookup"><span data-stu-id="32f5c-208">a.</span></span> <span data-ttu-id="32f5c-209">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32f5c-210">b.</span><span class="sxs-lookup"><span data-stu-id="32f5c-210">b.</span></span> <span data-ttu-id="32f5c-211">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32f5c-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="32f5c-212">c.</span><span class="sxs-lookup"><span data-stu-id="32f5c-212">c.</span></span> <span data-ttu-id="32f5c-213">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32f5c-214">d.</span><span class="sxs-lookup"><span data-stu-id="32f5c-214">d.</span></span> <span data-ttu-id="32f5c-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="32f5c-216">Creazione di un utente di test di Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="32f5c-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="32f5c-217">In questa sezione viene creato un utente di nome Britta Simon in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="32f5c-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="32f5c-218">L'applicazione Blackboard Learn supporta il provisioning degli utenti just-in-time.</span><span class="sxs-lookup"><span data-stu-id="32f5c-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="32f5c-219">Assicurarsi di aver configurato le attestazioni hello come descritto nella sezione hello  **[configurazione Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="32f5c-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32f5c-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f5c-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32f5c-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBlackboard informazioni.</span><span class="sxs-lookup"><span data-stu-id="32f5c-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Assegna utente][200] 

<span data-ttu-id="32f5c-223">**tooassign Britta Simon tooBlackboard ulteriori informazioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32f5c-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f5c-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="32f5c-226">Nell'elenco di applicazioni hello, selezionare **Lavagna informazioni**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="32f5c-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="32f5c-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-230">Click **Add** button.</span></span> <span data-ttu-id="32f5c-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="32f5c-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="32f5c-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32f5c-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32f5c-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32f5c-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32f5c-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32f5c-236">Testing single sign-on</span></span>

<span data-ttu-id="32f5c-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="32f5c-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32f5c-238">Quando si fa clic su riquadro informazioni Lavagna hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Lavagna altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="32f5c-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="32f5c-239">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32f5c-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32f5c-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="32f5c-240">Additional resources</span></span>

* [<span data-ttu-id="32f5c-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32f5c-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32f5c-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32f5c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

