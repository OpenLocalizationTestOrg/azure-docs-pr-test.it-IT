---
title: 'Esercitazione: integrazione di Azure Active Directory con LinkedIn Lookup| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e la ricerca di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="193cf-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="193cf-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="193cf-104">In questa esercitazione, è illustrato come toointegrate ricerca LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="193cf-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="193cf-105">Integrazione di ricerca di LinkedIn con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="193cf-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="193cf-106">È possibile controllare in Azure AD che ha accesso tooLinkedIn ricerca</span><span class="sxs-lookup"><span data-stu-id="193cf-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="193cf-107">È possibile abilitare l'utenti tooautomatically get connesso tooLinkedIn ricerca (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="193cf-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="193cf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="193cf-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="193cf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="193cf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="193cf-110">Prerequisites</span></span>

<span data-ttu-id="193cf-111">integrazione di Azure AD con ricerca LinkedIn tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="193cf-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="193cf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="193cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="193cf-113">Sottoscrizione di LinkedIn Lookup abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="193cf-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="193cf-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="193cf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="193cf-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="193cf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="193cf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="193cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="193cf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="193cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="193cf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="193cf-118">Scenario description</span></span>
<span data-ttu-id="193cf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="193cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="193cf-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="193cf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="193cf-121">Aggiunta di ricerca di LinkedIn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="193cf-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="193cf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="193cf-123">Aggiunta di ricerca di LinkedIn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="193cf-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="193cf-124">integrazione hello tooconfigure di ricerca di LinkedIn in Azure AD, è necessario tooadd LinkedIn ricerca dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="193cf-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="193cf-125">**tooadd ricerca LinkedIn dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="193cf-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="193cf-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="193cf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="193cf-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="193cf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="193cf-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="193cf-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="193cf-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello di hello finestra di dialogo tooadd nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="193cf-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="193cf-133">Nella casella di ricerca hello, digitare **LinkedIn ricerca**.</span><span class="sxs-lookup"><span data-stu-id="193cf-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="193cf-135">Nel riquadro dei risultati hello, selezionare **ricerca LinkedIn**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="193cf-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="193cf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="193cf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Lookup in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="193cf-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="193cf-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ricerca di LinkedIn è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="193cf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="193cf-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in ricerca di LinkedIn deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="193cf-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="193cf-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nella ricerca di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="193cf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="193cf-142">tooconfigure e prova AD Azure single sign-on con LinkedIn ricerca, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="193cf-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="193cf-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="193cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="193cf-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="193cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="193cf-145">**[Creazione di un utente test ricerca LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave un equivalente di Britta Simon nella ricerca di LinkedIn che è la rappresentazione toohello collegato AD Azure.</span><span class="sxs-lookup"><span data-stu-id="193cf-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="193cf-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="193cf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="193cf-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="193cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="193cf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="193cf-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione di ricerca di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="193cf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="193cf-150">**Azure AD tooconfigure single sign-on con ricerca LinkedIn, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="193cf-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="193cf-151">Nel portale di Azure su hello hello **ricerca LinkedIn** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="193cf-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="193cf-153">In hello **Single sign-on** finestra di dialogo, nella **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="193cf-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="193cf-155">In una finestra del web browser, accesso tooyour **ricerca LinkedIn** sito Web come amministratore.</span><span class="sxs-lookup"><span data-stu-id="193cf-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="193cf-156">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="193cf-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="193cf-157">Selezionare inoltre **ricerca** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="193cf-159">Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="193cf-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="193cf-161">Nel portale di Azure in **URL e il dominio di ricerca di LinkedIn** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="193cf-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="193cf-163">a.</span><span class="sxs-lookup"><span data-stu-id="193cf-163">a.</span></span> <span data-ttu-id="193cf-164">In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="193cf-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="193cf-165">b.</span><span class="sxs-lookup"><span data-stu-id="193cf-165">b.</span></span> <span data-ttu-id="193cf-166">In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="193cf-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="193cf-167">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="193cf-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="193cf-169">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="193cf-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="193cf-170">Questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="193cf-170">This is not real value.</span></span> <span data-ttu-id="193cf-171">utente Hello presenta tooupdate questi valori con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="193cf-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="193cf-172">Contatto [team di supporto Client di LinkedIn ricerca](https://business.LinkedIn.com/lookup) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="193cf-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="193cf-173">Il **ricerca LinkedIn** asserzioni SAML hello prevista dall'applicazione in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="193cf-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="193cf-174">Hello utente dispone di configurazione di attributi del token SAML tooadd attributo personalizzato mapping toohello.</span><span class="sxs-lookup"><span data-stu-id="193cf-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="193cf-175">Hello seguente schermata mostra un esempio.</span><span class="sxs-lookup"><span data-stu-id="193cf-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="193cf-176">il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn ricerca prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="193cf-177">È possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="193cf-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="193cf-179">In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="193cf-180">Hello utente necessita di attestazioni di quattro tooadd denominate **posta elettronica**, **reparto**, **firstname**, e **lastname** e il valore di hello è mappata a toobe **user.mail**, **Department**, **user.givenname**, e **user.surname** rispettivamente</span><span class="sxs-lookup"><span data-stu-id="193cf-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="193cf-181">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="193cf-181">Attribute Name</span></span> | <span data-ttu-id="193cf-182">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="193cf-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="193cf-183">email</span><span class="sxs-lookup"><span data-stu-id="193cf-183">email</span></span>| <span data-ttu-id="193cf-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="193cf-184">user.mail</span></span> |    
    | <span data-ttu-id="193cf-185">department</span><span class="sxs-lookup"><span data-stu-id="193cf-185">department</span></span>| <span data-ttu-id="193cf-186">user.department</span><span class="sxs-lookup"><span data-stu-id="193cf-186">user.department</span></span> |
    | <span data-ttu-id="193cf-187">firstname</span><span class="sxs-lookup"><span data-stu-id="193cf-187">firstname</span></span>| <span data-ttu-id="193cf-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="193cf-188">user.givenname</span></span> |
    | <span data-ttu-id="193cf-189">lastname</span><span class="sxs-lookup"><span data-stu-id="193cf-189">lastname</span></span>| <span data-ttu-id="193cf-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="193cf-190">user.surname</span></span> |

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="193cf-192">a.</span><span class="sxs-lookup"><span data-stu-id="193cf-192">a.</span></span> <span data-ttu-id="193cf-193">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="193cf-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="193cf-196">b.</span><span class="sxs-lookup"><span data-stu-id="193cf-196">b.</span></span> <span data-ttu-id="193cf-197">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="193cf-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="193cf-198">c.</span><span class="sxs-lookup"><span data-stu-id="193cf-198">c.</span></span> <span data-ttu-id="193cf-199">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="193cf-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="193cf-200">d.</span><span class="sxs-lookup"><span data-stu-id="193cf-200">d.</span></span> <span data-ttu-id="193cf-201">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="193cf-201">Click **Ok**</span></span>

10. <span data-ttu-id="193cf-202">Eseguire hello seguendo i passaggi hello **nome** - attributo</span><span class="sxs-lookup"><span data-stu-id="193cf-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="193cf-203">a.</span><span class="sxs-lookup"><span data-stu-id="193cf-203">a.</span></span> <span data-ttu-id="193cf-204">Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.</span><span class="sxs-lookup"><span data-stu-id="193cf-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="193cf-206">b.</span><span class="sxs-lookup"><span data-stu-id="193cf-206">b.</span></span> <span data-ttu-id="193cf-207">Eliminare il valore di URL hello dalla hello **dello spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="193cf-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="193cf-208">c.</span><span class="sxs-lookup"><span data-stu-id="193cf-208">c.</span></span> <span data-ttu-id="193cf-209">Fare clic su **Ok** impostazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="193cf-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="193cf-210">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="193cf-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="193cf-212">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="193cf-212">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="193cf-214">Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione.</span><span class="sxs-lookup"><span data-stu-id="193cf-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="193cf-215">File XML di hello caricamento è stato scaricato dal portale di Azure hello facendo hello **file caricare XML** opzione.</span><span class="sxs-lookup"><span data-stu-id="193cf-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="193cf-217">Fare clic su **su** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="193cf-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="193cf-218">Modifica stato SSO da **non connesso** troppo**connesso**</span><span class="sxs-lookup"><span data-stu-id="193cf-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="193cf-220">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="193cf-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="193cf-221">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="193cf-222">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="193cf-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="193cf-223">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="193cf-224">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="193cf-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="193cf-226">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="193cf-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="193cf-227">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="193cf-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="193cf-229">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="193cf-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="193cf-231">Fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="193cf-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="193cf-233">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="193cf-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="193cf-235">a.</span><span class="sxs-lookup"><span data-stu-id="193cf-235">a.</span></span> <span data-ttu-id="193cf-236">In hello **nome** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="193cf-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="193cf-237">b.</span><span class="sxs-lookup"><span data-stu-id="193cf-237">b.</span></span> <span data-ttu-id="193cf-238">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="193cf-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="193cf-239">c.</span><span class="sxs-lookup"><span data-stu-id="193cf-239">c.</span></span> <span data-ttu-id="193cf-240">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="193cf-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="193cf-241">d.</span><span class="sxs-lookup"><span data-stu-id="193cf-241">d.</span></span> <span data-ttu-id="193cf-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="193cf-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="193cf-243">Creazione di un utente test di LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="193cf-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="193cf-244">Applicazione di ricerca collegato supporta immediatamente in il provisioning dell'utente di tempo (JIT) e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="193cf-245">Attivare **automaticamente assegnare licenze** tooassign un utente toohello di licenza.</span><span class="sxs-lookup"><span data-stu-id="193cf-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="193cf-247">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="193cf-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="193cf-248">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLinkedIn ricerca.</span><span class="sxs-lookup"><span data-stu-id="193cf-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Assegna utente][200] 

<span data-ttu-id="193cf-250">**tooassign Britta Simon tooLinkedIn ricerca, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="193cf-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="193cf-251">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="193cf-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="193cf-253">Nell'elenco di applicazioni hello, selezionare **LinkedIn ricerca**.</span><span class="sxs-lookup"><span data-stu-id="193cf-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="193cf-255">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="193cf-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="193cf-257">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="193cf-257">Click **Add** button.</span></span> <span data-ttu-id="193cf-258">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="193cf-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="193cf-260">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="193cf-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="193cf-261">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="193cf-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="193cf-262">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="193cf-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="193cf-263">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="193cf-263">Testing single sign-on</span></span>

<span data-ttu-id="193cf-264">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="193cf-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="193cf-265">Quando si fa clic hello LinkedIn ricerca riquadro in hello Pannello di accesso, dovrebbe essere reindirizzato tooOrganizational pagina in cui occorre tooprovide i dettagli dell'account personali LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="193cf-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="193cf-266">In questo modo l'account personale viene collegato all'account aziendale di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="193cf-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="193cf-267">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="193cf-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="193cf-268">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="193cf-268">Additional resources</span></span>

* [<span data-ttu-id="193cf-269">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="193cf-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="193cf-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="193cf-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

