---
title: 'Esercitazione: Integrazione di Azure Active Directory con Origami | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Origami.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="0a8b6-103">Esercitazione: Integrazione di Azure Active Directory con Origami</span><span class="sxs-lookup"><span data-stu-id="0a8b6-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="0a8b6-104">In questa esercitazione, è illustrato come toointegrate Origami con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a8b6-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a8b6-105">Integrazione Origami con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a8b6-106">È possibile controllare in Azure AD che ha accesso tooOrigami</span><span class="sxs-lookup"><span data-stu-id="0a8b6-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="0a8b6-107">È possibile abilitare l'utenti tooautomatically get connesso tooOrigami (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a8b6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0a8b6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a8b6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a8b6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a8b6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a8b6-110">Prerequisites</span></span>

<span data-ttu-id="0a8b6-111">integrazione di Azure AD con Origami tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="0a8b6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a8b6-113">Sottoscrizione di Origami abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a8b6-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a8b6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a8b6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a8b6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a8b6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a8b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a8b6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0a8b6-118">Scenario description</span></span>
<span data-ttu-id="0a8b6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a8b6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a8b6-121">Aggiunta di Origami dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0a8b6-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="0a8b6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="0a8b6-123">Aggiunta di Origami dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0a8b6-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="0a8b6-124">integrazione hello tooconfigure di Origami in Azure AD, è necessario tooadd Origami dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a8b6-125">**tooadd Origami dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a8b6-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a8b6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a8b6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a8b6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0a8b6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0a8b6-133">Nella casella di ricerca hello, digitare **Origami**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-133">In hello search box, type **Origami**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="0a8b6-135">Nel riquadro dei risultati hello, selezionare **Origami**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a8b6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a8b6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Origami con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a8b6-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a8b6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Origami è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="0a8b6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Origami deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="0a8b6-141">In Origami, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a8b6-142">tooconfigure e prova AD Azure single sign-on con Origami, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a8b6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a8b6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a8b6-145">**[Creazione di un utente test Origami](#creating-an-origami-test-user)**  -toohave un equivalente di Britta Simon in Origami che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a8b6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a8b6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a8b6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a8b6-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Origami.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="0a8b6-150">**Azure AD tooconfigure single sign-on con Origami, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a8b6-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a8b6-151">Nel portale di Azure su hello hello **Origami** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0a8b6-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="0a8b6-155">In hello **Origami dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="0a8b6-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0a8b6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a8b6-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-158">hello value is not real.</span></span> <span data-ttu-id="0a8b6-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0a8b6-160">Contatto [team di supporto Client Origami](https://wordpress.org/support/theme/origami) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="0a8b6-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="0a8b6-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0a8b6-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a8b6-165">In hello **configurazione Origami** fare clic su **configurare Origami** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a8b6-166">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0a8b6-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="0a8b6-168">Accedi toohello account Origami con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="0a8b6-169">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="0a8b6-171">Nella pagina della finestra di installazione su singolo segno hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="0a8b6-173">a.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-173">a.</span></span> <span data-ttu-id="0a8b6-174">Selezionare **Abilita Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="0a8b6-175">b.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-175">b.</span></span> <span data-ttu-id="0a8b6-176">In hello **pagina URL di accesso del Provider di identità** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a8b6-177">c.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-177">c.</span></span> <span data-ttu-id="0a8b6-178">In hello **URL pagina di disconnessione del Provider di identità** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a8b6-179">d.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-179">d.</span></span> <span data-ttu-id="0a8b6-180">Fare clic su **Sfoglia** certificato hello tooupload scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="0a8b6-181">e.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-181">e.</span></span> <span data-ttu-id="0a8b6-182">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0a8b6-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0a8b6-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a8b6-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a8b6-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a8b6-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a8b6-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a8b6-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0a8b6-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a8b6-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a8b6-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a8b6-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a8b6-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a8b6-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a8b6-198">a.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-198">a.</span></span> <span data-ttu-id="0a8b6-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a8b6-200">b.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-200">b.</span></span> <span data-ttu-id="0a8b6-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a8b6-202">c.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-202">c.</span></span> <span data-ttu-id="0a8b6-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a8b6-204">d.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-204">d.</span></span> <span data-ttu-id="0a8b6-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="0a8b6-206">Creazione di un utente test in Origami</span><span class="sxs-lookup"><span data-stu-id="0a8b6-206">Creating an Origami test user</span></span>

<span data-ttu-id="0a8b6-207">In questa sezione viene creato un utente di nome Britta Simon in Origami.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="0a8b6-208">Accedi toohello account Origami con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="0a8b6-209">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="0a8b6-211">In hello **utenti e sicurezza** finestra di dialogo, fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="0a8b6-213">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-213">Click **Add New User**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="0a8b6-215">Nella finestra di dialogo Aggiungi nuovo utente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a8b6-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="0a8b6-217">a.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-217">a.</span></span> <span data-ttu-id="0a8b6-218">In hello **nome utente** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="0a8b6-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="0a8b6-219">b.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-219">b.</span></span> <span data-ttu-id="0a8b6-220">In hello **Password** casella di testo, digitare una password.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="0a8b6-221">c.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-221">c.</span></span> <span data-ttu-id="0a8b6-222">In hello **Conferma Password** casella di testo, digitare nuovamente la password hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="0a8b6-223">d.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-223">d.</span></span> <span data-ttu-id="0a8b6-224">In hello **nome** casella di testo, immettere nome hello dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="0a8b6-225">e.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-225">e.</span></span> <span data-ttu-id="0a8b6-226">In hello **cognome** casella di testo immettere hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="0a8b6-227">f.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-227">f.</span></span> <span data-ttu-id="0a8b6-228">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-228">Click **Save**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="0a8b6-230">Assegnare **ruoli utente** e **accesso Client** toohello utente.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a8b6-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a8b6-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a8b6-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooOrigami.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0a8b6-235">**tooassign Britta Simon tooOrigami, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a8b6-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a8b6-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0a8b6-238">Nell'elenco di applicazioni hello, selezionare **Origami**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-238">In hello applications list, select **Origami**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="0a8b6-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0a8b6-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-242">Click **Add** button.</span></span> <span data-ttu-id="0a8b6-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0a8b6-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a8b6-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a8b6-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a8b6-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a8b6-248">Testing single sign-on</span></span>

<span data-ttu-id="0a8b6-249">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a8b6-250">Quando si fa clic su riquadro Origami hello in hello Pannello di accesso, è necessario ottenere applicazione Origami tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="0a8b6-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a8b6-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0a8b6-251">Additional resources</span></span>

* [<span data-ttu-id="0a8b6-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a8b6-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a8b6-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a8b6-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

