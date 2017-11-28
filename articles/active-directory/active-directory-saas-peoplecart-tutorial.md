---
title: 'Esercitazione: Integrazione di Azure Active Directory con Peoplecart | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Peoplecart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 481c7246a63f669ab39cb4ec652cebf40ba35f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="9c0be-103">Esercitazione: integrazione di Azure Active Directory con Peoplecart</span><span class="sxs-lookup"><span data-stu-id="9c0be-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="9c0be-104">In questa esercitazione, è illustrato come toointegrate Peoplecart con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c0be-104">In this tutorial, you learn how toointegrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c0be-105">Integrazione Peoplecart con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9c0be-105">Integrating Peoplecart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9c0be-106">È possibile controllare in Azure AD che ha accesso tooPeoplecart</span><span class="sxs-lookup"><span data-stu-id="9c0be-106">You can control in Azure AD who has access tooPeoplecart</span></span>
- <span data-ttu-id="9c0be-107">È possibile abilitare l'utenti tooautomatically get connesso tooPeoplecart (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-107">You can enable your users tooautomatically get signed-on tooPeoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9c0be-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9c0be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9c0be-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c0be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c0be-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c0be-110">Prerequisites</span></span>

<span data-ttu-id="9c0be-111">integrazione di Azure AD con Peoplecart tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9c0be-111">tooconfigure Azure AD integration with Peoplecart, you need hello following items:</span></span>

- <span data-ttu-id="9c0be-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c0be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c0be-113">Sottoscrizione di Peoplecart abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9c0be-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c0be-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9c0be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c0be-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9c0be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c0be-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9c0be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c0be-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c0be-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c0be-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9c0be-118">Scenario description</span></span>
<span data-ttu-id="9c0be-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9c0be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c0be-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9c0be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c0be-121">Aggiunta di Peoplecart dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9c0be-121">Adding Peoplecart from hello gallery</span></span>
2. <span data-ttu-id="9c0be-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-hello-gallery"></a><span data-ttu-id="9c0be-123">Aggiunta di Peoplecart dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9c0be-123">Adding Peoplecart from hello gallery</span></span>
<span data-ttu-id="9c0be-124">integrazione hello tooconfigure di Peoplecart in Azure AD, è necessario tooadd Peoplecart dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9c0be-124">tooconfigure hello integration of Peoplecart into Azure AD, you need tooadd Peoplecart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9c0be-125">**tooadd Peoplecart dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9c0be-125">**tooadd Peoplecart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c0be-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9c0be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="9c0be-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9c0be-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="9c0be-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9c0be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="9c0be-133">Nella casella di ricerca hello, digitare **Peoplecart**selezionare **Peoplecart** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9c0be-133">In hello search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9c0be-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9c0be-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Peoplecart in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9c0be-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9c0be-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Peoplecart è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c0be-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Peoplecart is tooa user in Azure AD.</span></span> <span data-ttu-id="9c0be-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Peoplecart deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9c0be-138">In other words, a link relationship between an Azure AD user and hello related user in Peoplecart needs toobe established.</span></span>

