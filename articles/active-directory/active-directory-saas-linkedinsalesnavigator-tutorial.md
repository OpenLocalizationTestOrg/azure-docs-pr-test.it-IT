---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Sales Navigator | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LinkedInSalesNavigator.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="7e6c7-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="7e6c7-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="7e6c7-104">In questa esercitazione, è illustrato come toointegrate LinkedIn Sales Navigator con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e6c7-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e6c7-105">Integrazione di LinkedIn Sales Navigator con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e6c7-106">È possibile controllare in Azure AD che ha accesso tooLinkedIn Navigator vendite</span><span class="sxs-lookup"><span data-stu-id="7e6c7-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="7e6c7-107">È possibile abilitare l'utenti tooautomatically get connesso tooLinkedIn Navigator Sales (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e6c7-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7e6c7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e6c7-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, Sfoglia [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e6c7-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e6c7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e6c7-110">Prerequisites</span></span>

<span data-ttu-id="7e6c7-111">integrazione di Azure AD con LinkedIn Sales Navigator tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="7e6c7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e6c7-113">Sottoscrizione di LinkedIn Sales Navigator abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e6c7-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e6c7-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e6c7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e6c7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e6c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e6c7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7e6c7-118">Scenario description</span></span>
<span data-ttu-id="7e6c7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e6c7-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e6c7-121">Aggiunta di LinkedIn Sales Navigator dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7e6c7-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="7e6c7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="7e6c7-123">Aggiunta di LinkedIn Sales Navigator dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7e6c7-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="7e6c7-124">integrazione hello tooconfigure di LinkedIn Sales Navigator in Azure AD, è necessario tooadd LinkedIn Sales Navigator dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e6c7-125">**tooadd LinkedIn Sales Navigator dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e6c7-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e6c7-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e6c7-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7e6c7-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7e6c7-133">Nella casella di ricerca hello, digitare **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="7e6c7-135">Nel riquadro dei risultati hello, selezionare **LinkedIn Sales Navigator**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e6c7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e6c7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Sales Navigator in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e6c7-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e6c7-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nello strumento di navigazione di LinkedIn Sales è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="7e6c7-140">In altre parole, una relazione di collegamento tra un utente AD Azure e l'utente correlato di hello nello strumento di navigazione di LinkedIn Sales deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="7e6c7-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nello strumento di navigazione Sales LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="7e6c7-142">tooconfigure e prova AD Azure single sign-on con LinkedIn Sales Navigator, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e6c7-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e6c7-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e6c7-145">**[Creazione di un utente test LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)**  -toohave un equivalente di Britta Simon nello strumento di navigazione Sales LinkedIn che è la rappresentazione toohello collegato Azure AD dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="7e6c7-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e6c7-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e6c7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e6c7-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Navigator Sales LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="7e6c7-150">**tooconfigure Azure single sign-on AD Navigator Sales LinkedIn eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e6c7-151">Nel portale di Azure su hello hello **LinkedIn Sales Navigator** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7e6c7-153">In hello **Single sign-on** finestra di dialogo, nella **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="7e6c7-155">In una finestra del web browser, accesso tooyour **LinkedIn Sales Navigator** sito Web come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="7e6c7-156">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="7e6c7-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="7e6c7-157">Selezionare inoltre **Sales Navigator** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="7e6c7-159">Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="7e6c7-161">Nel portale di Azure in **LinkedIn Sales Navigator dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="7e6c7-163">a.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-163">a.</span></span> <span data-ttu-id="7e6c7-164">In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="7e6c7-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="7e6c7-165">b.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-165">b.</span></span> <span data-ttu-id="7e6c7-166">In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="7e6c7-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="7e6c7-167">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="7e6c7-169">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="7e6c7-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="7e6c7-170">Il **LinkedIn Sales Navigator** asserzioni SAML hello in un formato specifico, che richiede la configurazione di attributi del token SAML tooadd attributo personalizzato mapping tooyour prevista dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="7e6c7-171">Hello seguente schermata mostra un esempio.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="7e6c7-172">il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn Sales Navigator prevede che il mapping con indirizzo di posta elettronica dell'utente hello toobe.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="7e6c7-173">È possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="7e6c7-175">In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="7e6c7-176">Hello utente necessita di attestazioni di quattro tooadd denominate **posta elettronica**, **reparto**, **firstname**, e **lastname** e il valore di hello è mappata a toobe **user.mail**, **Department**, **user.givenname**, e **user.surname** rispettivamente</span><span class="sxs-lookup"><span data-stu-id="7e6c7-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="7e6c7-177">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7e6c7-177">Attribute Name</span></span> | <span data-ttu-id="7e6c7-178">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="7e6c7-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="7e6c7-179">email</span><span class="sxs-lookup"><span data-stu-id="7e6c7-179">email</span></span>| <span data-ttu-id="7e6c7-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="7e6c7-180">user.mail</span></span> |
    | <span data-ttu-id="7e6c7-181">department</span><span class="sxs-lookup"><span data-stu-id="7e6c7-181">department</span></span>| <span data-ttu-id="7e6c7-182">user.department</span><span class="sxs-lookup"><span data-stu-id="7e6c7-182">user.department</span></span> |
    | <span data-ttu-id="7e6c7-183">firstname</span><span class="sxs-lookup"><span data-stu-id="7e6c7-183">firstname</span></span>| <span data-ttu-id="7e6c7-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7e6c7-184">user.givenname</span></span> |
    | <span data-ttu-id="7e6c7-185">lastname</span><span class="sxs-lookup"><span data-stu-id="7e6c7-185">lastname</span></span>| <span data-ttu-id="7e6c7-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="7e6c7-186">user.surname</span></span> |
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="7e6c7-188">a.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-188">a.</span></span> <span data-ttu-id="7e6c7-189">Fare clic su **Aggiungi attributo** tooopen finestra di dialogo attributo hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="7e6c7-192">b.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-192">b.</span></span> <span data-ttu-id="7e6c7-193">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7e6c7-194">c.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-194">c.</span></span> <span data-ttu-id="7e6c7-195">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7e6c7-196">d.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-196">d.</span></span> <span data-ttu-id="7e6c7-197">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-197">Click **Ok**</span></span>

