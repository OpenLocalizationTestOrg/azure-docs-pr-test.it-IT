---
title: 'Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e CompetencyIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: c032884b092da85684e24e98f75371475e09322d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="eb6ce-103">Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="eb6ce-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="eb6ce-104">In questa esercitazione, è illustrato come toointegrate CompetencyIQ con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb6ce-104">In this tutorial, you learn how toointegrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb6ce-105">Integrazione CompetencyIQ con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-105">Integrating CompetencyIQ with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb6ce-106">È possibile controllare in Azure AD che ha accesso tooCompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="eb6ce-106">You can control in Azure AD who has access tooCompetencyIQ</span></span>
- <span data-ttu-id="eb6ce-107">È possibile abilitare l'utenti tooautomatically get connesso tooCompetencyIQ (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-107">You can enable your users tooautomatically get signed-on tooCompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb6ce-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb6ce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb6ce-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb6ce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb6ce-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eb6ce-110">Prerequisites</span></span>

<span data-ttu-id="eb6ce-111">integrazione di Azure AD con CompetencyIQ tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-111">tooconfigure Azure AD integration with CompetencyIQ, you need hello following items:</span></span>

- <span data-ttu-id="eb6ce-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb6ce-113">Sottoscrizione di CompetencyIQ abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb6ce-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb6ce-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb6ce-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb6ce-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb6ce-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb6ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb6ce-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="eb6ce-118">Scenario description</span></span>
<span data-ttu-id="eb6ce-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb6ce-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb6ce-121">Aggiunta di CompetencyIQ dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="eb6ce-121">Adding CompetencyIQ from hello gallery</span></span>
2. <span data-ttu-id="eb6ce-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-hello-gallery"></a><span data-ttu-id="eb6ce-123">Aggiunta di CompetencyIQ dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="eb6ce-123">Adding CompetencyIQ from hello gallery</span></span>
<span data-ttu-id="eb6ce-124">integrazione hello tooconfigure di CompetencyIQ in Azure AD, è necessario tooadd CompetencyIQ dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-124">tooconfigure hello integration of CompetencyIQ into Azure AD, you need tooadd CompetencyIQ from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb6ce-125">**tooadd CompetencyIQ dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb6ce-125">**tooadd CompetencyIQ from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb6ce-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb6ce-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb6ce-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="eb6ce-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="eb6ce-133">Nella casella di ricerca hello, digitare **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-133">In hello search box, type **CompetencyIQ**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="eb6ce-135">Nel riquadro dei risultati hello, selezionare **CompetencyIQ**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-135">In hello results panel, select **CompetencyIQ**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb6ce-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb6ce-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CompetencyIQ usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eb6ce-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb6ce-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in CompetencyIQ è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CompetencyIQ is tooa user in Azure AD.</span></span> <span data-ttu-id="eb6ce-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in CompetencyIQ deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-140">In other words, a link relationship between an Azure AD user and hello related user in CompetencyIQ needs toobe established.</span></span>

<span data-ttu-id="eb6ce-141">In CompetencyIQ, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-141">In CompetencyIQ, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb6ce-142">tooconfigure e prova AD Azure single sign-on con CompetencyIQ, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-142">tooconfigure and test Azure AD single sign-on with CompetencyIQ, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb6ce-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb6ce-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb6ce-145">**[Creazione di un utente test CompetencyIQ](#creating-a-competencyiq-test-user)**  -toohave un equivalente di Britta Simon in CompetencyIQ che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - toohave a counterpart of Britta Simon in CompetencyIQ that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb6ce-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb6ce-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb6ce-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb6ce-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="eb6ce-150">**Azure AD tooconfigure single sign-on con CompetencyIQ, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb6ce-150">**tooconfigure Azure AD single sign-on with CompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb6ce-151">Nel portale di Azure su hello hello **CompetencyIQ** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-151">In hello Azure portal, on hello **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="eb6ce-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="eb6ce-155">In hello **CompetencyIQ dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-155">On hello **CompetencyIQ Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="eb6ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-157">a.</span></span> <span data-ttu-id="eb6ce-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="eb6ce-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="eb6ce-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-159">b.</span></span> <span data-ttu-id="eb6ce-160">In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="eb6ce-160">In hello **Identifier** textbox, type hello URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb6ce-161">valore dell'URL Hello Sign-on è non reale pertanto aggiornare questa con URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-161">hello Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="eb6ce-162">Contatto [team di supporto CompetencyIQ Client](https://www.competencyiq.com/) tooget questo.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) tooget this.</span></span> 
 
4. <span data-ttu-id="eb6ce-163">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="eb6ce-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="eb6ce-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb6ce-167">In hello **CompetencyIQ configurazione** fare clic su **configurare CompetencyIQ** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-167">On hello **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb6ce-168">Hello copia **ID entità SAML**, e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="eb6ce-168">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="eb6ce-170">tooconfigure single sign-on sul **CompetencyIQ** lato, è necessario hello toosend scaricato **Metadata XML**, **ID entità SAML** e **SAML Single Sign-On URL del servizio** troppo[team di supporto CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="eb6ce-170">tooconfigure single sign-on on **CompetencyIQ** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="eb6ce-171">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eb6ce-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="eb6ce-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb6ce-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb6ce-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb6ce-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb6ce-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb6ce-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="eb6ce-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb6ce-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb6ce-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb6ce-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb6ce-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb6ce-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="eb6ce-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb6ce-187">a.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-187">a.</span></span> <span data-ttu-id="eb6ce-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb6ce-189">b.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-189">b.</span></span> <span data-ttu-id="eb6ce-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb6ce-191">c.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-191">c.</span></span> <span data-ttu-id="eb6ce-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb6ce-193">d.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-193">d.</span></span> <span data-ttu-id="eb6ce-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="eb6ce-195">Creazione di un utente di test di CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="eb6ce-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="eb6ce-196">toolog agli utenti di Azure AD tooenable in tooCompetencyIQ, è necessario eseguirne il provisioning in CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-196">tooenable Azure AD users toolog in tooCompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="eb6ce-197">Contatto [team di supporto CompetencyIQ](https://www.competencyiq.com/) toocreate gli utenti in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) toocreate users in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb6ce-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb6ce-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb6ce-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCompetencyIQ.</span></span>

![Assegna utente][200] 

<span data-ttu-id="eb6ce-201">**tooassign Britta Simon tooCompetencyIQ, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb6ce-201">**tooassign Britta Simon tooCompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb6ce-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="eb6ce-204">Nell'elenco di applicazioni hello, selezionare **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-204">In hello applications list, select **CompetencyIQ**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="eb6ce-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="eb6ce-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-208">Click **Add** button.</span></span> <span data-ttu-id="eb6ce-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="eb6ce-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb6ce-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb6ce-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb6ce-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb6ce-214">Testing single sign-on</span></span>

<span data-ttu-id="eb6ce-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb6ce-216">Quando si fa clic su riquadro CompetencyIQ hello in hello Pannello di accesso, dovrebbe ottenere automaticamente connessi a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eb6ce-216">When you click hello CompetencyIQ tile in hello Access Panel, you should get automatically logged into hello application.</span></span>
<span data-ttu-id="eb6ce-217">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb6ce-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb6ce-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eb6ce-218">Additional resources</span></span>

* [<span data-ttu-id="eb6ce-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb6ce-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb6ce-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb6ce-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

