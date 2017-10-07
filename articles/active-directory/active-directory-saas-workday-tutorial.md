---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workday | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workday.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="07432-103">Esercitazione: Integrazione di Azure Active Directory con Workday</span><span class="sxs-lookup"><span data-stu-id="07432-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="07432-104">In questa esercitazione, è illustrato come toointegrate Workday con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07432-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07432-105">Integrazione Workday con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="07432-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="07432-106">È possibile controllare in Azure AD che ha accesso tooWorkday</span><span class="sxs-lookup"><span data-stu-id="07432-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="07432-107">È possibile abilitare l'utenti tooautomatically get connesso tooWorkday (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07432-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="07432-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="07432-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07432-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07432-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07432-110">Prerequisites</span></span>

<span data-ttu-id="07432-111">integrazione di Azure AD con Workday tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="07432-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="07432-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07432-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07432-113">Sottoscrizione di Workday abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07432-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07432-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="07432-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07432-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="07432-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07432-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="07432-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07432-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07432-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07432-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="07432-118">Scenario description</span></span>
<span data-ttu-id="07432-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="07432-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07432-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="07432-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07432-121">Aggiunta di Workday dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="07432-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="07432-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="07432-123">Aggiunta di Workday dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="07432-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="07432-124">integrazione hello tooconfigure di Workday in Azure AD, è necessario tooadd Workday dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="07432-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="07432-125">**tooadd Workday dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07432-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="07432-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07432-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07432-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="07432-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="07432-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07432-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="07432-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07432-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="07432-133">Nella casella di ricerca hello, digitare **Workday**.</span><span class="sxs-lookup"><span data-stu-id="07432-133">In hello search box, type **Workday**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="07432-135">Nel riquadro dei risultati hello, selezionare **Workday**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="07432-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07432-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07432-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workday in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07432-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="07432-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workday è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07432-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="07432-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workday richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="07432-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="07432-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Workday.</span><span class="sxs-lookup"><span data-stu-id="07432-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="07432-142">tooconfigure e test Azure single sign-on AD con Workday, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="07432-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="07432-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07432-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="07432-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07432-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07432-145">**[Creazione di un utente test Workday](#creating-a-workday-test-user)**  -toohave un equivalente di Britta Simon in Workday che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="07432-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="07432-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07432-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07432-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="07432-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07432-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07432-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workday.</span><span class="sxs-lookup"><span data-stu-id="07432-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="07432-150">**Azure AD tooconfigure single sign-on con Workday, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07432-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="07432-151">Nel portale di Azure su hello hello **Workday** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="07432-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="07432-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07432-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="07432-155">In hello **Workday dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="07432-157">a.</span><span class="sxs-lookup"><span data-stu-id="07432-157">a.</span></span> <span data-ttu-id="07432-158">In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="07432-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="07432-159">b.</span><span class="sxs-lookup"><span data-stu-id="07432-159">b.</span></span> <span data-ttu-id="07432-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="07432-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07432-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="07432-161">These values are not hello real.</span></span> <span data-ttu-id="07432-162">Aggiornare questi valori con URL hello effettivo Sign-on e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="07432-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="07432-163">L'URL di risposta deve avere un sottodominio, ad esempio www, wd2, wd3, wd3-impl, wd5, wd5-impl.</span><span class="sxs-lookup"><span data-stu-id="07432-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="07432-164">Usare qualcosa come "*http://www.myworkday.com*" funziona mentre "*http://myworkday.com*" non funziona.</span><span class="sxs-lookup"><span data-stu-id="07432-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="07432-165">Contatto [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="07432-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="07432-166">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="07432-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="07432-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="07432-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="07432-170">In hello **configurazione di Workday** fare clic su **configurare Workday** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="07432-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="07432-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="07432-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="07432-172">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="07432-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="07432-173">In una finestra del web browser, accedere come amministratore nel sito della società di tooyour Workday.</span><span class="sxs-lookup"><span data-stu-id="07432-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="07432-174">Andare troppo**Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="07432-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="07432-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="07432-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="07432-176">Andare troppo**Account amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="07432-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="07432-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="07432-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="07432-178">Andare troppo**Modifica configurazione Tenant-sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="07432-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="07432-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span><span class="sxs-lookup"><span data-stu-id="07432-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="07432-180">In hello **gli URL di reindirizzamento** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="07432-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span><span class="sxs-lookup"><span data-stu-id="07432-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="07432-182">a.</span><span class="sxs-lookup"><span data-stu-id="07432-182">a.</span></span> <span data-ttu-id="07432-183">Fare clic su **Aggiungi riga**.</span><span class="sxs-lookup"><span data-stu-id="07432-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="07432-184">b.</span><span class="sxs-lookup"><span data-stu-id="07432-184">b.</span></span> <span data-ttu-id="07432-185">In hello **Login Redirect URL** casella di testo e hello **Mobile Redirect URL** casella di testo, hello tipo **URL Sign-on** immesso in hello **Workday dominio e URL** sezione di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07432-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="07432-186">c.</span><span class="sxs-lookup"><span data-stu-id="07432-186">c.</span></span> <span data-ttu-id="07432-187">Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **Sign-Out URL**e quindi incollarlo hello **l'URL di reindirizzamento disconnessione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="07432-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="07432-188">d.</span><span class="sxs-lookup"><span data-stu-id="07432-188">d.</span></span>  <span data-ttu-id="07432-189">In **ambiente** casella di testo, nome del tipo hello ambiente.</span><span class="sxs-lookup"><span data-stu-id="07432-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="07432-190">Hello valore dell'attributo di ambiente hello è associato il valore toohello hello dell'URL del tenant:</span><span class="sxs-lookup"><span data-stu-id="07432-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="07432-191">-Se il nome di dominio hello di hello l'URL tenant Workday inizia con impl, ad esempio: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **ambiente** attributo deve essere impostato tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="07432-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="07432-192">-Se il nome di dominio hello inizia con un altro elemento, è necessario toocontact [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello corrispondenza **ambiente** valore.</span><span class="sxs-lookup"><span data-stu-id="07432-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="07432-193">In hello **SAML Setup** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="07432-194">![Configurazione SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="07432-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="07432-195">a.</span><span class="sxs-lookup"><span data-stu-id="07432-195">a.</span></span>  <span data-ttu-id="07432-196">Selezionare **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="07432-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="07432-197">b.</span><span class="sxs-lookup"><span data-stu-id="07432-197">b.</span></span>  <span data-ttu-id="07432-198">Fare clic su **Aggiungi riga**.</span><span class="sxs-lookup"><span data-stu-id="07432-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="07432-199">Nella sezione relativa ai provider di identità SAML hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="07432-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="07432-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="07432-201">a.</span><span class="sxs-lookup"><span data-stu-id="07432-201">a.</span></span> <span data-ttu-id="07432-202">Nella casella di testo Nome Provider di identità hello, digitare un nome di provider (ad esempio: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="07432-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="07432-203">b.</span><span class="sxs-lookup"><span data-stu-id="07432-203">b.</span></span> <span data-ttu-id="07432-204">Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **ID entità SAML** valore e quindi incollarlo hello **dell'autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="07432-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="07432-205">c.</span><span class="sxs-lookup"><span data-stu-id="07432-205">c.</span></span> <span data-ttu-id="07432-206">Selezionare **Enable Workday Initiated Logout** (Abilita disconnessione avviata da Workday).</span><span class="sxs-lookup"><span data-stu-id="07432-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="07432-207">d.</span><span class="sxs-lookup"><span data-stu-id="07432-207">d.</span></span> <span data-ttu-id="07432-208">Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **Sign-Out URL** valore e quindi incollarlo hello **URL richiesta di disconnessione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="07432-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="07432-209">e.</span><span class="sxs-lookup"><span data-stu-id="07432-209">e.</span></span> <span data-ttu-id="07432-210">Fare clic su **Certificato di chiave pubblica del provider di identità** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07432-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="07432-211">![Creare](./media/active-directory-saas-workday-tutorial/IC782928.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="07432-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="07432-212">f.</span><span class="sxs-lookup"><span data-stu-id="07432-212">f.</span></span> <span data-ttu-id="07432-213">Fare clic su **Crea chiave pubblica x509**.</span><span class="sxs-lookup"><span data-stu-id="07432-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="07432-214">![Creare](./media/active-directory-saas-workday-tutorial/IC782929.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="07432-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="07432-215">In hello **View x509 Public Key** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="07432-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span><span class="sxs-lookup"><span data-stu-id="07432-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="07432-217">a.</span><span class="sxs-lookup"><span data-stu-id="07432-217">a.</span></span> <span data-ttu-id="07432-218">In hello **nome** casella di testo, digitare un nome per il certificato (ad esempio: *DPI\_SP*).</span><span class="sxs-lookup"><span data-stu-id="07432-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="07432-219">b.</span><span class="sxs-lookup"><span data-stu-id="07432-219">b.</span></span> <span data-ttu-id="07432-220">In hello **valido dal** casella di testo, hello di tipo valido dal valore dell'attributo del certificato.</span><span class="sxs-lookup"><span data-stu-id="07432-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="07432-221">c.</span><span class="sxs-lookup"><span data-stu-id="07432-221">c.</span></span>  <span data-ttu-id="07432-222">In hello **valido per** casella di testo, valore di tipo hello tooattribute valido del certificato.</span><span class="sxs-lookup"><span data-stu-id="07432-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="07432-223">È possibile ottenere hello valido dalla data e hello toodate valido dal certificato scaricato hello facendovi doppio clic.</span><span class="sxs-lookup"><span data-stu-id="07432-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="07432-224">le date di Hello sono elencate sotto hello **dettagli** scheda.</span><span class="sxs-lookup"><span data-stu-id="07432-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="07432-225">d.</span><span class="sxs-lookup"><span data-stu-id="07432-225">d.</span></span>  <span data-ttu-id="07432-226">Aprire il certificato con codifica base 64 nel blocco note e quindi hello copia del contenuto di esso.</span><span class="sxs-lookup"><span data-stu-id="07432-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="07432-227">e.</span><span class="sxs-lookup"><span data-stu-id="07432-227">e.</span></span>  <span data-ttu-id="07432-228">In hello **certificato** casella di testo, incollare hello contenuto degli Appunti.</span><span class="sxs-lookup"><span data-stu-id="07432-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="07432-229">f.</span><span class="sxs-lookup"><span data-stu-id="07432-229">f.</span></span>  <span data-ttu-id="07432-230">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="07432-230">Click **OK**.</span></span>

15. <span data-ttu-id="07432-231">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="07432-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span><span class="sxs-lookup"><span data-stu-id="07432-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="07432-233">a.</span><span class="sxs-lookup"><span data-stu-id="07432-233">a.</span></span>  <span data-ttu-id="07432-234">Abilitare hello **x509 Private Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="07432-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="07432-235">b.</span><span class="sxs-lookup"><span data-stu-id="07432-235">b.</span></span>  <span data-ttu-id="07432-236">In hello **ID Provider di servizi** casella tipo **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="07432-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="07432-237">c.</span><span class="sxs-lookup"><span data-stu-id="07432-237">c.</span></span>  <span data-ttu-id="07432-238">Selezionare **Abilita autenticazione SAML SP initiated**.</span><span class="sxs-lookup"><span data-stu-id="07432-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="07432-239">d.</span><span class="sxs-lookup"><span data-stu-id="07432-239">d.</span></span>  <span data-ttu-id="07432-240">Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **URL servizio SSO IdP** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="07432-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="07432-241">e.</span><span class="sxs-lookup"><span data-stu-id="07432-241">e.</span></span> <span data-ttu-id="07432-242">Selezionare **Do Not Deflate SP-initiated Authentication Request**.</span><span class="sxs-lookup"><span data-stu-id="07432-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="07432-243">f.</span><span class="sxs-lookup"><span data-stu-id="07432-243">f.</span></span> <span data-ttu-id="07432-244">In **Authentication Request Signature Method** selezionare **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="07432-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="07432-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span><span class="sxs-lookup"><span data-stu-id="07432-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="07432-246">g.</span><span class="sxs-lookup"><span data-stu-id="07432-246">g.</span></span> <span data-ttu-id="07432-247">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="07432-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="07432-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="07432-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="07432-249">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="07432-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="07432-250">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="07432-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="07432-251">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07432-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07432-252">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="07432-253">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="07432-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="07432-255">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07432-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="07432-256">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07432-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07432-258">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="07432-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07432-260">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="07432-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07432-262">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07432-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07432-264">a.</span><span class="sxs-lookup"><span data-stu-id="07432-264">a.</span></span> <span data-ttu-id="07432-265">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07432-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07432-266">b.</span><span class="sxs-lookup"><span data-stu-id="07432-266">b.</span></span> <span data-ttu-id="07432-267">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="07432-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07432-268">c.</span><span class="sxs-lookup"><span data-stu-id="07432-268">c.</span></span> <span data-ttu-id="07432-269">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="07432-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="07432-270">d.</span><span class="sxs-lookup"><span data-stu-id="07432-270">d.</span></span> <span data-ttu-id="07432-271">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07432-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="07432-272">Creazione di un utente test di Workday</span><span class="sxs-lookup"><span data-stu-id="07432-272">Creating a Workday test user</span></span>

<span data-ttu-id="07432-273">tooget un utente di test, il provisioning in Workday, è necessario hello toocontact [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="07432-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="07432-274">Hello [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) Crea utente hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07432-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="07432-275">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="07432-276">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="07432-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Assegna utente][200] 

<span data-ttu-id="07432-278">**tooassign Britta Simon tooWorkday, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07432-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="07432-279">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07432-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="07432-281">Nell'elenco di applicazioni hello, selezionare **Workday**.</span><span class="sxs-lookup"><span data-stu-id="07432-281">In hello applications list, select **Workday**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="07432-283">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07432-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="07432-285">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07432-285">Click **Add** button.</span></span> <span data-ttu-id="07432-286">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07432-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="07432-288">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="07432-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="07432-289">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07432-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07432-290">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07432-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07432-291">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07432-291">Testing single sign-on</span></span>

<span data-ttu-id="07432-292">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="07432-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="07432-293">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07432-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07432-294">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="07432-294">Additional resources</span></span>

* [<span data-ttu-id="07432-295">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07432-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07432-296">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07432-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="07432-297">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="07432-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