10. <span data-ttu-id="7e6c7-198">Eseguire hello seguendo i passaggi hello **nome** - attributo</span><span class="sxs-lookup"><span data-stu-id="7e6c7-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="7e6c7-199">a.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-199">a.</span></span> <span data-ttu-id="7e6c7-200">Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="7e6c7-202">b.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-202">b.</span></span> <span data-ttu-id="7e6c7-203">Eliminare il valore di URL hello dalla hello **dello spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="7e6c7-204">c.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-204">c.</span></span> <span data-ttu-id="7e6c7-205">Fare clic su **Ok** impostazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="7e6c7-206">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="7e6c7-208">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7e6c7-208">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="7e6c7-210">Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="7e6c7-211">Fare clic su **file caricare XML** hello tooupload file Metadata XML che è stato scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="7e6c7-213">Fare clic su **su** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="7e6c7-214">Modifica stato SSO da **non connesso** troppo**connesso**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="7e6c7-216">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="7e6c7-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e6c7-217">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e6c7-218">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e6c7-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e6c7-219">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e6c7-220">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7e6c7-222">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e6c7-223">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e6c7-225">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e6c7-227">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e6c7-229">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7e6c7-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e6c7-231">a.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-231">a.</span></span> <span data-ttu-id="7e6c7-232">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e6c7-233">b.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-233">b.</span></span> <span data-ttu-id="7e6c7-234">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e6c7-235">c.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-235">c.</span></span> <span data-ttu-id="7e6c7-236">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e6c7-237">d.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-237">d.</span></span> <span data-ttu-id="7e6c7-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="7e6c7-239">Creazione di un utente test di LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="7e6c7-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="7e6c7-240">Collegato Sales Navigator applicazione supporta solo per il provisioning utente ora (JIT) e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="7e6c7-241">Attivare **automaticamente assegnare licenze** tooassign un utente toohello di licenza.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7e6c7-243">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e6c7-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7e6c7-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLinkedIn Navigator Sales.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7e6c7-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e6c7-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e6c7-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7e6c7-249">Nell'elenco di applicazioni hello, selezionare **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="7e6c7-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7e6c7-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-253">Click **Add** button.</span></span> <span data-ttu-id="7e6c7-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7e6c7-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e6c7-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e6c7-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e6c7-259">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7e6c7-259">Testing single sign-on</span></span>

<span data-ttu-id="7e6c7-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e6c7-261">Quando si fa clic su riquadro LinkedIn Sales Navigator hello in hello Pannello di accesso, dovrebbe essere reindirizzato tooOrganizational pagina in cui occorre tooprovide i dettagli dell'account personali LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="7e6c7-262">In questo modo l'account personale viene collegato all'account aziendale di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7e6c7-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="7e6c7-263">Per ulteriori informazioni su hello Pannello di accesso, vedere [Introduzione al pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7e6c7-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e6c7-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7e6c7-264">Additional resources</span></span>

* [<span data-ttu-id="7e6c7-265">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e6c7-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e6c7-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e6c7-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

