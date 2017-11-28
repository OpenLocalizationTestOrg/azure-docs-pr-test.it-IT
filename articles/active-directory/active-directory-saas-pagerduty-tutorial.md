---
title: 'Esercitazione: Integrazione di Azure Active Directory con PagerDuty | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="4a314-103">Esercitazione: integrazione di Azure Active Directory con PagerDuty</span><span class="sxs-lookup"><span data-stu-id="4a314-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="4a314-104">In questa esercitazione, è illustrato come toointegrate PagerDuty con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a314-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a314-105">Integrazione PagerDuty con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4a314-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a314-106">È possibile controllare in Azure AD che ha accesso tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="4a314-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="4a314-107">È possibile abilitare l'utenti tooautomatically get connesso tooPagerDuty (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a314-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4a314-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a314-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a314-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a314-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4a314-110">Prerequisites</span></span>

<span data-ttu-id="4a314-111">integrazione di Azure AD con PagerDuty tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4a314-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="4a314-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a314-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a314-113">Sottoscrizione di PagerDuty abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4a314-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a314-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4a314-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a314-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4a314-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a314-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4a314-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a314-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a314-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a314-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4a314-118">Scenario description</span></span>
<span data-ttu-id="4a314-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4a314-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a314-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4a314-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a314-121">Aggiunta di PagerDuty dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4a314-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="4a314-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="4a314-123">Aggiunta di PagerDuty dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4a314-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="4a314-124">integrazione hello tooconfigure di PagerDuty in Azure AD, è necessario tooadd PagerDuty dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4a314-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a314-125">**tooadd PagerDuty dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4a314-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a314-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4a314-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="4a314-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4a314-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a314-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a314-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="4a314-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4a314-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="4a314-133">Nella casella di ricerca hello, digitare **PagerDuty**selezionare **PagerDuty** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a314-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4a314-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4a314-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PagerDuty in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a314-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a314-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PagerDuty è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a314-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="4a314-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PagerDuty deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4a314-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="4a314-139">In PagerDuty, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4a314-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4a314-140">tooconfigure e test Azure single sign-on AD con PagerDuty, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4a314-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a314-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a314-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a314-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a314-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a314-143">**[Creare un utente test PagerDuty](#create-a-pagerduty-test-user)**  -toohave un equivalente di Britta Simon in PagerDuty che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4a314-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a314-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a314-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a314-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4a314-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4a314-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4a314-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="4a314-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="4a314-148">**Azure AD tooconfigure single sign-on con PagerDuty, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4a314-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a314-149">Nel portale di Azure su hello hello **PagerDuty** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4a314-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="4a314-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a314-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="4a314-153">In hello **PagerDuty dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a314-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="4a314-155">a.</span><span class="sxs-lookup"><span data-stu-id="4a314-155">a.</span></span> <span data-ttu-id="4a314-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="4a314-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="4a314-157">b.</span><span class="sxs-lookup"><span data-stu-id="4a314-157">b.</span></span> <span data-ttu-id="4a314-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="4a314-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a314-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4a314-159">These values are not real.</span></span> <span data-ttu-id="4a314-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="4a314-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4a314-161">Contatto [team di supporto PagerDuty Client](https://www.pagerduty.com/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4a314-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="4a314-162">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4a314-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="4a314-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4a314-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a314-166">In hello **PagerDuty configurazione** fare clic su **configurare PagerDuty** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4a314-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4a314-167">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4a314-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="4a314-169">In un'altra finestra del Web browser accedere al sito aziendale di Pagerduty come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4a314-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="4a314-170">Scegliere dal menu hello in primo piano hello **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="4a314-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="4a314-171">![Impostazioni account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="4a314-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="4a314-172">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4a314-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="4a314-173">![Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a314-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="4a314-174">In hello **abilitare Single Sign-on (SSO)** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a314-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4a314-175">![Abilitare l'accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Abilitare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a314-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="4a314-176">a.</span><span class="sxs-lookup"><span data-stu-id="4a314-176">a.</span></span> <span data-ttu-id="4a314-177">Aprire il certificato con codifica base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo</span><span class="sxs-lookup"><span data-stu-id="4a314-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="4a314-178">b.</span><span class="sxs-lookup"><span data-stu-id="4a314-178">b.</span></span> <span data-ttu-id="4a314-179">In hello **URL di accesso** casella di testo, incollare **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a314-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="4a314-180">c.</span><span class="sxs-lookup"><span data-stu-id="4a314-180">c.</span></span> <span data-ttu-id="4a314-181">In hello **Logout URL** casella di testo, incollare **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a314-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="4a314-182">d.</span><span class="sxs-lookup"><span data-stu-id="4a314-182">d.</span></span> <span data-ttu-id="4a314-183">Selezionare **Attiva Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4a314-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="4a314-184">e.</span><span class="sxs-lookup"><span data-stu-id="4a314-184">e.</span></span> <span data-ttu-id="4a314-185">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="4a314-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4a314-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4a314-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4a314-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4a314-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4a314-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a314-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4a314-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-189">Create an Azure AD test user</span></span>

<span data-ttu-id="4a314-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a314-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="4a314-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4a314-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a314-193">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4a314-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a314-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4a314-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a314-197">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a314-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a314-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a314-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a314-201">a.</span><span class="sxs-lookup"><span data-stu-id="4a314-201">a.</span></span> <span data-ttu-id="4a314-202">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a314-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a314-203">b.</span><span class="sxs-lookup"><span data-stu-id="4a314-203">b.</span></span> <span data-ttu-id="4a314-204">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a314-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a314-205">c.</span><span class="sxs-lookup"><span data-stu-id="4a314-205">c.</span></span> <span data-ttu-id="4a314-206">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4a314-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a314-207">d.</span><span class="sxs-lookup"><span data-stu-id="4a314-207">d.</span></span> <span data-ttu-id="4a314-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4a314-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="4a314-209">Creare un utente test PagerDuty</span><span class="sxs-lookup"><span data-stu-id="4a314-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="4a314-210">toolog agli utenti di Azure AD tooenable in tooPagerDuty, è necessario eseguirne il provisioning in PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="4a314-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="4a314-211">Nel caso di hello di PagerDuty, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4a314-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="4a314-212">È possibile usare qualsiasi altro Pagerduty utente account strumento di creazione o le API fornite da Pagerduty tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="4a314-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="4a314-213">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4a314-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a314-214">Accedi tooyour **Pagerduty** tenant.</span><span class="sxs-lookup"><span data-stu-id="4a314-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="4a314-215">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="4a314-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="4a314-216">Fare clic su **Aggiungi utenti**.</span><span class="sxs-lookup"><span data-stu-id="4a314-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="4a314-217">![Aggiungere utenti](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="4a314-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="4a314-218">In hello **invito del team** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a314-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="4a314-219">![Invitare il team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invitare il team")</span><span class="sxs-lookup"><span data-stu-id="4a314-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="4a314-220">a.</span><span class="sxs-lookup"><span data-stu-id="4a314-220">a.</span></span> <span data-ttu-id="4a314-221">Hello tipo **First e Last Name** dell'utente come **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4a314-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="4a314-222">b.</span><span class="sxs-lookup"><span data-stu-id="4a314-222">b.</span></span> <span data-ttu-id="4a314-223">Immettere l'indirizzo **e-mail** univoco dell'utente, come **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4a314-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="4a314-224">c.</span><span class="sxs-lookup"><span data-stu-id="4a314-224">c.</span></span> <span data-ttu-id="4a314-225">Fare clic su **Add** (Aggiungi) e quindi su **Send Invites** (Invia inviti).</span><span class="sxs-lookup"><span data-stu-id="4a314-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4a314-226">Tutti gli utenti aggiunti riceveranno un toocreate invito un account PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="4a314-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4a314-227">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a314-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4a314-228">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPagerDuty.</span><span class="sxs-lookup"><span data-stu-id="4a314-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Assegnazione del ruolo utente hello][200]

<span data-ttu-id="4a314-230">**tooassign Britta Simon tooPagerDuty, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4a314-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a314-231">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a314-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4a314-233">Nell'elenco di applicazioni hello, selezionare **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="4a314-233">In hello applications list, select **PagerDuty**.</span></span>

    ![collegamento PagerDuty Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="4a314-235">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4a314-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="4a314-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4a314-237">Click **Add** button.</span></span> <span data-ttu-id="4a314-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4a314-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="4a314-240">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4a314-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a314-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4a314-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a314-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4a314-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4a314-243">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4a314-243">Test single sign-on</span></span>

<span data-ttu-id="4a314-244">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4a314-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a314-245">Quando fa clic su riquadro PagerDuty hello in hello Panelyou di accesso deve ottenere automaticamente firmato in tooyour PagerDuty applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a314-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="4a314-246">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a314-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a314-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4a314-247">Additional resources</span></span>

* [<span data-ttu-id="4a314-248">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a314-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a314-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a314-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

