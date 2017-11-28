---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="6bdd8-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="6bdd8-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="6bdd8-104">In questa esercitazione, è illustrato come toointegrate Learning LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6bdd8-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6bdd8-105">Integrazione di apprendimento di LinkedIn con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6bdd8-106">È possibile controllare in Azure AD che ha accesso tooLinkedIn di apprendimento</span><span class="sxs-lookup"><span data-stu-id="6bdd8-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="6bdd8-107">È possibile abilitare il get tooautomatically utenti connesso tooLinkedIn Learning (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6bdd8-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bdd8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6bdd8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6bdd8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bdd8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6bdd8-110">Prerequisites</span></span>

<span data-ttu-id="6bdd8-111">integrazione di Azure AD con Learning LinkedIn tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="6bdd8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6bdd8-113">Sottoscrizione di LinkedIn Learning abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6bdd8-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6bdd8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6bdd8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6bdd8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6bdd8-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bdd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6bdd8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6bdd8-118">Scenario description</span></span>
<span data-ttu-id="6bdd8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6bdd8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6bdd8-121">Aggiunta di apprendimento LinkedIn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6bdd8-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="6bdd8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="6bdd8-123">Aggiunta di apprendimento LinkedIn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6bdd8-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="6bdd8-124">integrazione hello tooconfigure di LinkedIn apprendimento in Azure AD, è necessario tooadd LinkedIn Learning dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6bdd8-125">**tooadd Learning LinkedIn dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bdd8-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6bdd8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6bdd8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6bdd8-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6bdd8-133">Nella casella di ricerca hello, digitare **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="6bdd8-134">Dal riquadro dei risultati, fare clic su **LinkedIn Learning** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6bdd8-136">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6bdd8-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Learning in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6bdd8-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6bdd8-138">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning LinkedIn è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="6bdd8-139">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in LinkedIn Learning richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="6bdd8-140">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Learning LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="6bdd8-141">tooconfigure e prova AD Azure single sign-on con LinkedIn Learning, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6bdd8-142">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6bdd8-143">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6bdd8-144">**[Creazione di un utente test LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="6bdd8-145">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6bdd8-146">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6bdd8-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6bdd8-148">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Learning LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="6bdd8-149">**Azure AD tooconfigure single sign-on con Learning LinkedIn, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bdd8-150">Nel portale di Azure su hello hello **LinkedIn Learning** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6bdd8-152">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="6bdd8-154">In una finestra del web browser, tenant LinkedIn Learning tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="6bdd8-155">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="6bdd8-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="6bdd8-156">Selezionare inoltre **Learning - predefinito** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="6bdd8-158">Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="6bdd8-160">Nel portale di Azure in **LinkedIn Learning dominio e gli URL**, eseguire i passaggi se si desidera tooconfigure SSO hello in **avviata da IdP** modalità</span><span class="sxs-lookup"><span data-stu-id="6bdd8-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="6bdd8-162">a.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-162">a.</span></span> <span data-ttu-id="6bdd8-163">In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="6bdd8-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="6bdd8-164">b.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-164">b.</span></span> <span data-ttu-id="6bdd8-165">In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="6bdd8-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="6bdd8-166">Se si desidera tooconfigure SSO in **SP Initiated**, quindi fare clic su Mostra avanzate URL opzione di impostazione nella sezione di configurazione hello e configurare URL hello-sign-on con hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="6bdd8-168">L'applicazione di apprendimento LinkedIn prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="6bdd8-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="6bdd8-170">il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn Learning prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="6bdd8-171">A tale scopo è possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="6bdd8-173">In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="6bdd8-174">Hello utente necessita di attestazioni di quattro tooadd denominate **posta elettronica**, **reparto**, **firstname**, e **lastname** e il valore di hello è mappata a toobe **user.mail**, **Department**, **user.givenname**, e **user.surname** rispettivamente</span><span class="sxs-lookup"><span data-stu-id="6bdd8-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="6bdd8-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="6bdd8-175">Attribute Name</span></span> | <span data-ttu-id="6bdd8-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="6bdd8-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="6bdd8-177">email</span><span class="sxs-lookup"><span data-stu-id="6bdd8-177">email</span></span>| <span data-ttu-id="6bdd8-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="6bdd8-178">user.mail</span></span> |    
    | <span data-ttu-id="6bdd8-179">department</span><span class="sxs-lookup"><span data-stu-id="6bdd8-179">department</span></span>| <span data-ttu-id="6bdd8-180">user.department</span><span class="sxs-lookup"><span data-stu-id="6bdd8-180">user.department</span></span> |
    | <span data-ttu-id="6bdd8-181">firstname</span><span class="sxs-lookup"><span data-stu-id="6bdd8-181">firstname</span></span>| <span data-ttu-id="6bdd8-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6bdd8-182">user.givenname</span></span> |
    | <span data-ttu-id="6bdd8-183">lastname</span><span class="sxs-lookup"><span data-stu-id="6bdd8-183">lastname</span></span>| <span data-ttu-id="6bdd8-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="6bdd8-184">user.surname</span></span> |
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="6bdd8-186">a.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-186">a.</span></span> <span data-ttu-id="6bdd8-187">Fare clic su **Aggiungi attributo** tooopen finestra di dialogo attributo hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="6bdd8-190">b.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-190">b.</span></span> <span data-ttu-id="6bdd8-191">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6bdd8-192">c.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-192">c.</span></span> <span data-ttu-id="6bdd8-193">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6bdd8-194">d.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-194">d.</span></span> <span data-ttu-id="6bdd8-195">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-195">Click **Ok**</span></span>

10. <span data-ttu-id="6bdd8-196">Eseguire hello seguendo i passaggi hello **nome** - attributo</span><span class="sxs-lookup"><span data-stu-id="6bdd8-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="6bdd8-197">a.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-197">a.</span></span> <span data-ttu-id="6bdd8-198">Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="6bdd8-200">b.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-200">b.</span></span> <span data-ttu-id="6bdd8-201">Eliminare il valore di URL hello dalla hello **dello spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="6bdd8-202">c.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-202">c.</span></span> <span data-ttu-id="6bdd8-203">Fare clic su **Ok** impostazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="6bdd8-204">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="6bdd8-206">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-206">Click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="6bdd8-208">Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="6bdd8-209">Caricare file XML di hello che è stato scaricato dal portale di Azure hello facendo hello caricare XML file opzione.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="6bdd8-211">Fare clic su **su** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="6bdd8-212">Modifica stato SSO da **non connesso** troppo**connesso**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6bdd8-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="6bdd8-215">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6bdd8-217">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bdd8-218">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6bdd8-220">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6bdd8-222">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6bdd8-224">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6bdd8-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6bdd8-226">a.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-226">a.</span></span> <span data-ttu-id="6bdd8-227">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6bdd8-228">b.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-228">b.</span></span> <span data-ttu-id="6bdd8-229">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6bdd8-230">c.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-230">c.</span></span> <span data-ttu-id="6bdd8-231">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6bdd8-232">d.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-232">d.</span></span> <span data-ttu-id="6bdd8-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="6bdd8-234">Creare un utente test di LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="6bdd8-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="6bdd8-235">L'applicazione LinkedIn Learning supporta</span><span class="sxs-lookup"><span data-stu-id="6bdd8-235">Linked Learning Application supports.</span></span> <span data-ttu-id="6bdd8-236">Provisioning utente tempo Just-in e dopo l'autenticazione degli utenti vengono creati automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="6bdd8-237">Nella pagina Impostazioni di amministrazione hello interruttore portale hello capovolto LinkedIn Learning hello **automaticamente assegnare licenze** tooactive tooenable JIT in fase di provisioning e questo verrà assegnato un utente toohello di licenza.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6bdd8-239">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bdd8-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6bdd8-240">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso tooLinkedIn di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6bdd8-242">**tooassign tooLinkedIn Britta Simon apprendimento, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bdd8-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bdd8-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6bdd8-245">Nell'elenco di applicazioni hello, selezionare **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="6bdd8-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6bdd8-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-249">Click **Add** button.</span></span> <span data-ttu-id="6bdd8-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6bdd8-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6bdd8-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6bdd8-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6bdd8-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6bdd8-255">Testing single sign-on</span></span>

<span data-ttu-id="6bdd8-256">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6bdd8-257">Quando si fa clic su riquadro LinkedIn Learning hello in hello Pannello di accesso, è necessario ottenere una pagina di accesso Azure hello e su dopo l'esito positivo sign-on, viene visualizzato nell'applicazione Learning LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="6bdd8-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6bdd8-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6bdd8-258">Additional resources</span></span>

* [<span data-ttu-id="6bdd8-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bdd8-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6bdd8-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bdd8-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png