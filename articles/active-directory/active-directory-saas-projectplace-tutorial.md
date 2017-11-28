---
title: 'Esercitazione: Integrazione di Azure Active Directory con Projectplace | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Projectplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="e824e-103">Esercitazione: Integrazione di Azure Active Directory con Projectplace</span><span class="sxs-lookup"><span data-stu-id="e824e-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="e824e-104">In questa esercitazione, è illustrato come toointegrate Projectplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e824e-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e824e-105">Integrazione di Projectplace con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e824e-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e824e-106">È possibile controllare in Azure AD che ha accesso tooProjectplace</span><span class="sxs-lookup"><span data-stu-id="e824e-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="e824e-107">È possibile abilitare l'utenti tooautomatically get connesso tooProjectplace (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e824e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e824e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e824e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e824e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e824e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e824e-110">Prerequisites</span></span>

<span data-ttu-id="e824e-111">integrazione di Azure AD con Projectplace tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e824e-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="e824e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e824e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e824e-113">Sottoscrizione di Projectplace abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e824e-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e824e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e824e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e824e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e824e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e824e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e824e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e824e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e824e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e824e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e824e-118">Scenario description</span></span>
<span data-ttu-id="e824e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e824e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e824e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e824e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e824e-121">Aggiunta di Projectplace dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e824e-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="e824e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="e824e-123">Aggiunta di Projectplace dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e824e-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="e824e-124">integrazione hello tooconfigure di Projectplace in Azure AD, è necessario tooadd Projectplace dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e824e-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e824e-125">**tooadd Projectplace dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e824e-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e824e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e824e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e824e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e824e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e824e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e824e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e824e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e824e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e824e-133">Nella casella di ricerca hello, digitare **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="e824e-133">In hello search box, type **Projectplace**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="e824e-135">Nel riquadro dei risultati hello, selezionare **Projectplace**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e824e-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e824e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e824e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Projectplace usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e824e-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e824e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Projectplace è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e824e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="e824e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Projectplace deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e824e-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="e824e-141">In Projectplace, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e824e-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e824e-142">tooconfigure e prova AD Azure single sign-on con Projectplace, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e824e-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e824e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e824e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e824e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e824e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e824e-145">**[Creazione di un utente test Projectplace](#creating-a-projectplace-test-user)**  -toohave un equivalente di Britta Simon in Projectplace che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e824e-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e824e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e824e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e824e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e824e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e824e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e824e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Projectplace.</span><span class="sxs-lookup"><span data-stu-id="e824e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="e824e-150">**Azure AD tooconfigure single sign-on con Projectplace, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e824e-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="e824e-151">Nel portale di Azure su hello hello **Projectplace** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e824e-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e824e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e824e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="e824e-155">In hello **Projectplace dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e824e-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="e824e-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="e824e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e824e-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="e824e-158">This value is not real.</span></span> <span data-ttu-id="e824e-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e824e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e824e-160">Contatto [team di supporto Client di Projectplace](https://success.planview.com/Projectplace/Support) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="e824e-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="e824e-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="e824e-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="e824e-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e824e-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e824e-165">tooconfigure single sign-on sul **Projectplace** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="e824e-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="e824e-166">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="e824e-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="e824e-167">configurazione Hello single sign-on è eseguita da hello toobe [team di supporto di Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="e824e-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="e824e-168">Si riceverà una notifica non appena la configurazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e824e-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="e824e-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e824e-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e824e-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e824e-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e824e-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e824e-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e824e-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e824e-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e824e-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e824e-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e824e-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e824e-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e824e-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e824e-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e824e-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e824e-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e824e-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e824e-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e824e-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e824e-184">a.</span><span class="sxs-lookup"><span data-stu-id="e824e-184">a.</span></span> <span data-ttu-id="e824e-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e824e-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e824e-186">b.</span><span class="sxs-lookup"><span data-stu-id="e824e-186">b.</span></span> <span data-ttu-id="e824e-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e824e-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e824e-188">c.</span><span class="sxs-lookup"><span data-stu-id="e824e-188">c.</span></span> <span data-ttu-id="e824e-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e824e-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e824e-190">d.</span><span class="sxs-lookup"><span data-stu-id="e824e-190">d.</span></span> <span data-ttu-id="e824e-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e824e-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="e824e-192">Creazione di un utente di test di Projectplace</span><span class="sxs-lookup"><span data-stu-id="e824e-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="e824e-193">In ordine tooenable Azure AD utenti toolog a Projectplace, è necessario eseguirne il provisioning in Projectplace.</span><span class="sxs-lookup"><span data-stu-id="e824e-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="e824e-194">Nel caso di hello di Projectplace, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e824e-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="e824e-195">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e824e-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e824e-196">Accedi tooyour **Projectplace** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e824e-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="e824e-197">Andare troppo**persone**, quindi fare clic su **membri**.</span><span class="sxs-lookup"><span data-stu-id="e824e-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="e824e-198">![Persone](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="e824e-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="e824e-199">Fare clic su **Aggiungi membro**.</span><span class="sxs-lookup"><span data-stu-id="e824e-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="e824e-200">![Aggiungere membri](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Aggiungere membri")</span><span class="sxs-lookup"><span data-stu-id="e824e-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="e824e-201">In hello **Add Member** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e824e-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e824e-202">![Nuovi membri](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Nuovi membri")</span><span class="sxs-lookup"><span data-stu-id="e824e-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="e824e-203">a.</span><span class="sxs-lookup"><span data-stu-id="e824e-203">a.</span></span> <span data-ttu-id="e824e-204">In hello **nuovi membri** casella di testo, digitare hello di indirizzo di posta elettronica di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="e824e-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="e824e-205">b.</span><span class="sxs-lookup"><span data-stu-id="e824e-205">b.</span></span> <span data-ttu-id="e824e-206">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="e824e-206">Click **Send**.</span></span>

   <span data-ttu-id="e824e-207">Tra cui un account di hello tooconfirm collegamento prima che diventi attivo tramite posta elettronica viene inviato toohello titolare dell'account di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e824e-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="e824e-208">È possibile usare qualsiasi altro Projectplace utente account strumento di creazione o le API fornite da Projectplace tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="e824e-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e824e-209">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e824e-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e824e-210">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooProjectplace.</span><span class="sxs-lookup"><span data-stu-id="e824e-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e824e-212">**tooassign Britta Simon tooProjectplace, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e824e-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="e824e-213">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e824e-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e824e-215">Nell'elenco di applicazioni hello, selezionare **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="e824e-215">In hello applications list, select **Projectplace**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="e824e-217">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e824e-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e824e-219">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e824e-219">Click **Add** button.</span></span> <span data-ttu-id="e824e-220">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e824e-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e824e-222">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e824e-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e824e-223">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e824e-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e824e-224">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e824e-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e824e-225">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e824e-225">Testing single sign-on</span></span>

<span data-ttu-id="e824e-226">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e824e-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e824e-227">Quando si fa clic su riquadro Projectplace hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Projectplace applicazione.</span><span class="sxs-lookup"><span data-stu-id="e824e-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="e824e-228">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e824e-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e824e-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e824e-229">Additional resources</span></span>

* [<span data-ttu-id="e824e-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e824e-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e824e-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e824e-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

