---
title: 'Esercitazione: Integrazione di Azure Active Directory con 10,000ft Plans | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e 10.000 ft piani.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="4d998-103">Esercitazione: Integrazione di Azure Active Directory con 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="4d998-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="4d998-104">In questa esercitazione, è illustrato come toointegrate 10.000 ft prevede con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d998-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d998-105">Integrazione di 10.000 ft piani con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4d998-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d998-106">È possibile controllare in Azure AD che ha accesso too10, ft 000 piani</span><span class="sxs-lookup"><span data-stu-id="4d998-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="4d998-107">È possibile abilitare l'utenti tooautomatically get connesso too10, piani ft 000 (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d998-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4d998-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d998-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d998-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d998-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4d998-110">Prerequisites</span></span>

<span data-ttu-id="4d998-111">integrazione di Azure AD con piani di 10.000 ft tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4d998-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="4d998-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d998-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d998-113">Sottoscrizione di 10,000ft Plans abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4d998-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d998-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d998-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d998-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4d998-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d998-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4d998-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d998-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d998-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d998-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4d998-118">Scenario description</span></span>
<span data-ttu-id="4d998-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4d998-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d998-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4d998-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d998-121">Aggiunta di 10.000 ft piani di raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4d998-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="4d998-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="4d998-123">Aggiunta di 10.000 ft piani di raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4d998-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="4d998-124">integrazione hello tooconfigure di 10.000 ft piani in Azure AD, è necessario tooadd 10.000 ft piani dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4d998-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d998-125">**Piani di tooadd 10.000 ft dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4d998-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d998-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4d998-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d998-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4d998-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d998-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4d998-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4d998-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4d998-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4d998-133">Nella casella di ricerca hello, digitare **10.000 ft piani**.</span><span class="sxs-lookup"><span data-stu-id="4d998-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="4d998-135">Nel riquadro dei risultati hello, selezionare **10.000 ft piani**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4d998-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d998-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d998-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 10,000ft Plans usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d998-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d998-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nei piani di 10.000 ft è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d998-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="4d998-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in 10.000 ft piani deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4d998-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="4d998-141">Nei piani di 10.000 ft, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4d998-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d998-142">tooconfigure e prova AD Azure single sign-on con piani di 10.000 ft, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4d998-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d998-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4d998-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d998-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d998-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d998-145">**[Creazione di un 10.000 ft piani di test utente](#creating-a-10000ft-plans-test-user)**  -toohave un equivalente di Britta Simon in 10.000 ft piani che è collegato AD Azure toohello rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4d998-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d998-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4d998-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d998-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4d998-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d998-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d998-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione i piani di 10.000 ft.</span><span class="sxs-lookup"><span data-stu-id="4d998-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="4d998-150">**tooconfigure AD Azure single sign-on con piani di 10.000 ft, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4d998-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d998-151">Nel portale di Azure su hello hello **10.000 ft piani** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4d998-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4d998-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4d998-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="4d998-155">In hello **10.000 ft piani di dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4d998-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="4d998-157">a.</span><span class="sxs-lookup"><span data-stu-id="4d998-157">a.</span></span> <span data-ttu-id="4d998-158">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="4d998-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="4d998-159">b.</span><span class="sxs-lookup"><span data-stu-id="4d998-159">b.</span></span> <span data-ttu-id="4d998-160">In hello **identificatore** casella di testo, digitare l'URL hello:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4d998-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d998-161">valore per Hello **identificatore** è diversa se si dispone di un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4d998-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="4d998-162">Contatto [team di supporto di piani di 10.000 ft](https://www.10000ft.com/plans/support) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="4d998-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="4d998-163">In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4d998-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="4d998-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4d998-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d998-167">In hello **10.000 ft piani configurazione** fare clic su **configurare i piani di 10.000 ft** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4d998-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d998-168">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4d998-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="4d998-170">tooconfigure single sign-on sul **10.000 ft piani** lato, è necessario hello toosend scaricato **Certificate(Raw), Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[ team di supporto di piani di 10.000 ft](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="4d998-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="4d998-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4d998-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d998-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4d998-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d998-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d998-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d998-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d998-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4d998-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4d998-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4d998-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d998-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4d998-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d998-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4d998-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d998-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4d998-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d998-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4d998-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d998-186">a.</span><span class="sxs-lookup"><span data-stu-id="4d998-186">a.</span></span> <span data-ttu-id="4d998-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d998-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d998-188">b.</span><span class="sxs-lookup"><span data-stu-id="4d998-188">b.</span></span> <span data-ttu-id="4d998-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d998-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d998-190">c.</span><span class="sxs-lookup"><span data-stu-id="4d998-190">c.</span></span> <span data-ttu-id="4d998-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4d998-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d998-192">d.</span><span class="sxs-lookup"><span data-stu-id="4d998-192">d.</span></span> <span data-ttu-id="4d998-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4d998-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="4d998-194">Creazione di un utente test di 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="4d998-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="4d998-195">obiettivo di Hello di questa sezione è un utente denominato Britta Simon nei piani di 10.000 ft toocreate.</span><span class="sxs-lookup"><span data-stu-id="4d998-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="4d998-196">10,000ft Plans supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4d998-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4d998-197">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4d998-197">There is no action item for you in this section.</span></span> <span data-ttu-id="4d998-198">Se non esiste ancora, durante un tooaccess tentativo 10.000 ft piani viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="4d998-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d998-199">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto di piani di 10.000 ft](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="4d998-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d998-200">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d998-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d998-201">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso too10, ft 000 piani.</span><span class="sxs-lookup"><span data-stu-id="4d998-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4d998-203">**tooassign Britta Simon too10, piani di ft 000, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4d998-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d998-204">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4d998-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4d998-206">Nell'elenco di applicazioni hello, selezionare **10.000 ft piani**.</span><span class="sxs-lookup"><span data-stu-id="4d998-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="4d998-208">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4d998-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4d998-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4d998-210">Click **Add** button.</span></span> <span data-ttu-id="4d998-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4d998-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4d998-213">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4d998-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d998-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4d998-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d998-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4d998-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d998-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4d998-216">Testing single sign-on</span></span>

<span data-ttu-id="4d998-217">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4d998-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="4d998-218">Quando si fa clic hello 10.000 ft piani riquadro in hello Pannello di accesso, è necessario ottenere l'applicazione di piani di 10.000 ft tooyour automaticamente firmato in.</span><span class="sxs-lookup"><span data-stu-id="4d998-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="4d998-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4d998-219">Additional resources</span></span>

* [<span data-ttu-id="4d998-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d998-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d998-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d998-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