<span data-ttu-id="9c0be-139">In Peoplecart, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="9c0be-139">In Peoplecart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9c0be-140">tooconfigure e prova AD Azure single sign-on con Peoplecart, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9c0be-140">tooconfigure and test Azure AD single sign-on with Peoplecart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9c0be-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9c0be-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9c0be-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c0be-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c0be-143">**[Creare un utente test Peoplecart](#create-a-peoplecart-test-user)**  -toohave un equivalente di Britta Simon in Peoplecart che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9c0be-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - toohave a counterpart of Britta Simon in Peoplecart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c0be-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c0be-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c0be-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9c0be-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9c0be-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9c0be-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="9c0be-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="9c0be-148">**Azure AD tooconfigure single sign-on con Peoplecart, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9c0be-148">**tooconfigure Azure AD single sign-on with Peoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c0be-149">Nel portale di Azure su hello hello **Peoplecart** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-149">In hello Azure portal, on hello **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9c0be-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c0be-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="9c0be-153">In hello **Peoplecart dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c0be-153">On hello **Peoplecart Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="9c0be-155">a.</span><span class="sxs-lookup"><span data-stu-id="9c0be-155">a.</span></span> <span data-ttu-id="9c0be-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="9c0be-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="9c0be-157">b.</span><span class="sxs-lookup"><span data-stu-id="9c0be-157">b.</span></span> <span data-ttu-id="9c0be-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="9c0be-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c0be-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="9c0be-159">These values are not real.</span></span> <span data-ttu-id="9c0be-160">Aggiornare questi valori con hello URL effettivo Sign-On e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="9c0be-160">Update these values with hello actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="9c0be-161">Contatto [team di supporto Peoplecart Client](https://peoplecart.com/ContactUs.aspx) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="9c0be-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) tooget these values.</span></span> 
 
4. <span data-ttu-id="9c0be-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9c0be-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="9c0be-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9c0be-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9c0be-166">In hello **Peoplecart configurazione** fare clic su **configurare Peoplecart** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="9c0be-166">On hello **Peoplecart Configuration** section, click **Configure Peoplecart** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9c0be-167">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="9c0be-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="9c0be-169">tooconfigure single sign-on sul **Peoplecart** lato, è necessario hello toosend scaricato **Metadata XML** e **SAML Single Sign-On Service URL** troppo[ Il team di supporto Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c0be-169">tooconfigure single sign-on on **Peoplecart** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="9c0be-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="9c0be-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9c0be-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="9c0be-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9c0be-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="9c0be-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9c0be-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c0be-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9c0be-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-174">Create an Azure AD test user</span></span>
<span data-ttu-id="9c0be-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9c0be-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="9c0be-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9c0be-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c0be-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9c0be-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9c0be-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9c0be-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9c0be-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9c0be-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c0be-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9c0be-186">a.</span><span class="sxs-lookup"><span data-stu-id="9c0be-186">a.</span></span> <span data-ttu-id="9c0be-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c0be-188">b.</span><span class="sxs-lookup"><span data-stu-id="9c0be-188">b.</span></span> <span data-ttu-id="9c0be-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9c0be-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9c0be-190">c.</span><span class="sxs-lookup"><span data-stu-id="9c0be-190">c.</span></span> <span data-ttu-id="9c0be-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9c0be-192">d.</span><span class="sxs-lookup"><span data-stu-id="9c0be-192">d.</span></span> <span data-ttu-id="9c0be-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="9c0be-194">Creare un utente test di Peoplecart</span><span class="sxs-lookup"><span data-stu-id="9c0be-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="9c0be-195">In questa sezione viene creato un utente chiamato Britta Simon in Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="9c0be-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="9c0be-196">Lavorare con [team di supporto Peoplecart](https://peoplecart.com/ContactUs.aspx) utenti hello tooadd nella piattaforma Peoplecart hello.</span><span class="sxs-lookup"><span data-stu-id="9c0be-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) tooadd hello users in hello Peoplecart platform.</span></span> <span data-ttu-id="9c0be-197">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9c0be-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9c0be-198">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c0be-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9c0be-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPeoplecart.</span><span class="sxs-lookup"><span data-stu-id="9c0be-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeoplecart.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="9c0be-201">**tooassign Britta Simon tooPeoplecart, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9c0be-201">**tooassign Britta Simon tooPeoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c0be-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9c0be-204">Nell'elenco di applicazioni hello, selezionare **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-204">In hello applications list, select **Peoplecart**.</span></span>

    ![collegamento Peoplecart Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="9c0be-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="9c0be-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-208">Click **Add** button.</span></span> <span data-ttu-id="9c0be-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="9c0be-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9c0be-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9c0be-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c0be-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9c0be-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9c0be-214">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9c0be-214">Test single sign-on</span></span>

<span data-ttu-id="9c0be-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9c0be-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9c0be-216">Quando si fa clic su riquadro Peoplecart hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="9c0be-216">When you click hello Peoplecart tile in hello Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="9c0be-217">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c0be-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c0be-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9c0be-218">Additional resources</span></span>

* [<span data-ttu-id="9c0be-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c0be-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c0be-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c0be-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

