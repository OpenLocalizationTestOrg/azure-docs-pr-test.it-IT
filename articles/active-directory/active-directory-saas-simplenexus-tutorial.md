---
title: 'Esercitazione: Integrazione di Azure Active Directory con SimpleNexus| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SimpleNexus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 89f455d8c551045ddfcbe7234e86b13dad1140a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="c5b05-103">Esercitazione: Integrazione di Azure Active Directory con SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="c5b05-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="c5b05-104">In questa esercitazione, è illustrato come toointegrate SimpleNexus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5b05-104">In this tutorial, you learn how toointegrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5b05-105">Integrazione di SimpleNexus con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c5b05-105">Integrating SimpleNexus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5b05-106">È possibile controllare in Azure AD che ha accesso tooSimpleNexus</span><span class="sxs-lookup"><span data-stu-id="c5b05-106">You can control in Azure AD who has access tooSimpleNexus</span></span>
- <span data-ttu-id="c5b05-107">È possibile abilitare l'utenti tooautomatically get connesso tooSimpleNexus (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-107">You can enable your users tooautomatically get signed-on tooSimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5b05-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5b05-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5b05-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5b05-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b05-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5b05-110">Prerequisites</span></span>

<span data-ttu-id="c5b05-111">integrazione di Azure AD con SimpleNexus tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c5b05-111">tooconfigure Azure AD integration with SimpleNexus, you need hello following items:</span></span>

- <span data-ttu-id="c5b05-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5b05-113">Sottoscrizione di SimpleNexus abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c5b05-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5b05-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c5b05-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5b05-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c5b05-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5b05-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c5b05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5b05-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5b05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5b05-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c5b05-118">Scenario description</span></span>
<span data-ttu-id="c5b05-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c5b05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5b05-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c5b05-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5b05-121">Aggiunta di SimpleNexus dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c5b05-121">Adding SimpleNexus from hello gallery</span></span>
2. <span data-ttu-id="c5b05-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-hello-gallery"></a><span data-ttu-id="c5b05-123">Aggiunta di SimpleNexus dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c5b05-123">Adding SimpleNexus from hello gallery</span></span>
<span data-ttu-id="c5b05-124">integrazione hello tooconfigure di SimpleNexus in Azure AD, è necessario tooadd SimpleNexus dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c5b05-124">tooconfigure hello integration of SimpleNexus into Azure AD, you need tooadd SimpleNexus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5b05-125">**tooadd SimpleNexus dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5b05-125">**tooadd SimpleNexus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b05-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c5b05-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5b05-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5b05-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c5b05-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c5b05-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c5b05-133">Nella casella di ricerca hello, digitare **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-133">In hello search box, type **SimpleNexus**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="c5b05-135">Nel riquadro dei risultati hello, selezionare **SimpleNexus**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5b05-135">In hello results panel, select **SimpleNexus**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5b05-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5b05-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SimpleNexus usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c5b05-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5b05-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SimpleNexus è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b05-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SimpleNexus is tooa user in Azure AD.</span></span> <span data-ttu-id="c5b05-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SimpleNexus deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c5b05-140">In other words, a link relationship between an Azure AD user and hello related user in SimpleNexus needs toobe established.</span></span>

<span data-ttu-id="c5b05-141">In SimpleNexus, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="c5b05-141">In SimpleNexus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5b05-142">tooconfigure e prova AD Azure single sign-on con SimpleNexus, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c5b05-142">tooconfigure and test Azure AD single sign-on with SimpleNexus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5b05-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c5b05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5b05-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5b05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5b05-145">**[Creazione di un utente test SimpleNexus](#creating-a-simplenexus-test-user)**  -toohave un equivalente di Britta Simon in SimpleNexus che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c5b05-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - toohave a counterpart of Britta Simon in SimpleNexus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5b05-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5b05-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5b05-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c5b05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5b05-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5b05-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="c5b05-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="c5b05-150">**Azure AD tooconfigure single sign-on con SimpleNexus, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5b05-150">**tooconfigure Azure AD single sign-on with SimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b05-151">Nel portale di Azure su hello hello **SimpleNexus** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-151">In hello Azure portal, on hello **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c5b05-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5b05-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="c5b05-155">In hello **SimpleNexus dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5b05-155">On hello **SimpleNexus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="c5b05-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5b05-157">a.</span></span> <span data-ttu-id="c5b05-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="c5b05-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="c5b05-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5b05-159">b.</span></span> <span data-ttu-id="c5b05-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c5b05-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5b05-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c5b05-161">These values are not real.</span></span> <span data-ttu-id="c5b05-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="c5b05-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5b05-163">Contatto [team di supporto di SimpleNexus Client](https://simplenexus.com/site/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c5b05-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="c5b05-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c5b05-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="c5b05-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c5b05-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5b05-168">tooconfigure single sign-on sul **SimpleNexus** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="c5b05-168">tooconfigure single sign-on on **SimpleNexus** side, you need toosend hello downloaded **Metadata XML** too[SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="c5b05-169">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c5b05-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c5b05-170">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c5b05-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5b05-171">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c5b05-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5b05-172">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5b05-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5b05-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5b05-174">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c5b05-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c5b05-176">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5b05-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b05-177">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c5b05-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5b05-179">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5b05-181">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c5b05-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5b05-183">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5b05-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5b05-185">a.</span><span class="sxs-lookup"><span data-stu-id="c5b05-185">a.</span></span> <span data-ttu-id="c5b05-186">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5b05-187">b.</span><span class="sxs-lookup"><span data-stu-id="c5b05-187">b.</span></span> <span data-ttu-id="c5b05-188">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5b05-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5b05-189">c.</span><span class="sxs-lookup"><span data-stu-id="c5b05-189">c.</span></span> <span data-ttu-id="c5b05-190">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5b05-191">d.</span><span class="sxs-lookup"><span data-stu-id="c5b05-191">d.</span></span> <span data-ttu-id="c5b05-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="c5b05-193">Creazione di un utente di test di SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="c5b05-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="c5b05-194">In ordine tooenable Azure AD utenti toolog in tooSimpleNexus, è necessario eseguirne il provisioning in SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="c5b05-194">In order tooenable Azure AD users toolog in tooSimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="c5b05-195">In hello caso di SimpleNexus, il provisioning è un'attività manuale eseguita dall'amministratore tenant hello.</span><span class="sxs-lookup"><span data-stu-id="c5b05-195">In hello case of SimpleNexus, provisioning is a manual task performed by hello tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="c5b05-196">È possibile usare qualsiasi altro SimpleNexus utente account strumento di creazione o le API fornite da SimpleNexus tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="c5b05-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5b05-197">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b05-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5b05-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="c5b05-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSimpleNexus.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c5b05-200">**tooassign Britta Simon tooSimpleNexus, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5b05-200">**tooassign Britta Simon tooSimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b05-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c5b05-203">Nell'elenco di applicazioni hello, selezionare **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-203">In hello applications list, select **SimpleNexus**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="c5b05-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c5b05-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-207">Click **Add** button.</span></span> <span data-ttu-id="c5b05-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c5b05-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c5b05-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5b05-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5b05-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c5b05-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5b05-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c5b05-213">Testing single sign-on</span></span>

<span data-ttu-id="c5b05-214">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c5b05-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5b05-215">Quando si fa clic hello SimpleNexus riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="c5b05-215">When you click hello SimpleNexus tile in hello Access Panel, you should get automatically signed-on tooyour SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5b05-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c5b05-216">Additional resources</span></span>

* [<span data-ttu-id="c5b05-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5b05-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5b05-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5b05-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

