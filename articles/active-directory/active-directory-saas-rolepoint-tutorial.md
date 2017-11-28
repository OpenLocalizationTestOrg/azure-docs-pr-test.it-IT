---
title: 'Esercitazione: Integrazione di Azure Active Directory con RolePoint | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RolePoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="fdc9f-103">Esercitazione: Integrazione di Azure Active Directory con RolePoint</span><span class="sxs-lookup"><span data-stu-id="fdc9f-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="fdc9f-104">In questa esercitazione, è illustrato come toointegrate RolePoint con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdc9f-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdc9f-105">Integrazione RolePoint con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fdc9f-106">È possibile controllare in Azure AD che ha accesso tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="fdc9f-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="fdc9f-107">È possibile abilitare l'utenti tooautomatically get connesso tooRolePoint (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fdc9f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fdc9f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fdc9f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fdc9f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdc9f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fdc9f-110">Prerequisites</span></span>

<span data-ttu-id="fdc9f-111">integrazione di Azure AD con RolePoint tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="fdc9f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdc9f-113">Sottoscrizione di RolePoint abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fdc9f-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdc9f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdc9f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdc9f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fdc9f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdc9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdc9f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fdc9f-118">Scenario description</span></span>
<span data-ttu-id="fdc9f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdc9f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdc9f-121">Aggiunta di RolePoint dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fdc9f-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="fdc9f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="fdc9f-123">Aggiunta di RolePoint dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fdc9f-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="fdc9f-124">integrazione hello tooconfigure di RolePoint in Azure AD, è necessario tooadd RolePoint dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fdc9f-125">**tooadd RolePoint dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fdc9f-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc9f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fdc9f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fdc9f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fdc9f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fdc9f-133">Nella casella di ricerca hello, digitare **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-133">In hello search box, type **RolePoint**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="fdc9f-135">Nel riquadro dei risultati hello, selezionare **RolePoint**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fdc9f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fdc9f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RolePoint in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fdc9f-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fdc9f-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in RolePoint è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="fdc9f-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RolePoint deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="fdc9f-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="fdc9f-142">tooconfigure e prova AD Azure single sign-on con RolePoint, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fdc9f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fdc9f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdc9f-145">**[Creazione di un utente test RolePoint](#creating-a-rolepoint-test-user)**  -toohave un equivalente di Britta Simon in RolePoint che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fdc9f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdc9f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fdc9f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fdc9f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RolePoint.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="fdc9f-150">**Azure AD tooconfigure single sign-on con RolePoint, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fdc9f-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc9f-151">Nel portale di Azure su hello hello **RolePoint** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fdc9f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="fdc9f-155">In hello **RolePoint dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="fdc9f-157">a.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-157">a.</span></span> <span data-ttu-id="fdc9f-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="fdc9f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="fdc9f-159">b.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-159">b.</span></span> <span data-ttu-id="fdc9f-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="fdc9f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fdc9f-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-161">These values are not hello real.</span></span> <span data-ttu-id="fdc9f-162">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="fdc9f-163">In questo caso si consiglia di valore univoco di hello toouse della stringa in hello Identifier.Contact [team di supporto RolePoint](mailto:info@rolepoint.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="fdc9f-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="fdc9f-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fdc9f-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="fdc9f-168">tooconfigure single sign-on sul **RolePoint** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="fdc9f-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="fdc9f-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fdc9f-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fdc9f-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fdc9f-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fdc9f-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fdc9f-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="fdc9f-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fdc9f-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fdc9f-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc9f-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fdc9f-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fdc9f-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fdc9f-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fdc9f-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fdc9f-184">a.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-184">a.</span></span> <span data-ttu-id="fdc9f-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdc9f-186">b.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-186">b.</span></span> <span data-ttu-id="fdc9f-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fdc9f-188">c.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-188">c.</span></span> <span data-ttu-id="fdc9f-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fdc9f-190">d.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-190">d.</span></span> <span data-ttu-id="fdc9f-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="fdc9f-192">Creazione di un utente test di RolePoint</span><span class="sxs-lookup"><span data-stu-id="fdc9f-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="fdc9f-193">In questa sezione viene creato un utente chiamato Britta Simon in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="fdc9f-194">Lavorare con [team di supporto RolePoint](mailto:info@rolepoint.com) utenti hello tooadd nella piattaforma RolePoint hello.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fdc9f-195">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc9f-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fdc9f-196">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRolePoint.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fdc9f-198">**tooassign Britta Simon tooRolePoint, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fdc9f-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc9f-199">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fdc9f-201">Nell'elenco di applicazioni hello, selezionare **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-201">In hello applications list, select **RolePoint**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="fdc9f-203">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fdc9f-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-205">Click **Add** button.</span></span> <span data-ttu-id="fdc9f-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fdc9f-208">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fdc9f-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdc9f-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fdc9f-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fdc9f-211">Testing single sign-on</span></span>

<span data-ttu-id="fdc9f-212">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fdc9f-213">Quando si fa clic su riquadro RolePoint hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour RolePoint applicazione.</span><span class="sxs-lookup"><span data-stu-id="fdc9f-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fdc9f-214">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fdc9f-214">Additional resources</span></span>

* [<span data-ttu-id="fdc9f-215">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdc9f-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdc9f-216">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdc9f-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

