---
title: 'Esercitazione: Integrazione di Azure Active Directory con Druva| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="cfaf0-103">Esercitazione: Integrazione di Azure Active Directory con Druva</span><span class="sxs-lookup"><span data-stu-id="cfaf0-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="cfaf0-104">In questa esercitazione, è illustrato come toointegrate Druva con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfaf0-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfaf0-105">Integrazione di Druva con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfaf0-106">È possibile controllare in Azure AD che ha accesso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="cfaf0-107">È possibile abilitare l'utenti tooautomatically get connesso tooDruva (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cfaf0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cfaf0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfaf0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfaf0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cfaf0-110">Prerequisites</span></span>

<span data-ttu-id="cfaf0-111">integrazione di Azure AD con Druva tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="cfaf0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfaf0-113">Sottoscrizione di Druva abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cfaf0-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfaf0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfaf0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfaf0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfaf0-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfaf0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfaf0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cfaf0-118">Scenario description</span></span>
<span data-ttu-id="cfaf0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfaf0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfaf0-121">Aggiunta di Druva dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfaf0-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="cfaf0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfaf0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="cfaf0-123">Aggiunta di Druva dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfaf0-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="cfaf0-124">integrazione hello tooconfigure di Druva in Azure AD, è necessario tooadd Druva dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfaf0-125">**tooadd Druva dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfaf0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="cfaf0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfaf0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="cfaf0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="cfaf0-133">Nella casella di ricerca hello, digitare **Druva**selezionare **Druva** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Druva](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cfaf0-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfaf0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cfaf0-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Druva in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cfaf0-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfaf0-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Druva è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="cfaf0-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Druva deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="cfaf0-139">In Druva, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfaf0-140">tooconfigure e prova AD Azure single sign-on con Druva, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfaf0-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfaf0-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfaf0-143">**[Creare un utente test Druva](#create-a-druva-test-user)**  -toohave un equivalente di Britta Simon in Druva che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfaf0-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfaf0-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cfaf0-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfaf0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cfaf0-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Druva.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="cfaf0-148">**Azure AD tooconfigure single sign-on con Druva, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfaf0-149">Nel portale di Azure su hello hello **Druva** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="cfaf0-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="cfaf0-153">In hello **Druva dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="cfaf0-155">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="cfaf0-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="cfaf0-156">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="cfaf0-158">L'applicazione Druva prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi Token SAML** configurazione.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="cfaf0-160">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine precedente hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="cfaf0-161">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="cfaf0-161">Attribute Name</span></span>      | <span data-ttu-id="cfaf0-162">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="cfaf0-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="cfaf0-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="cfaf0-163">insync\_auth\_token</span></span> |<span data-ttu-id="cfaf0-164">Immettere valore generato token hello</span><span class="sxs-lookup"><span data-stu-id="cfaf0-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="cfaf0-165">a.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-165">a.</span></span> <span data-ttu-id="cfaf0-166">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="cfaf0-169">b.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-169">b.</span></span> <span data-ttu-id="cfaf0-170">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="cfaf0-171">c.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-171">c.</span></span> <span data-ttu-id="cfaf0-172">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="cfaf0-173">valore del token generato Hello è illustrato più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="cfaf0-174">d.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-174">d.</span></span> <span data-ttu-id="cfaf0-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="cfaf0-176">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cfaf0-176">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cfaf0-178">In hello **Druva configurazione** fare clic su **configurare Druva** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cfaf0-179">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="cfaf0-181">In una finestra del web browser, accedere come amministratore nel sito della società Druva di tooyour.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="cfaf0-182">Andare troppo**Gestisci \> impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="cfaf0-183">![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795091.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="cfaf0-184">Nella finestra di dialogo Impostazioni di Single Sign-On hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="cfaf0-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="cfaf0-186">a.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-186">a.</span></span> <span data-ttu-id="cfaf0-187">Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **ID Provider Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="cfaf0-188">b.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-188">b.</span></span> <span data-ttu-id="cfaf0-189">Incolla **Sign-Out URL** valore, che è stato copiato dal portale di Azure hello in hello **ID Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="cfaf0-190">c.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-190">c.</span></span> <span data-ttu-id="cfaf0-191">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **ID Provider Certificate** casella di testo</span><span class="sxs-lookup"><span data-stu-id="cfaf0-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="cfaf0-192">d.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-192">d.</span></span> <span data-ttu-id="cfaf0-193">hello tooopen **impostazioni** pagina, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="cfaf0-194">In hello **impostazioni** pagina, fare clic su **Generate SSO Token**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="cfaf0-195">![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795093.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="cfaf0-196">In hello **Single Sign-on Authentication Token** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="cfaf0-197">![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="cfaf0-198">a.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-198">a.</span></span> <span data-ttu-id="cfaf0-199">Fare clic su **copia**, Incolla copiato valore hello **valore** casella di testo in hello **Aggiungi attributo** sezione.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="cfaf0-200">b.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-200">b.</span></span> <span data-ttu-id="cfaf0-201">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="cfaf0-202">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cfaf0-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfaf0-203">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfaf0-204">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfaf0-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cfaf0-205">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfaf0-205">Create an Azure AD test user</span></span>

<span data-ttu-id="cfaf0-206">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="cfaf0-208">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfaf0-209">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cfaf0-211">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cfaf0-213">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cfaf0-215">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cfaf0-217">a.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-217">a.</span></span> <span data-ttu-id="cfaf0-218">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfaf0-219">b.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-219">b.</span></span> <span data-ttu-id="cfaf0-220">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cfaf0-221">c.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-221">c.</span></span> <span data-ttu-id="cfaf0-222">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cfaf0-223">d.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-223">d.</span></span> <span data-ttu-id="cfaf0-224">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="cfaf0-225">Creare un utente test Druva</span><span class="sxs-lookup"><span data-stu-id="cfaf0-225">Create a Druva test user</span></span>

<span data-ttu-id="cfaf0-226">In ordine tooenable Azure AD utenti toolog in tooDruva, è necessario eseguirne il provisioning in Druva.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="cfaf0-227">Nel caso di hello di Druva, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="cfaf0-228">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfaf0-229">Accedi tooyour **Druva** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="cfaf0-230">Andare troppo**Gestisci \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="cfaf0-231">![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="cfaf0-232">Fare clic su **Create New**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="cfaf0-233">![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="cfaf0-234">Nella finestra di dialogo Create New User hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfaf0-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="cfaf0-235">![Crea nuovo utente](./media/active-directory-saas-druva-tutorial/ic795099.png "Crea nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="cfaf0-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="cfaf0-236">a.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-236">a.</span></span> <span data-ttu-id="cfaf0-237">In hello **indirizzo di posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cfaf0-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="cfaf0-238">b.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-238">b.</span></span> <span data-ttu-id="cfaf0-239">In hello **nome** casella di testo, immettere il nome di hello dell'utente come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="cfaf0-240">c.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-240">c.</span></span> <span data-ttu-id="cfaf0-241">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="cfaf0-242">È possibile usare qualsiasi altro Druva utente account strumento di creazione o le API fornite da Druva tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cfaf0-243">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfaf0-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cfaf0-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="cfaf0-246">**tooassign Britta Simon tooDruva, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfaf0-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfaf0-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cfaf0-249">Nell'elenco di applicazioni hello, selezionare **Druva**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-249">In hello applications list, select **Druva**.</span></span>

    ![collegamento di Druva Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="cfaf0-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="cfaf0-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-253">Click **Add** button.</span></span> <span data-ttu-id="cfaf0-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="cfaf0-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfaf0-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfaf0-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cfaf0-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cfaf0-259">Test single sign-on</span></span>

<span data-ttu-id="cfaf0-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfaf0-261">Quando si fa clic su riquadro Druva hello in hello Pannello di accesso, è necessario ottenere l'applicazione Druva tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="cfaf0-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="cfaf0-262">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cfaf0-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cfaf0-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cfaf0-263">Additional resources</span></span>

* [<span data-ttu-id="cfaf0-264">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfaf0-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfaf0-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfaf0-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

