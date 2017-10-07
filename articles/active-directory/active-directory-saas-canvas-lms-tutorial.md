---
title: 'Esercitazione: Integrazione di Azure Active Directory con Canvas LMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="e7646-103">Esercitazione: Integrazione di Azure Active Directory con Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="e7646-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="e7646-104">In questa esercitazione, è illustrato come area di disegno toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7646-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7646-105">Area di disegno di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e7646-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7646-106">È possibile controllare in Azure AD che ha accesso tooCanvas</span><span class="sxs-lookup"><span data-stu-id="e7646-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="e7646-107">È possibile abilitare l'utenti tooautomatically get connesso tooCanvas (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7646-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e7646-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7646-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7646-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7646-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e7646-110">Prerequisites</span></span>

<span data-ttu-id="e7646-111">integrazione di Azure AD con Canvas tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e7646-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="e7646-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7646-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7646-113">Sottoscrizione di Canvas abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7646-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7646-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e7646-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7646-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e7646-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7646-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e7646-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7646-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7646-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7646-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e7646-118">Scenario description</span></span>
<span data-ttu-id="e7646-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e7646-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7646-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e7646-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7646-121">Aggiunta area di disegno dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7646-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="e7646-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="e7646-123">Aggiunta area di disegno dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7646-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="e7646-124">integrazione hello tooconfigure dell'area di disegno in Azure AD, è necessario tooadd area di disegno da elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e7646-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7646-125">**tooadd Canvas dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7646-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7646-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7646-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7646-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e7646-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7646-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7646-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e7646-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e7646-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e7646-133">Nella casella di ricerca hello, digitare **area di disegno**.</span><span class="sxs-lookup"><span data-stu-id="e7646-133">In hello search box, type **Canvas**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="e7646-135">Nel riquadro dei risultati hello, selezionare **area di disegno**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e7646-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7646-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7646-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Canvas usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7646-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7646-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di disegno è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7646-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="e7646-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di disegno deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e7646-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="e7646-141">Nell'area di disegno, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e7646-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7646-142">tooconfigure e prova AD Azure single sign-on con area di disegno, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e7646-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7646-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7646-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7646-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7646-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7646-145">**[Creazione di un utente test Canvas](#creating-a-canvas-test-user)**  -toohave un equivalente di Britta Simon nell'area di disegno che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e7646-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7646-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7646-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7646-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7646-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7646-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7646-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione area di disegno.</span><span class="sxs-lookup"><span data-stu-id="e7646-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="e7646-150">**Azure AD tooconfigure single sign-on con area di disegno, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7646-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7646-151">Nel portale di Azure su hello hello **area di disegno** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e7646-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e7646-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7646-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="e7646-155">In hello **URL e area di disegno dominio** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7646-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="e7646-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7646-157">a.</span></span> <span data-ttu-id="e7646-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="e7646-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="e7646-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7646-159">b.</span></span> <span data-ttu-id="e7646-160">In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="e7646-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7646-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="e7646-161">These values are not real.</span></span> <span data-ttu-id="e7646-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="e7646-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e7646-163">Contatto [team di supporto Client di area di disegno](https://community.canvaslms.com/community/help) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="e7646-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="e7646-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="e7646-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="e7646-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e7646-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7646-168">In hello **configurazione Canvas** fare clic su **configurare Canvas** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="e7646-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7646-169">Hello copia **Modifica URL Password, Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e7646-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="e7646-171">In una finestra del web browser, accedere come amministratore nel sito della società Canvas di tooyour.</span><span class="sxs-lookup"><span data-stu-id="e7646-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="e7646-172">Andare troppo**corsi \> gli account gestiti \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e7646-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="e7646-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="e7646-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="e7646-174">Nel riquadro di spostamento hello hello sinistra, selezionare **autenticazione**, quindi fare clic su **Aggiungi nuova configurazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="e7646-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="e7646-175">![Autenticazione](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="e7646-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="e7646-176">Nella pagina di integrazione corrente hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7646-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e7646-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span><span class="sxs-lookup"><span data-stu-id="e7646-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="e7646-178">a.</span><span class="sxs-lookup"><span data-stu-id="e7646-178">a.</span></span> <span data-ttu-id="e7646-179">In **IdP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7646-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7646-180">b.</span><span class="sxs-lookup"><span data-stu-id="e7646-180">b.</span></span> <span data-ttu-id="e7646-181">In **Log On URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7646-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="e7646-182">c.</span><span class="sxs-lookup"><span data-stu-id="e7646-182">c.</span></span> <span data-ttu-id="e7646-183">In **Log Out URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7646-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7646-184">d.</span><span class="sxs-lookup"><span data-stu-id="e7646-184">d.</span></span> <span data-ttu-id="e7646-185">In **Change Password Link** casella di testo, hello Incolla valore **Modifica URL Password** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7646-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="e7646-186">e.</span><span class="sxs-lookup"><span data-stu-id="e7646-186">e.</span></span> <span data-ttu-id="e7646-187">In **Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7646-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="e7646-188">f.</span><span class="sxs-lookup"><span data-stu-id="e7646-188">f.</span></span> <span data-ttu-id="e7646-189">Da hello **accesso attributo** elenco, selezionare **NameID**.</span><span class="sxs-lookup"><span data-stu-id="e7646-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="e7646-190">g.</span><span class="sxs-lookup"><span data-stu-id="e7646-190">g.</span></span> <span data-ttu-id="e7646-191">Da hello **identificatore di formato** elenco, selezionare **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="e7646-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="e7646-192">h.</span><span class="sxs-lookup"><span data-stu-id="e7646-192">h.</span></span> <span data-ttu-id="e7646-193">Fare clic su **Save authentication settings**.</span><span class="sxs-lookup"><span data-stu-id="e7646-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="e7646-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e7646-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7646-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e7646-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7646-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7646-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7646-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7646-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e7646-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e7646-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7646-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7646-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7646-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7646-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e7646-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7646-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e7646-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7646-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7646-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7646-209">a.</span><span class="sxs-lookup"><span data-stu-id="e7646-209">a.</span></span> <span data-ttu-id="e7646-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7646-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7646-211">b.</span><span class="sxs-lookup"><span data-stu-id="e7646-211">b.</span></span> <span data-ttu-id="e7646-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7646-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7646-213">c.</span><span class="sxs-lookup"><span data-stu-id="e7646-213">c.</span></span> <span data-ttu-id="e7646-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7646-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7646-215">d.</span><span class="sxs-lookup"><span data-stu-id="e7646-215">d.</span></span> <span data-ttu-id="e7646-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e7646-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="e7646-217">Creazione di un utente di test di Canvas</span><span class="sxs-lookup"><span data-stu-id="e7646-217">Creating a Canvas test user</span></span>

<span data-ttu-id="e7646-218">toolog agli utenti di Azure AD tooenable in tooCanvas, è necessario eseguirne il provisioning in Canvas.</span><span class="sxs-lookup"><span data-stu-id="e7646-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="e7646-219">Nel caso di Canvas, il provisioning degli utenti è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e7646-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="e7646-220">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7646-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7646-221">Accedi tooyour **area di disegno** tenant.</span><span class="sxs-lookup"><span data-stu-id="e7646-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="e7646-222">Andare troppo**corsi \> gli account gestiti \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e7646-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="e7646-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="e7646-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="e7646-224">Fare clic su **Users**.</span><span class="sxs-lookup"><span data-stu-id="e7646-224">Click **Users**.</span></span>
   
   <span data-ttu-id="e7646-225">![Utenti](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="e7646-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="e7646-226">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="e7646-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="e7646-227">![Utenti](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="e7646-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="e7646-228">In hello Aggiungi una pagina della finestra di dialogo Nuovo utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7646-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7646-229">![Aggiungere un utente](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="e7646-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="e7646-230">a.</span><span class="sxs-lookup"><span data-stu-id="e7646-230">a.</span></span> <span data-ttu-id="e7646-231">In hello **nome completo** casella di testo, immettere il nome di hello dell'utente come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7646-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="e7646-232">b.</span><span class="sxs-lookup"><span data-stu-id="e7646-232">b.</span></span> <span data-ttu-id="e7646-233">In hello **posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e7646-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="e7646-234">c.</span><span class="sxs-lookup"><span data-stu-id="e7646-234">c.</span></span> <span data-ttu-id="e7646-235">In hello **accesso** casella di testo, immettere l'indirizzo di posta elettronica dell'utente hello Azure AD come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e7646-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="e7646-236">d.</span><span class="sxs-lookup"><span data-stu-id="e7646-236">d.</span></span> <span data-ttu-id="e7646-237">Selezionare **la creazione dell'account utente di hello posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="e7646-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="e7646-238">e.</span><span class="sxs-lookup"><span data-stu-id="e7646-238">e.</span></span> <span data-ttu-id="e7646-239">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="e7646-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="e7646-240">È possibile utilizzare qualsiasi altro area di disegno account strumento di creazione utente o le API fornite da Canvas tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="e7646-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7646-241">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7646-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7646-242">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCanvas.</span><span class="sxs-lookup"><span data-stu-id="e7646-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e7646-244">**tooassign Britta Simon tooCanvas, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7646-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7646-245">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7646-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e7646-247">Nell'elenco di applicazioni hello, selezionare **area di disegno**.</span><span class="sxs-lookup"><span data-stu-id="e7646-247">In hello applications list, select **Canvas**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="e7646-249">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7646-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e7646-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e7646-251">Click **Add** button.</span></span> <span data-ttu-id="e7646-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7646-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e7646-254">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e7646-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7646-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7646-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7646-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7646-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7646-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7646-257">Testing single sign-on</span></span>

<span data-ttu-id="e7646-258">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e7646-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7646-259">Quando si fa clic su riquadro area di disegno hello in hello Pannello di accesso, è necessario ottenere applicazione Canvas tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="e7646-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="e7646-260">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7646-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7646-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e7646-261">Additional resources</span></span>

* [<span data-ttu-id="e7646-262">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7646-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7646-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7646-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

