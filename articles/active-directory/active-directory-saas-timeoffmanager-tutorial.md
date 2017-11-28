---
title: 'Esercitazione: Integrazione di Azure Active Directory con TimeOffManager | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="8504d-103">Esercitazione: Integrazione di Azure Active Directory con TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="8504d-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="8504d-104">In questa esercitazione, è illustrato come toointegrate TimeOffManager con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8504d-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8504d-105">Integrazione di TimeOffManager con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8504d-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8504d-106">È possibile controllare in Azure AD che ha accesso tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="8504d-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="8504d-107">È possibile abilitare l'utenti tooautomatically get connesso tooTimeOffManager (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8504d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8504d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8504d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8504d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8504d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8504d-110">Prerequisites</span></span>

<span data-ttu-id="8504d-111">integrazione di Azure AD con TimeOffManager tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8504d-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="8504d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8504d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8504d-113">Sottoscrizione di TimeOffManager abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8504d-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8504d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8504d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8504d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8504d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8504d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8504d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8504d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8504d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8504d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8504d-118">Scenario description</span></span>
<span data-ttu-id="8504d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8504d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8504d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8504d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8504d-121">Aggiungere TimeOffManager dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="8504d-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="8504d-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="8504d-123">Aggiungere TimeOffManager dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="8504d-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="8504d-124">integrazione hello tooconfigure di TimeOffManager in Azure AD, è necessario tooadd TimeOffManager dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8504d-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8504d-125">**tooadd TimeOffManager dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8504d-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8504d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8504d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8504d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8504d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8504d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8504d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8504d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8504d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8504d-133">Nella casella di ricerca hello, digitare **TimeOffManager**selezionare **TimeOffManager** dal Pannello di risultato e quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8504d-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8504d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8504d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TimeOffManager usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8504d-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8504d-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TimeOffManager è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8504d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="8504d-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TimeOffManager deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8504d-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="8504d-139">In TimeOffManager, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8504d-140">tooconfigure e prova AD Azure single sign-on con TimeOffManager, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8504d-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8504d-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8504d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8504d-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8504d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8504d-143">**[Creare un utente test TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave un equivalente di Britta Simon in TimeOffManager che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8504d-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8504d-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8504d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8504d-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8504d-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8504d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8504d-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="8504d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="8504d-148">**Azure AD tooconfigure single sign-on con TimeOffManager, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8504d-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="8504d-149">Nel portale di Azure su hello hello **TimeOffManager** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8504d-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8504d-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8504d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="8504d-153">In hello **TimeOffManager dominio e gli URL** sezione, eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="8504d-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Sezione URL e dominio TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="8504d-155">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="8504d-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8504d-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="8504d-156">This value is not real.</span></span> <span data-ttu-id="8504d-157">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="8504d-158">È possibile ottenere questo valore da **Single Sign-on pagina Impostazioni** descritta più avanti nell'esercitazione hello o un contatto [team di supporto TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="8504d-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="8504d-159">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8504d-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="8504d-161">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooTimeOffManger con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="8504d-162">L'applicazione TimeOffManger prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="8504d-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8504d-163">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="8504d-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="8504d-164">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="8504d-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="8504d-165">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8504d-165">Attribute Name</span></span> | <span data-ttu-id="8504d-166">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8504d-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8504d-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="8504d-167">Firstname</span></span> |<span data-ttu-id="8504d-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="8504d-168">User.givenname</span></span> |
    | <span data-ttu-id="8504d-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="8504d-169">Lastname</span></span> |<span data-ttu-id="8504d-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="8504d-170">User.surname</span></span> |
    | <span data-ttu-id="8504d-171">Email</span><span class="sxs-lookup"><span data-stu-id="8504d-171">Email</span></span> |<span data-ttu-id="8504d-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="8504d-172">User.mail</span></span> |
    
    <span data-ttu-id="8504d-173">a.</span><span class="sxs-lookup"><span data-stu-id="8504d-173">a.</span></span>  <span data-ttu-id="8504d-174">Per ogni riga di dati della tabella hello precedente, fare clic su **Aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="8504d-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="8504d-175">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="8504d-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="8504d-176">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="8504d-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="8504d-177">b.</span><span class="sxs-lookup"><span data-stu-id="8504d-177">b.</span></span>  <span data-ttu-id="8504d-178">In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8504d-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8504d-179">c.</span><span class="sxs-lookup"><span data-stu-id="8504d-179">c.</span></span>  <span data-ttu-id="8504d-180">In hello **valore dell'attributo** casella di testo, il valore di attributo hello selezionare mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8504d-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="8504d-181">d.</span><span class="sxs-lookup"><span data-stu-id="8504d-181">d.</span></span>  <span data-ttu-id="8504d-182">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8504d-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="8504d-183">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8504d-183">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8504d-185">In hello **TimeOffManager configurazione** fare clic su **configurare TimeOffManager** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8504d-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8504d-186">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8504d-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sezione Configurazione di TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="8504d-188">In un'altra finestra del Web browser accedere al sito aziendale di TimeOffManager come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8504d-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="8504d-189">Andare troppo**Account \> opzioni Account \> Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="8504d-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="8504d-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="8504d-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="8504d-191">In hello **Single Sign-On Settings** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8504d-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="8504d-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="8504d-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="8504d-193">a.</span><span class="sxs-lookup"><span data-stu-id="8504d-193">a.</span></span> <span data-ttu-id="8504d-194">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollare hello intero certificato nella **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8504d-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="8504d-195">b.</span><span class="sxs-lookup"><span data-stu-id="8504d-195">b.</span></span> <span data-ttu-id="8504d-196">In **Idp Issuer** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8504d-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="8504d-197">c.</span><span class="sxs-lookup"><span data-stu-id="8504d-197">c.</span></span> <span data-ttu-id="8504d-198">In **IdP Endpoint URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8504d-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="8504d-199">d.</span><span class="sxs-lookup"><span data-stu-id="8504d-199">d.</span></span> <span data-ttu-id="8504d-200">Per **Enforce SAML** (Applica SAML), selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="8504d-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="8504d-201">e.</span><span class="sxs-lookup"><span data-stu-id="8504d-201">e.</span></span> <span data-ttu-id="8504d-202">Per **Auto-Create Users** (Crea utenti in automatico), selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="8504d-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="8504d-203">f.</span><span class="sxs-lookup"><span data-stu-id="8504d-203">f.</span></span> <span data-ttu-id="8504d-204">In **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8504d-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="8504d-205">g.</span><span class="sxs-lookup"><span data-stu-id="8504d-205">g.</span></span> <span data-ttu-id="8504d-206">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="8504d-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="8504d-207">In **Single Sign-on impostazioni** valore hello copia della pagina **URL del servizio Consumer di asserzione** e incollarlo in hello **URL di risposta** casella di testo **TimeOffManager Dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8504d-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="8504d-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="8504d-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="8504d-209">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8504d-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8504d-210">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8504d-211">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8504d-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8504d-212">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-212">Create an Azure AD test user</span></span>
<span data-ttu-id="8504d-213">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8504d-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8504d-215">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8504d-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8504d-216">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8504d-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8504d-218">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8504d-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi --> Tutti gli utenti](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8504d-220">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8504d-222">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8504d-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8504d-224">a.</span><span class="sxs-lookup"><span data-stu-id="8504d-224">a.</span></span> <span data-ttu-id="8504d-225">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8504d-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8504d-226">b.</span><span class="sxs-lookup"><span data-stu-id="8504d-226">b.</span></span> <span data-ttu-id="8504d-227">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8504d-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8504d-228">c.</span><span class="sxs-lookup"><span data-stu-id="8504d-228">c.</span></span> <span data-ttu-id="8504d-229">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8504d-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8504d-230">d.</span><span class="sxs-lookup"><span data-stu-id="8504d-230">d.</span></span> <span data-ttu-id="8504d-231">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8504d-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="8504d-232">Creare un utente di test di TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="8504d-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="8504d-233">In ordine tooenable Azure AD utenti toolog a TimeOffManager, devono essere tooTimeOffManager provisioning.</span><span class="sxs-lookup"><span data-stu-id="8504d-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="8504d-234">TimeOffManager supporta solo il provisioning just in time dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8504d-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="8504d-235">Non è necessario eseguire alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="8504d-235">There is no action item for you.</span></span>  

<span data-ttu-id="8504d-236">gli utenti di Hello vengono aggiunti automaticamente durante il primo accesso hello con single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8504d-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="8504d-237">È possibile usare qualsiasi altro TimeOffManager utente account strumento di creazione o le API fornite da TimeOffManager tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8504d-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8504d-238">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8504d-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8504d-239">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="8504d-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8504d-241">**tooassign Britta Simon tooTimeOffManager, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8504d-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="8504d-242">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8504d-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8504d-244">Nell'elenco di applicazioni hello, selezionare **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="8504d-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager nell'elenco di app](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="8504d-246">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8504d-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8504d-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8504d-248">Click **Add** button.</span></span> <span data-ttu-id="8504d-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8504d-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8504d-251">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8504d-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8504d-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8504d-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8504d-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8504d-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8504d-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8504d-254">Test single sign-on</span></span>

<span data-ttu-id="8504d-255">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8504d-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8504d-256">Quando si fa clic su riquadro TimeOffManager hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour TimeOffManager applicazione.</span><span class="sxs-lookup"><span data-stu-id="8504d-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="8504d-257">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8504d-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8504d-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8504d-258">Additional resources</span></span>

* [<span data-ttu-id="8504d-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8504d-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8504d-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8504d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

