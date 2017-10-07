---
title: 'Esercitazione: Integrazione di Azure Active Directory con BC in hello Cloud | Documenti Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BC in hello Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="9eb1d-103">Esercitazione: Integrazione di Azure Active Directory con BC in hello Cloud</span><span class="sxs-lookup"><span data-stu-id="9eb1d-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="9eb1d-104">In questa esercitazione viene illustrato come toointegrate BC in hello Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9eb1d-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9eb1d-105">L'integrazione BC in hello Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9eb1d-106">È possibile controllare in Azure AD che dispongono dell'accesso tooBC hello Cloud</span><span class="sxs-lookup"><span data-stu-id="9eb1d-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="9eb1d-107">È possibile abilitare l'utenti tooautomatically get connesso tooBC in hello Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9eb1d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9eb1d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9eb1d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9eb1d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eb1d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9eb1d-110">Prerequisites</span></span>

<span data-ttu-id="9eb1d-111">integrazione di Azure AD con BC in hello Cloud tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="9eb1d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9eb1d-113">Un BC in hello single sign-Cloud nella sottoscrizione abilitata</span><span class="sxs-lookup"><span data-stu-id="9eb1d-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9eb1d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9eb1d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9eb1d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9eb1d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9eb1d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9eb1d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9eb1d-118">Scenario description</span></span>
<span data-ttu-id="9eb1d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9eb1d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9eb1d-121">Aggiunta di hello Cloud dalla raccolta hello BC</span><span class="sxs-lookup"><span data-stu-id="9eb1d-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="9eb1d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="9eb1d-123">Aggiunta di hello Cloud dalla raccolta hello BC</span><span class="sxs-lookup"><span data-stu-id="9eb1d-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="9eb1d-124">integrazione di hello tooconfigure di BC in hello Cloud in Azure AD, è necessario tooadd BC in hello Cloud dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9eb1d-125">**tooadd BC in hello Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9eb1d-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb1d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9eb1d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9eb1d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9eb1d-131">tooadd nuova applicazione, fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9eb1d-133">Nella casella di ricerca hello, digitare **BC in hello Cloud**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="9eb1d-135">Nel riquadro dei risultati hello, selezionare **BC in hello Cloud**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9eb1d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9eb1d-138">In questa sezione, configurare e testare Azure AD single sign-on con BC in hello che cloud basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9eb1d-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9eb1d-139">Per toowork di accesso singolo, Azure AD deve tooknow quali hello utente controparte BC in hello Cloud è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="9eb1d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello BC in hello Cloud deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="9eb1d-141">In BC in hello Cloud, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9eb1d-142">tooconfigure e prova AD Azure single sign-on con BC in hello Cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9eb1d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9eb1d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9eb1d-145">**[Creazione di un BC in utente di prova hello Cloud](#creating-a-bc-in-the-cloud-test-user)**  -toohave un equivalente di Britta Simon in BC in hello Cloud che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9eb1d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9eb1d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9eb1d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9eb1d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in il BC in un'applicazione hello Cloud.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="9eb1d-150">**Azure AD tooconfigure single sign-on con BC in hello Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9eb1d-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb1d-151">Nel portale di Azure su hello hello **BC in hello Cloud** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9eb1d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="9eb1d-155">In hello **BC hello dominio Cloud e URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="9eb1d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-157">a.</span></span> <span data-ttu-id="9eb1d-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="9eb1d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="9eb1d-159">b.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-159">b.</span></span> <span data-ttu-id="9eb1d-160">In hello **identificatore** casella di testo, digitare un URL come:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="9eb1d-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9eb1d-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="9eb1d-161">This value is not real.</span></span> <span data-ttu-id="9eb1d-162">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9eb1d-163">Contatto [BC nel team di supporto Cloud Client hello](https://www.bcinthecloud.com/supportcenter/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="9eb1d-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="9eb1d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9eb1d-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9eb1d-168">tooconfigure single sign-on sul **BC in hello Cloud** lato, è necessario hello toosend scaricato **Metadata XML** troppo[BC nel team di supporto Cloud hello](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="9eb1d-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="9eb1d-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="9eb1d-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9eb1d-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9eb1d-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9eb1d-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9eb1d-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9eb1d-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9eb1d-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9eb1d-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb1d-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9eb1d-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9eb1d-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9eb1d-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9eb1d-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9eb1d-184">a.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-184">a.</span></span> <span data-ttu-id="9eb1d-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9eb1d-186">b.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-186">b.</span></span> <span data-ttu-id="9eb1d-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9eb1d-188">c.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-188">c.</span></span> <span data-ttu-id="9eb1d-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9eb1d-190">d.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-190">d.</span></span> <span data-ttu-id="9eb1d-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="9eb1d-192">Creazione di un BC in utente di prova hello Cloud</span><span class="sxs-lookup"><span data-stu-id="9eb1d-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="9eb1d-193">In questa sezione si crea un utente denominato Britta Simon in BC in hello Cloud.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="9eb1d-194">Lavorare con [BC nel team di supporto Cloud Client hello](https://www.bcinthecloud.com/supportcenter/) per aggiungere utenti hello Ciao BC hello applicazione Cloud.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="9eb1d-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9eb1d-196">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb1d-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9eb1d-197">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBC in hello Cloud.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9eb1d-199">**tooassign tooBC Britta Simon in hello Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9eb1d-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb1d-200">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9eb1d-202">Nell'elenco di applicazioni hello, selezionare **BC in hello Cloud**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="9eb1d-204">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9eb1d-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-206">Click **Add** button.</span></span> <span data-ttu-id="9eb1d-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9eb1d-209">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9eb1d-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9eb1d-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9eb1d-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9eb1d-212">Testing single sign-on</span></span>

<span data-ttu-id="9eb1d-213">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="9eb1d-214">Quando si fa clic hello BC nel riquadro di Cloud hello in hello Pannello di accesso, viene visualizzato automaticamente firmato in tooyour BC hello applicazione Cloud.</span><span class="sxs-lookup"><span data-stu-id="9eb1d-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="9eb1d-215">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9eb1d-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9eb1d-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9eb1d-216">Additional resources</span></span>

* [<span data-ttu-id="9eb1d-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eb1d-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9eb1d-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eb1d-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

