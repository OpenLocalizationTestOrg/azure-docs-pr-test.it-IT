---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workstars | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workstars.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="ccaae-103">Esercitazione: integrazione di Azure Active Directory con Workstars</span><span class="sxs-lookup"><span data-stu-id="ccaae-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="ccaae-104">In questa esercitazione, è illustrato come toointegrate Workstars con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ccaae-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ccaae-105">Integrazione Workstars con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ccaae-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ccaae-106">È possibile controllare in Azure AD che ha accesso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="ccaae-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="ccaae-107">È possibile abilitare l'utenti tooautomatically get connesso tooWorkstars (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccaae-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ccaae-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccaae-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ccaae-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ccaae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccaae-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ccaae-110">Prerequisites</span></span>

<span data-ttu-id="ccaae-111">integrazione di Azure AD con Workstars tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ccaae-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="ccaae-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccaae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ccaae-113">Sottoscrizione di Workstars abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ccaae-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ccaae-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ccaae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ccaae-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ccaae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ccaae-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ccaae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ccaae-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ccaae-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ccaae-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ccaae-118">Scenario description</span></span>
<span data-ttu-id="ccaae-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ccaae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ccaae-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ccaae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ccaae-121">Aggiunta di Workstars dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ccaae-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="ccaae-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccaae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="ccaae-123">Aggiunta di Workstars dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ccaae-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="ccaae-124">integrazione hello tooconfigure di Workstars in Azure AD, è necessario tooadd Workstars dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ccaae-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ccaae-125">**tooadd Workstars dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ccaae-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccaae-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ccaae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="ccaae-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ccaae-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="ccaae-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ccaae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="ccaae-133">Nella casella di ricerca hello, digitare **Workstars**selezionare **Workstars** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ccaae-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ccaae-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccaae-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ccaae-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workstars usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ccaae-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ccaae-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workstars è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccaae-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="ccaae-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workstars deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ccaae-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="ccaae-139">In Workstars, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ccaae-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ccaae-140">tooconfigure e prova AD Azure single sign-on con Workstars, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ccaae-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ccaae-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ccaae-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ccaae-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ccaae-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ccaae-143">**[Creare un utente test Workstars](#create-a-workstars-test-user)**  -toohave un equivalente di Britta Simon in Workstars che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ccaae-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ccaae-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ccaae-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ccaae-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ccaae-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ccaae-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccaae-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ccaae-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workstars.</span><span class="sxs-lookup"><span data-stu-id="ccaae-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="ccaae-148">**Azure AD tooconfigure single sign-on con Workstars, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ccaae-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccaae-149">Nel portale di Azure su hello hello **Workstars** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="ccaae-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ccaae-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="ccaae-153">In hello **Workstars dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ccaae-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="ccaae-155">a.</span><span class="sxs-lookup"><span data-stu-id="ccaae-155">a.</span></span> <span data-ttu-id="ccaae-156">In hello **identificatore** casella di testo, digitare l'URL hello:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="ccaae-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="ccaae-157">b.</span><span class="sxs-lookup"><span data-stu-id="ccaae-157">b.</span></span> <span data-ttu-id="ccaae-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="ccaae-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ccaae-159">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="ccaae-159">hello value is not real.</span></span> <span data-ttu-id="ccaae-160">Il valore di hello aggiornamento con hello URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="ccaae-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="ccaae-161">Contatto [team di supporto Workstars](https://support.workstars.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="ccaae-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="ccaae-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ccaae-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="ccaae-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ccaae-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ccaae-166">In hello **Workstars configurazione** fare clic su **configurare Workstars** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ccaae-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ccaae-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ccaae-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="ccaae-169">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour Workstars.</span><span class="sxs-lookup"><span data-stu-id="ccaae-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="ccaae-170">Nella barra degli strumenti principale hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-170">In hello main toolbar, click **Settings**.</span></span>

    ![Impostazioni di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="ccaae-172">Andare troppo**Sign On** > **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-172">Go too**Sign On** > **Settings**.</span></span>

    ![Accesso a Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Impostazioni di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="ccaae-175">In hello **Single Sign in (SAML) - impostazioni** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ccaae-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![SAML di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="ccaae-177">a.</span><span class="sxs-lookup"><span data-stu-id="ccaae-177">a.</span></span> <span data-ttu-id="ccaae-178">Nella casella di testo **Nome provider identità** digitare **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="ccaae-179">b.</span><span class="sxs-lookup"><span data-stu-id="ccaae-179">b.</span></span> <span data-ttu-id="ccaae-180">In hello **Identity Provider Entity ID** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccaae-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ccaae-181">c.</span><span class="sxs-lookup"><span data-stu-id="ccaae-181">c.</span></span> <span data-ttu-id="ccaae-182">Copiare il contenuto di hello del file di certificato scaricato hello nel blocco note e quindi incollarlo hello **x509 certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ccaae-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="ccaae-183">d.</span><span class="sxs-lookup"><span data-stu-id="ccaae-183">d.</span></span> <span data-ttu-id="ccaae-184">In hello **URL SSO SAML** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccaae-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ccaae-185">e.</span><span class="sxs-lookup"><span data-stu-id="ccaae-185">e.</span></span> <span data-ttu-id="ccaae-186">In hello **URL disconnessione remota** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccaae-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ccaae-187">f.</span><span class="sxs-lookup"><span data-stu-id="ccaae-187">f.</span></span> <span data-ttu-id="ccaae-188">impostare **ID nome** su **Email (Default)** (Posta elettronica (impostazione predefinita)).</span><span class="sxs-lookup"><span data-stu-id="ccaae-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="ccaae-189">g.</span><span class="sxs-lookup"><span data-stu-id="ccaae-189">g.</span></span> <span data-ttu-id="ccaae-190">Fare clic su **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="ccaae-191">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ccaae-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ccaae-192">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ccaae-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ccaae-193">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ccaae-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ccaae-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccaae-194">Create an Azure AD test user</span></span>

<span data-ttu-id="ccaae-195">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ccaae-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="ccaae-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ccaae-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccaae-198">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ccaae-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ccaae-200">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ccaae-202">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ccaae-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ccaae-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ccaae-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ccaae-206">a.</span><span class="sxs-lookup"><span data-stu-id="ccaae-206">a.</span></span> <span data-ttu-id="ccaae-207">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ccaae-208">b.</span><span class="sxs-lookup"><span data-stu-id="ccaae-208">b.</span></span> <span data-ttu-id="ccaae-209">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ccaae-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ccaae-210">c.</span><span class="sxs-lookup"><span data-stu-id="ccaae-210">c.</span></span> <span data-ttu-id="ccaae-211">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="ccaae-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ccaae-212">d.</span><span class="sxs-lookup"><span data-stu-id="ccaae-212">d.</span></span> <span data-ttu-id="ccaae-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="ccaae-214">Creare un utente di test di Workstars</span><span class="sxs-lookup"><span data-stu-id="ccaae-214">Create a Workstars test user</span></span>

<span data-ttu-id="ccaae-215">In questa sezione viene creato un utente di nome Britta Simon in Workstars.</span><span class="sxs-lookup"><span data-stu-id="ccaae-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="ccaae-216">Lavorare con [Workstars team di supporto](https://support.workstars.com) utenti hello tooadd nella piattaforma Workstars hello.</span><span class="sxs-lookup"><span data-stu-id="ccaae-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ccaae-217">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccaae-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ccaae-218">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="ccaae-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="ccaae-220">**tooassign Britta Simon tooWorkstars, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ccaae-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccaae-221">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ccaae-223">Nell'elenco di applicazioni hello, selezionare **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-223">In hello applications list, select **Workstars**.</span></span>

    ![collegamento Workstars Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="ccaae-225">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="ccaae-227">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-227">Click **Add** button.</span></span> <span data-ttu-id="ccaae-228">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="ccaae-230">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ccaae-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ccaae-231">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ccaae-232">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ccaae-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ccaae-233">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ccaae-233">Test single sign-on</span></span>

<span data-ttu-id="ccaae-234">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ccaae-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ccaae-235">Quando si fa clic hello Workstars riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Workstars applicazione.</span><span class="sxs-lookup"><span data-stu-id="ccaae-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="ccaae-236">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ccaae-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ccaae-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ccaae-237">Additional resources</span></span>

* [<span data-ttu-id="ccaae-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccaae-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ccaae-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccaae-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

