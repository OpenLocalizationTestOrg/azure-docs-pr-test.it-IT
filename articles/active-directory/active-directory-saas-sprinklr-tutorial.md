---
title: 'Esercitazione: Integrazione di Azure Active Directory con Sprinklr | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="05adb-103">Esercitazione: Integrazione di Azure Active Directory con Sprinklr</span><span class="sxs-lookup"><span data-stu-id="05adb-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="05adb-104">In questa esercitazione, è illustrato come toointegrate Sprinklr con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05adb-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05adb-105">Integrazione Sprinklr con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="05adb-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05adb-106">È possibile controllare in Azure AD che ha accesso tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="05adb-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="05adb-107">È possibile abilitare l'utenti tooautomatically get connesso tooSprinklr (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05adb-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="05adb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="05adb-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05adb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05adb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05adb-110">Prerequisites</span></span>

<span data-ttu-id="05adb-111">integrazione di Azure AD con Sprinklr tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="05adb-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="05adb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05adb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05adb-113">Sottoscrizione di Sprinklr abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05adb-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05adb-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="05adb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05adb-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="05adb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05adb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="05adb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05adb-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05adb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05adb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="05adb-118">Scenario description</span></span>
<span data-ttu-id="05adb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="05adb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05adb-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="05adb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05adb-121">Aggiunta di Sprinklr dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="05adb-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="05adb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="05adb-123">Aggiunta di Sprinklr dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="05adb-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="05adb-124">integrazione hello tooconfigure di Sprinklr in Azure AD, è necessario tooadd Sprinklr dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="05adb-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05adb-125">**tooadd Sprinklr dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05adb-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05adb-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="05adb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05adb-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="05adb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05adb-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="05adb-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="05adb-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="05adb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="05adb-133">Nella casella di ricerca hello, digitare **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="05adb-133">In hello search box, type **Sprinklr**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="05adb-135">Nel riquadro dei risultati hello, selezionare **Sprinklr**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="05adb-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05adb-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05adb-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Sprinklr usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05adb-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05adb-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Sprinklr è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05adb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="05adb-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Sprinklr deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="05adb-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="05adb-141">In Sprinklr, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="05adb-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05adb-142">tooconfigure e test Azure single sign-on AD con Sprinklr, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="05adb-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05adb-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="05adb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05adb-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05adb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05adb-145">**[Creazione di un utente test Sprinklr](#creating-a-sprinklr-test-user)**  -toohave un equivalente di Britta Simon in Sprinklr che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="05adb-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05adb-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05adb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05adb-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="05adb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05adb-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05adb-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="05adb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="05adb-150">**Azure AD tooconfigure single sign-on con Sprinklr, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05adb-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="05adb-151">Nel portale di Azure su hello hello **Sprinklr** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="05adb-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="05adb-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05adb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="05adb-155">In hello **Sprinklr dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05adb-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="05adb-157">a.</span><span class="sxs-lookup"><span data-stu-id="05adb-157">a.</span></span> <span data-ttu-id="05adb-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="05adb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="05adb-159">b.</span><span class="sxs-lookup"><span data-stu-id="05adb-159">b.</span></span> <span data-ttu-id="05adb-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="05adb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05adb-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="05adb-161">These values are not real.</span></span> <span data-ttu-id="05adb-162">Aggiornare il valore di hello con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="05adb-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05adb-163">Contatto [team di supporto Sprinklr Client](https://www.sprinklr.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="05adb-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="05adb-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="05adb-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="05adb-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="05adb-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05adb-168">In hello **Sprinklr configurazione** fare clic su **configurare Sprinklr** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="05adb-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="05adb-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="05adb-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="05adb-170">In una finestra del web browser, accedere come amministratore nel sito della società Sprinklr di tooyour.</span><span class="sxs-lookup"><span data-stu-id="05adb-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="05adb-171">Andare troppo**amministrazione \> impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="05adb-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="05adb-172">![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="05adb-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="05adb-173">Andare troppo**gestire Partner \> l'accesso Single Sign** su hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="05adb-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="05adb-174">![Gestione partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gestione partner")</span><span class="sxs-lookup"><span data-stu-id="05adb-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="05adb-175">Fare clic su **+ Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="05adb-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="05adb-176">![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Accessi Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="05adb-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="05adb-177">In hello **Single Sign-on** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05adb-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="05adb-178">![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Accessi Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="05adb-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="05adb-179">a.</span><span class="sxs-lookup"><span data-stu-id="05adb-179">a.</span></span> <span data-ttu-id="05adb-180">In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="05adb-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="05adb-181">b.</span><span class="sxs-lookup"><span data-stu-id="05adb-181">b.</span></span> <span data-ttu-id="05adb-182">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="05adb-182">Select **Enabled**.</span></span>

    <span data-ttu-id="05adb-183">c.</span><span class="sxs-lookup"><span data-stu-id="05adb-183">c.</span></span> <span data-ttu-id="05adb-184">Selezionare **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="05adb-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="05adb-185">e.</span><span class="sxs-lookup"><span data-stu-id="05adb-185">e.</span></span> <span data-ttu-id="05adb-186">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **Identity Provider Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="05adb-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="05adb-187">f.</span><span class="sxs-lookup"><span data-stu-id="05adb-187">f.</span></span> <span data-ttu-id="05adb-188">Hello Incolla **ID entità SAML** valore a cui è stato copiato dal portale di Azure in hello **Id entità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="05adb-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="05adb-189">g.</span><span class="sxs-lookup"><span data-stu-id="05adb-189">g.</span></span> <span data-ttu-id="05adb-190">Hello Incolla **SAML Single Sign-On Service URL** valore a cui è stato copiato dal portale di Azure in hello **Identity Provider Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="05adb-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="05adb-191">h.</span><span class="sxs-lookup"><span data-stu-id="05adb-191">h.</span></span> <span data-ttu-id="05adb-192">Hello Incolla **Sign-Out URL** valore a cui è stato copiato dal portale di Azure in hello **Identity Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="05adb-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="05adb-193">i.</span><span class="sxs-lookup"><span data-stu-id="05adb-193">i.</span></span> <span data-ttu-id="05adb-194">In **SAML User ID Type** (Tipo ID utente SAML) selezionare **Assertion contains User”s sprinklr.com username** (L'asserzione contiene il nome utente sprinklr.com dell'utente).</span><span class="sxs-lookup"><span data-stu-id="05adb-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="05adb-195">j.</span><span class="sxs-lookup"><span data-stu-id="05adb-195">j.</span></span> <span data-ttu-id="05adb-196">Come **SAML User ID Location**selezionare **è l'ID utente nell'elemento di nome identificatore hello dell'istruzione Subject hello**.</span><span class="sxs-lookup"><span data-stu-id="05adb-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="05adb-197">k.</span><span class="sxs-lookup"><span data-stu-id="05adb-197">k.</span></span> <span data-ttu-id="05adb-198">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="05adb-198">Click **Save**.</span></span>
       
    <span data-ttu-id="05adb-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="05adb-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="05adb-200">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="05adb-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05adb-201">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="05adb-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05adb-202">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05adb-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05adb-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="05adb-204">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="05adb-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="05adb-206">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05adb-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05adb-207">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="05adb-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05adb-209">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="05adb-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05adb-211">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="05adb-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05adb-213">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05adb-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05adb-215">a.</span><span class="sxs-lookup"><span data-stu-id="05adb-215">a.</span></span> <span data-ttu-id="05adb-216">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05adb-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05adb-217">b.</span><span class="sxs-lookup"><span data-stu-id="05adb-217">b.</span></span> <span data-ttu-id="05adb-218">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05adb-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05adb-219">c.</span><span class="sxs-lookup"><span data-stu-id="05adb-219">c.</span></span> <span data-ttu-id="05adb-220">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="05adb-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05adb-221">d.</span><span class="sxs-lookup"><span data-stu-id="05adb-221">d.</span></span> <span data-ttu-id="05adb-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="05adb-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="05adb-223">Creazione di un utente di test di Sprinklr</span><span class="sxs-lookup"><span data-stu-id="05adb-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="05adb-224">Accedi tooyour sito della società Sprinklr come amministratore.</span><span class="sxs-lookup"><span data-stu-id="05adb-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="05adb-225">Andare troppo**amministrazione \> impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="05adb-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="05adb-226">![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="05adb-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="05adb-227">Andare troppo**gestire Client \> utenti** hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="05adb-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="05adb-228">![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="05adb-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="05adb-229">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="05adb-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="05adb-230">![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="05adb-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="05adb-231">In hello **modifica utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05adb-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="05adb-232">![Modifica degli utenti](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Modifica degli utenti")</span><span class="sxs-lookup"><span data-stu-id="05adb-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="05adb-233">a.</span><span class="sxs-lookup"><span data-stu-id="05adb-233">a.</span></span> <span data-ttu-id="05adb-234">In hello **posta elettronica**, **nome** e **cognome** nelle caselle di testo, informazioni sul tipo di hello di un account utente di Azure AD desiderato tooprovision.</span><span class="sxs-lookup"><span data-stu-id="05adb-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="05adb-235">b.</span><span class="sxs-lookup"><span data-stu-id="05adb-235">b.</span></span> <span data-ttu-id="05adb-236">Selezionare **Password disabled**.</span><span class="sxs-lookup"><span data-stu-id="05adb-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="05adb-237">c.</span><span class="sxs-lookup"><span data-stu-id="05adb-237">c.</span></span> <span data-ttu-id="05adb-238">Selezionare **Language** (Lingua).</span><span class="sxs-lookup"><span data-stu-id="05adb-238">Select **Language**.</span></span>

    <span data-ttu-id="05adb-239">d.</span><span class="sxs-lookup"><span data-stu-id="05adb-239">d.</span></span> <span data-ttu-id="05adb-240">Selezionare **User Type** (Tipo di utente).</span><span class="sxs-lookup"><span data-stu-id="05adb-240">Select **User Type**.</span></span>

    <span data-ttu-id="05adb-241">e.</span><span class="sxs-lookup"><span data-stu-id="05adb-241">e.</span></span> <span data-ttu-id="05adb-242">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="05adb-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="05adb-243">**Password Disabled** deve essere selezionato tooenable toolog un utente in tramite un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="05adb-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="05adb-244">Andare troppo**ruolo**e quindi eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05adb-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="05adb-245">![Ruoli partner](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Ruoli partner")</span><span class="sxs-lookup"><span data-stu-id="05adb-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="05adb-246">a.</span><span class="sxs-lookup"><span data-stu-id="05adb-246">a.</span></span> <span data-ttu-id="05adb-247">Da hello **globale** elenco, selezionare **tutti\_autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="05adb-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="05adb-248">b.</span><span class="sxs-lookup"><span data-stu-id="05adb-248">b.</span></span> <span data-ttu-id="05adb-249">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="05adb-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="05adb-250">È possibile usare qualsiasi altro Sprinklr utente account strumento di creazione o le API fornite da Sprinklr tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05adb-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="05adb-251">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05adb-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="05adb-252">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="05adb-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Assegna utente][200] 

<span data-ttu-id="05adb-254">**tooassign Britta Simon tooSprinklr, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05adb-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="05adb-255">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="05adb-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="05adb-257">Nell'elenco di applicazioni hello, selezionare **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="05adb-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="05adb-259">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="05adb-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="05adb-261">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="05adb-261">Click **Add** button.</span></span> <span data-ttu-id="05adb-262">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="05adb-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="05adb-264">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="05adb-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05adb-265">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="05adb-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05adb-266">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="05adb-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05adb-267">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05adb-267">Testing single sign-on</span></span>

<span data-ttu-id="05adb-268">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="05adb-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="05adb-269">Quando si fa clic su riquadro Sprinklr hello in hello Pannello di accesso, deve ottenere tooyour automaticamente firmato in Sprinklr applicazione per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05adb-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05adb-270">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="05adb-270">Additional resources</span></span>

* [<span data-ttu-id="05adb-271">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05adb-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05adb-272">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05adb-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

