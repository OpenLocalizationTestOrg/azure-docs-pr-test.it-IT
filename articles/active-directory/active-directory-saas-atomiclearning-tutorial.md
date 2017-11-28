---
title: 'Esercitazione: Integrazione di Azure Active Directory con Atomic Learning | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento atomica.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 12d7c380dbe47899eb35486c5e2a6936e8fb8b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="455c0-103">Esercitazione: Integrazione di Azure Active Directory con Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="455c0-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="455c0-104">In questa esercitazione, è illustrato come toointegrate Learning atomica con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="455c0-104">In this tutorial, you learn how toointegrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="455c0-105">Integrazione di apprendimento atomica con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="455c0-105">Integrating Atomic Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="455c0-106">È possibile controllare in Azure AD che ha accesso tooAtomic di apprendimento</span><span class="sxs-lookup"><span data-stu-id="455c0-106">You can control in Azure AD who has access tooAtomic Learning</span></span>
- <span data-ttu-id="455c0-107">È possibile abilitare il get tooautomatically utenti connesso tooAtomic Learning (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-107">You can enable your users tooautomatically get signed-on tooAtomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="455c0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="455c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="455c0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="455c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="455c0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="455c0-110">Prerequisites</span></span>

<span data-ttu-id="455c0-111">tooconfigure integrazione di Azure AD con Learning atomico, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="455c0-111">tooconfigure Azure AD integration with Atomic Learning, you need hello following items:</span></span>

- <span data-ttu-id="455c0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="455c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="455c0-113">Sottoscrizione di Atomic Learning abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="455c0-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="455c0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="455c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="455c0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="455c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="455c0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="455c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="455c0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="455c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="455c0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="455c0-118">Scenario description</span></span>
<span data-ttu-id="455c0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="455c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="455c0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="455c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="455c0-121">Aggiunta di apprendimento atomica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="455c0-121">Adding Atomic Learning from hello gallery</span></span>
2. <span data-ttu-id="455c0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-hello-gallery"></a><span data-ttu-id="455c0-123">Aggiunta di apprendimento atomica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="455c0-123">Adding Atomic Learning from hello gallery</span></span>
<span data-ttu-id="455c0-124">integrazione hello tooconfigure di apprendimento atomica in Azure AD, è necessario tooadd Learning atomica dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="455c0-124">tooconfigure hello integration of Atomic Learning into Azure AD, you need tooadd Atomic Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="455c0-125">**tooadd atomica Learning dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="455c0-125">**tooadd Atomic Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="455c0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="455c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="455c0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="455c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="455c0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="455c0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="455c0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="455c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="455c0-133">Nella casella di ricerca hello, digitare **Learning atomica**.</span><span class="sxs-lookup"><span data-stu-id="455c0-133">In hello search box, type **Atomic Learning**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="455c0-135">Nel riquadro dei risultati hello, selezionare **Learning atomica**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="455c0-135">In hello results panel, select **Atomic Learning**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="455c0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="455c0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Atomic Learning in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="455c0-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="455c0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning Atomic è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="455c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atomic Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="455c0-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Learning atomica deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="455c0-140">In other words, a link relationship between an Azure AD user and hello related user in Atomic Learning needs toobe established.</span></span>

<span data-ttu-id="455c0-141">In Learning atomica, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-141">In Atomic Learning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="455c0-142">tooconfigure e test Azure AD single sign-on con Learning atomico, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="455c0-142">tooconfigure and test Azure AD single sign-on with Atomic Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="455c0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="455c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="455c0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="455c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="455c0-145">**[Creazione di un utente test Learning atomica](#creating-an-atomic-learning-test-user)**  -toohave un equivalente di Britta Simon atomica scoprire che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="455c0-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - toohave a counterpart of Britta Simon in Atomic Learning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="455c0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="455c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="455c0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="455c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="455c0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="455c0-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Learning atomica.</span><span class="sxs-lookup"><span data-stu-id="455c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="455c0-150">**Azure AD tooconfigure single sign-on con Learning atomica, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="455c0-150">**tooconfigure Azure AD single sign-on with Atomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="455c0-151">Nel portale di Azure su hello hello **Learning atomica** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="455c0-151">In hello Azure portal, on hello **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="455c0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="455c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="455c0-155">In hello **atomica Learning dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="455c0-155">On hello **Atomic Learning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="455c0-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="455c0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="455c0-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="455c0-158">This value is not real.</span></span> <span data-ttu-id="455c0-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="455c0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="455c0-160">Contatto [team di supporto Client Learning atomica](mailto:cs@atomiclearning.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="455c0-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="455c0-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="455c0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="455c0-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="455c0-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="455c0-165">tooconfigure single sign-on sul **Learning atomica** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di apprendimento atomica](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="455c0-165">tooconfigure single sign-on on **Atomic Learning** side, you need toosend hello downloaded **Metadata XML** too[Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="455c0-166">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="455c0-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="455c0-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="455c0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="455c0-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="455c0-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="455c0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="455c0-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="455c0-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="455c0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="455c0-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="455c0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="455c0-174">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="455c0-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="455c0-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="455c0-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="455c0-178">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="455c0-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="455c0-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="455c0-182">a.</span><span class="sxs-lookup"><span data-stu-id="455c0-182">a.</span></span> <span data-ttu-id="455c0-183">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="455c0-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="455c0-184">b.</span><span class="sxs-lookup"><span data-stu-id="455c0-184">b.</span></span> <span data-ttu-id="455c0-185">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="455c0-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="455c0-186">c.</span><span class="sxs-lookup"><span data-stu-id="455c0-186">c.</span></span> <span data-ttu-id="455c0-187">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="455c0-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="455c0-188">d.</span><span class="sxs-lookup"><span data-stu-id="455c0-188">d.</span></span> <span data-ttu-id="455c0-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="455c0-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="455c0-190">Creazione di un utente test di Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="455c0-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="455c0-191">In questa sezione viene creato un utente di nome Britta Simon in Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="455c0-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="455c0-192">Atomic Learning supporta il provisioning just-in-time, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="455c0-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="455c0-193">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="455c0-193">There is no action item for you in this section.</span></span> <span data-ttu-id="455c0-194">Se non esiste ancora con indirizzo di posta elettronica hello per utente hello, durante un tooaccess tentativo Learning Atomic è creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="455c0-194">A new user is created during an attempt tooaccess Atomic Learning if it doesn't exist yet using hello email address for hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="455c0-195">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="455c0-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="455c0-196">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso tooAtomic di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="455c0-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtomic Learning.</span></span>

![Assegna utente][200] 

<span data-ttu-id="455c0-198">**tooassign tooAtomic Britta Simon apprendimento, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="455c0-198">**tooassign Britta Simon tooAtomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="455c0-199">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="455c0-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="455c0-201">Nell'elenco di applicazioni hello, selezionare **Learning atomica**.</span><span class="sxs-lookup"><span data-stu-id="455c0-201">In hello applications list, select **Atomic Learning**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="455c0-203">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="455c0-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="455c0-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="455c0-205">Click **Add** button.</span></span> <span data-ttu-id="455c0-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="455c0-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="455c0-208">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="455c0-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="455c0-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="455c0-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="455c0-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="455c0-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="455c0-211">Testing single sign-on</span></span>

<span data-ttu-id="455c0-212">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="455c0-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="455c0-213">Quando si fa clic su riquadro Learning atomica hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Learning atomica.</span><span class="sxs-lookup"><span data-stu-id="455c0-213">When you click hello Atomic Learning tile in hello Access Panel, you should get automatically signed-on tooyour Atomic Learning application.</span></span>
<span data-ttu-id="455c0-214">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="455c0-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="455c0-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="455c0-215">Additional resources</span></span>

* [<span data-ttu-id="455c0-216">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="455c0-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="455c0-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="455c0-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

