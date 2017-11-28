---
title: 'Esercitazione: integrazione di Azure Active Directory con Google Apps in Azure| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="0f701-103">Esercitazione: Integrazione di Azure Active Directory con Google Apps</span><span class="sxs-lookup"><span data-stu-id="0f701-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="0f701-104">In questa esercitazione, è illustrato come toointegrate Google Apps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f701-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f701-105">Integrazione di Google Apps con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0f701-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0f701-106">È possibile controllare in Azure AD che ha accesso tooGoogle App</span><span class="sxs-lookup"><span data-stu-id="0f701-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="0f701-107">È possibile abilitare l'utenti tooautomatically get connesso tooGoogle App (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f701-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f701-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0f701-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione di app SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f701-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f701-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f701-110">Prerequisites</span></span>

<span data-ttu-id="0f701-111">tooconfigure integrazione di Azure AD con Google Apps, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0f701-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="0f701-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f701-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f701-113">Sottoscrizione di Google Apps abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0f701-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f701-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0f701-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f701-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0f701-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f701-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0f701-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f701-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f701-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="0f701-118">Esercitazione video</span><span class="sxs-lookup"><span data-stu-id="0f701-118">Video tutorial</span></span>
<span data-ttu-id="0f701-119">Come tooEnable Single Sign-On tooGoogle App in 2 minuti:</span><span class="sxs-lookup"><span data-stu-id="0f701-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="0f701-120">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0f701-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="0f701-121">**D: I dispositivi Chromebooks e altri dispositivi Chrome sono compatibili con Single Sign-On di Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="0f701-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="0f701-122">R: Sì, gli utenti sono in grado di toosign in dispositivi Chromebook utilizzando le proprie credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f701-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="0f701-123">Per informazioni sui motivi per cui agli utenti può essere richiesto di immettere le credenziali due volte, vedere questo [articolo del supporto tecnico di Google Apps](https://support.google.com/chrome/a/answer/6060880) .</span><span class="sxs-lookup"><span data-stu-id="0f701-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="0f701-124">**D: se Abilita l'accesso single sign-on, sarà possibile toouse in grado di loro toosign le credenziali di Azure AD in qualsiasi prodotto di Google, ad esempio Google corsi, GMail, Google Drive, YouTube e così via?**</span><span class="sxs-lookup"><span data-stu-id="0f701-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="0f701-125">R: Sì, in base alle [quali Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) si sceglie tooenable o disabilitare per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0f701-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="0f701-126">**D: È possibile abilitare il Single Sign-On solo per un sottoinsieme di utenti di Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="0f701-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="0f701-127">R: no, attivazione di accesso single sign-on immediatamente richiede tutti i tooauthenticate agli utenti di Google Apps con le proprie credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f701-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="0f701-128">Provider di identità hello per l'ambiente di Google Apps perché Google Apps non supporta più provider di identità, può essere AD Azure o Google, ma non entrambi hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="0f701-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="0f701-129">**D: se un utente è connesso tramite Windows, vengono che automaticamente l'autenticazione tooGoogle App senza richiesta di immettere una password?**</span><span class="sxs-lookup"><span data-stu-id="0f701-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="0f701-130">R: Sono disponibili due opzioni per l'abilitazione di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="0f701-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="0f701-131">Nel primo caso gli utenti possono accedere ai dispositivi Windows 10 tramite [Aggiunta ad Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f701-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="0f701-132">In alternativa, gli utenti accesso è riuscito in dispositivi Windows che tooan appartenenti a un dominio Active Directory a cui è stata abilitata per single sign-on tooAzure AD tramite in locale un [Active Directory Federation Services (ADFS)](active-directory-aadconnect-user-signin.md) distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0f701-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="0f701-133">Entrambe le opzioni richiedono passaggi hello tooperform hello successivo dell'esercitazione tooenable single sign-on tra Azure AD e Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f701-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f701-134">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0f701-134">Scenario description</span></span>
<span data-ttu-id="0f701-135">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0f701-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f701-136">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0f701-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f701-137">Aggiunta di Google Apps dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0f701-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="0f701-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="0f701-139">Aggiunta di Google Apps dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0f701-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="0f701-140">integrazione hello tooconfigure di Google Apps in Azure AD, è necessario tooadd Google Apps dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0f701-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0f701-141">**tooadd Google Apps dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0f701-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f701-142">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0f701-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f701-144">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0f701-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0f701-145">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0f701-145">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0f701-147">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0f701-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0f701-149">Nella casella di ricerca hello, digitare **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0f701-149">In hello search box, type **Google Apps**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="0f701-151">Nel riquadro dei risultati hello, selezionare **Google Apps**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0f701-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f701-153">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f701-154">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Google Apps usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0f701-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0f701-155">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Google Apps è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f701-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="0f701-156">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Google Apps richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0f701-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="0f701-157">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f701-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="0f701-158">tooconfigure e test Azure single sign-on AD con Google Apps, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0f701-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0f701-159">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0f701-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0f701-160">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f701-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f701-161">**[Creazione di un utente di test di Google Apps](#creating-a-google-apps-test-user)**  -toohave un equivalente di Britta Simon in Google Apps che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0f701-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f701-162">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0f701-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f701-163">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0f701-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f701-164">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f701-165">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f701-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="0f701-166">**Azure AD tooconfigure single sign-on con Google Apps, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0f701-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f701-167">Nel portale di Azure su hello hello **Google Apps** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0f701-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0f701-169">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0f701-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="0f701-171">In hello **dominio Google Apps e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0f701-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="0f701-173">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="0f701-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0f701-174">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="0f701-174">This value is not real.</span></span> <span data-ttu-id="0f701-175">Aggiornare il valore di hello con URL hello effettivo Sign-on.</span><span class="sxs-lookup"><span data-stu-id="0f701-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="0f701-176">contattare hello [team di supporto di Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0f701-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="0f701-177">In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il certificato di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0f701-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="0f701-179">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0f701-179">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0f701-181">In hello **Google Apps configurazione** fare clic su **configurare Google Apps** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="0f701-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0f701-182">Hello copia **Sign-Out URL, SAML Single Sign-On Service URL e Modifica URL password** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0f701-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="0f701-184">Aprire una nuova scheda nel browser e accedere a hello [Console di amministrazione di Google Apps](http://admin.google.com/) con l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="0f701-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="0f701-185">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="0f701-185">Click **Security**.</span></span> <span data-ttu-id="0f701-186">Se non viene visualizzato il collegamento hello, possono essere nascosti in hello **più controlli** menu in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f701-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Fare clic su sicurezza.][10]

9. <span data-ttu-id="0f701-188">In hello **sicurezza** pagina, fare clic su **configurare single sign-on (SSO).**</span><span class="sxs-lookup"><span data-stu-id="0f701-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Fare clic su SSO.][11]

10. <span data-ttu-id="0f701-190">Eseguire hello dopo le modifiche di configurazione:</span><span class="sxs-lookup"><span data-stu-id="0f701-190">Perform hello following configuration changes:</span></span>
   
    ![Configurare SSL][12]
   
    <span data-ttu-id="0f701-192">a.</span><span class="sxs-lookup"><span data-stu-id="0f701-192">a.</span></span> <span data-ttu-id="0f701-193">Selezionare **Setup SSO with third party identity provider** (Configurare l'accesso SSO con un provider di terze parti).</span><span class="sxs-lookup"><span data-stu-id="0f701-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="0f701-194">b.</span><span class="sxs-lookup"><span data-stu-id="0f701-194">b.</span></span> <span data-ttu-id="0f701-195">Nel **accesso URL della pagina** campo in Google Apps, incollare il valore di hello di **URL servizio Single Sign-On**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f701-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0f701-196">c.</span><span class="sxs-lookup"><span data-stu-id="0f701-196">c.</span></span> <span data-ttu-id="0f701-197">In hello **URL pagina di disconnessione** campo in Google Apps, incollare il valore di hello di **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f701-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0f701-198">d.</span><span class="sxs-lookup"><span data-stu-id="0f701-198">d.</span></span> <span data-ttu-id="0f701-199">In hello **Modifica URL password** campo in Google Apps, incollare il valore di hello di **Modifica URL password**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f701-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0f701-200">e.</span><span class="sxs-lookup"><span data-stu-id="0f701-200">e.</span></span> <span data-ttu-id="0f701-201">In Google Apps, per hello **certificato di verifica**, carica certificato hello scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f701-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="0f701-202">f.</span><span class="sxs-lookup"><span data-stu-id="0f701-202">f.</span></span> <span data-ttu-id="0f701-203">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="0f701-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0f701-204">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0f701-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0f701-205">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0f701-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0f701-206">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f701-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f701-207">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f701-208">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0f701-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0f701-210">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0f701-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f701-211">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0f701-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f701-213">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0f701-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f701-215">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0f701-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f701-217">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0f701-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f701-219">a.</span><span class="sxs-lookup"><span data-stu-id="0f701-219">a.</span></span> <span data-ttu-id="0f701-220">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f701-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f701-221">b.</span><span class="sxs-lookup"><span data-stu-id="0f701-221">b.</span></span> <span data-ttu-id="0f701-222">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0f701-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f701-223">c.</span><span class="sxs-lookup"><span data-stu-id="0f701-223">c.</span></span> <span data-ttu-id="0f701-224">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0f701-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0f701-225">d.</span><span class="sxs-lookup"><span data-stu-id="0f701-225">d.</span></span> <span data-ttu-id="0f701-226">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0f701-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="0f701-227">Creazione di un utente test di Google Apps</span><span class="sxs-lookup"><span data-stu-id="0f701-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="0f701-228">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Google Apps Software toocreate.</span><span class="sxs-lookup"><span data-stu-id="0f701-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="0f701-229">Google Apps supporta il provisioning automatico abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0f701-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="0f701-230">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0f701-230">There is no action for you in this section.</span></span> <span data-ttu-id="0f701-231">Se un utente non esiste già nel Software di Google Apps, quando si tenta di Google Apps Software tooaccess uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="0f701-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="0f701-232">Se è necessario un utente toocreate manualmente, contattare hello [team di supporto di Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0f701-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0f701-233">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f701-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0f701-234">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooGoogle app.</span><span class="sxs-lookup"><span data-stu-id="0f701-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0f701-236">**tooassign Britta Simon tooGoogle App, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0f701-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f701-237">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0f701-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0f701-239">Nell'elenco di applicazioni hello, selezionare **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0f701-239">In hello applications list, select **Google Apps**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="0f701-241">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0f701-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0f701-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0f701-243">Click **Add** button.</span></span> <span data-ttu-id="0f701-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0f701-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0f701-246">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0f701-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0f701-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0f701-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f701-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0f701-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f701-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0f701-249">Testing single sign-on</span></span>

<span data-ttu-id="0f701-250">In questa sezione, tootest le impostazioni single sign-on, aprire Pannello di accesso a hello [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), quindi accedere all'account di prova hello e fare clic su **Google Apps** riquadro in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0f701-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f701-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0f701-251">Additional resources</span></span>

* [<span data-ttu-id="0f701-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f701-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f701-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f701-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0f701-254">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="0f701-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png