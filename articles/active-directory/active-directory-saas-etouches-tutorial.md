---
title: 'Esercitazione: Integrazione di Azure Active Directory con etouches | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed etouches.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="df1b2-103">Esercitazione: Integrazione di Azure Active Directory con eTouches</span><span class="sxs-lookup"><span data-stu-id="df1b2-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="df1b2-104">In questa esercitazione, è illustrato come etouches toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df1b2-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df1b2-105">Integrazione etouches con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="df1b2-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df1b2-106">È possibile controllare in Azure AD che ha accesso tooetouches</span><span class="sxs-lookup"><span data-stu-id="df1b2-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="df1b2-107">È possibile abilitare l'utenti tooautomatically get connesso tooetouches (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df1b2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="df1b2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="df1b2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df1b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df1b2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="df1b2-110">Prerequisites</span></span>

<span data-ttu-id="df1b2-111">integrazione di Azure AD con etouches tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="df1b2-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="df1b2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df1b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df1b2-113">Sottoscrizione di etouches abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df1b2-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df1b2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="df1b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df1b2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="df1b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df1b2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="df1b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df1b2-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df1b2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df1b2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="df1b2-118">Scenario description</span></span>
<span data-ttu-id="df1b2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="df1b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df1b2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="df1b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df1b2-121">Aggiunta di etouches dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="df1b2-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="df1b2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="df1b2-123">Aggiunta di etouches dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="df1b2-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="df1b2-124">integrazione hello tooconfigure di etouches in Azure AD, è necessario etouches tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="df1b2-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df1b2-125">**etouches tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1b2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="df1b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="df1b2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df1b2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="df1b2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="df1b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="df1b2-133">Nella casella di ricerca hello, digitare **etouches**selezionare **etouches** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="df1b2-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df1b2-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="df1b2-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con etouches usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df1b2-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df1b2-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in etouches è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df1b2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="df1b2-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in etouches deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="df1b2-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="df1b2-139">In etouches, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df1b2-140">tooconfigure e prova AD Azure single sign-on con etouches, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="df1b2-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df1b2-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="df1b2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df1b2-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df1b2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df1b2-143">**[Creare un utente test etouches](#create-an-etouches-test-user)**  -toohave un equivalente di Britta Simon in etouches che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="df1b2-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df1b2-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="df1b2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df1b2-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="df1b2-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df1b2-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df1b2-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione etouches.</span><span class="sxs-lookup"><span data-stu-id="df1b2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="df1b2-148">**Azure AD tooconfigure single sign-on con etouches, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1b2-149">Nel portale di Azure su hello hello **etouches** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="df1b2-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="df1b2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="df1b2-153">In hello **etouches dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="df1b2-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="df1b2-155">a.</span><span class="sxs-lookup"><span data-stu-id="df1b2-155">a.</span></span> <span data-ttu-id="df1b2-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="df1b2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="df1b2-157">b.</span><span class="sxs-lookup"><span data-stu-id="df1b2-157">b.</span></span> <span data-ttu-id="df1b2-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="df1b2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df1b2-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="df1b2-159">These values are not real.</span></span> <span data-ttu-id="df1b2-160">Si aggiorna il valore di hello con hello effettivo accesso URL e l'identificatore, illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="df1b2-161">applicazione di etouches prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="df1b2-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="df1b2-162">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="df1b2-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="df1b2-163">È possibile gestire i valori hello di questi attributi da hello **attributo utente** di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="df1b2-164">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="df1b2-164">hello following screenshot shows an example for this.</span></span> 

    ![Attributo utente](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="df1b2-166">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="df1b2-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="df1b2-167">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="df1b2-167">Attribute Name</span></span> | <span data-ttu-id="df1b2-168">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="df1b2-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="df1b2-169">Email</span><span class="sxs-lookup"><span data-stu-id="df1b2-169">Email</span></span> | <span data-ttu-id="df1b2-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="df1b2-170">user.mail</span></span> |    
    
    <span data-ttu-id="df1b2-171">a.</span><span class="sxs-lookup"><span data-stu-id="df1b2-171">a.</span></span> <span data-ttu-id="df1b2-172">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="df1b2-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Aggiungi attributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Finestra di dialogo Aggiungi attributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="df1b2-175">b.</span><span class="sxs-lookup"><span data-stu-id="df1b2-175">b.</span></span> <span data-ttu-id="df1b2-176">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="df1b2-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="df1b2-177">c.</span><span class="sxs-lookup"><span data-stu-id="df1b2-177">c.</span></span> <span data-ttu-id="df1b2-178">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="df1b2-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="df1b2-179">d.</span><span class="sxs-lookup"><span data-stu-id="df1b2-179">d.</span></span> <span data-ttu-id="df1b2-180">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="df1b2-181">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="df1b2-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="df1b2-183">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="df1b2-183">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="df1b2-185">tooget SSO configurato per l'applicazione, attenersi alla procedura seguente in un'applicazione hello etouches hello:</span><span class="sxs-lookup"><span data-stu-id="df1b2-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![Configurazione di etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="df1b2-187">a.</span><span class="sxs-lookup"><span data-stu-id="df1b2-187">a.</span></span> <span data-ttu-id="df1b2-188">Account di accesso troppo**etouches** applicazione utilizzando i diritti di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="df1b2-189">b.</span><span class="sxs-lookup"><span data-stu-id="df1b2-189">b.</span></span> <span data-ttu-id="df1b2-190">Passare toohello **SAML** configurazione.</span><span class="sxs-lookup"><span data-stu-id="df1b2-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="df1b2-191">c.</span><span class="sxs-lookup"><span data-stu-id="df1b2-191">c.</span></span> <span data-ttu-id="df1b2-192">In hello **impostazioni generali** sezione, aprire il certificato scaricato dal portale di Azure nel blocco note, hello copia il contenuto e quindi incollarlo nella casella di testo hello IDP metadati.</span><span class="sxs-lookup"><span data-stu-id="df1b2-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="df1b2-193">d.</span><span class="sxs-lookup"><span data-stu-id="df1b2-193">d.</span></span> <span data-ttu-id="df1b2-194">Fare clic su hello **Salva e rimanere** pulsante.</span><span class="sxs-lookup"><span data-stu-id="df1b2-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="df1b2-195">e.</span><span class="sxs-lookup"><span data-stu-id="df1b2-195">e.</span></span> <span data-ttu-id="df1b2-196">Fare clic su hello **i metadati degli aggiornamenti** pulsante nella sezione dei metadati SAML hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="df1b2-197">f.</span><span class="sxs-lookup"><span data-stu-id="df1b2-197">f.</span></span> <span data-ttu-id="df1b2-198">Verrà visualizzata hello pagina ed esegue SSO.</span><span class="sxs-lookup"><span data-stu-id="df1b2-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="df1b2-199">Una volta hello SSO sta quindi è possibile impostare il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="df1b2-200">g.</span><span class="sxs-lookup"><span data-stu-id="df1b2-200">g.</span></span> <span data-ttu-id="df1b2-201">Nel campo nome utente hello selezionare hello **emailaddress** come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="df1b2-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="df1b2-202">h.</span><span class="sxs-lookup"><span data-stu-id="df1b2-202">h.</span></span> <span data-ttu-id="df1b2-203">Hello copia **ID entità SP** valore e incollarlo in hello **identificatore** casella di testo, ovvero in **etouches dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="df1b2-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="df1b2-204">i.</span><span class="sxs-lookup"><span data-stu-id="df1b2-204">i.</span></span> <span data-ttu-id="df1b2-205">Hello copia **URL SSO / ACS** valore e incollarlo in hello **URL di accesso** casella di testo, ovvero in **etouches dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="df1b2-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="df1b2-206">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="df1b2-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df1b2-207">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df1b2-208">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df1b2-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df1b2-209">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-209">Create an Azure AD test user</span></span>
<span data-ttu-id="df1b2-210">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="df1b2-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="df1b2-212">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1b2-213">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="df1b2-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df1b2-215">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df1b2-217">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df1b2-219">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="df1b2-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df1b2-221">a.</span><span class="sxs-lookup"><span data-stu-id="df1b2-221">a.</span></span> <span data-ttu-id="df1b2-222">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df1b2-223">b.</span><span class="sxs-lookup"><span data-stu-id="df1b2-223">b.</span></span> <span data-ttu-id="df1b2-224">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df1b2-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df1b2-225">c.</span><span class="sxs-lookup"><span data-stu-id="df1b2-225">c.</span></span> <span data-ttu-id="df1b2-226">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="df1b2-227">d.</span><span class="sxs-lookup"><span data-stu-id="df1b2-227">d.</span></span> <span data-ttu-id="df1b2-228">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="df1b2-229">Creare un utente di test di etouches</span><span class="sxs-lookup"><span data-stu-id="df1b2-229">Create an etouches test user</span></span>

<span data-ttu-id="df1b2-230">In questa sezione viene creato un utente di nome Britta Simon in etouches.</span><span class="sxs-lookup"><span data-stu-id="df1b2-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="df1b2-231">Lavorare con [team di supporto Client etouches](https://www.etouches.com/event-software/support/customer-support/) utenti hello tooadd nella piattaforma etouches hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="df1b2-232">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1b2-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="df1b2-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooetouches.</span><span class="sxs-lookup"><span data-stu-id="df1b2-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="df1b2-235">**tooassign Britta Simon tooetouches, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1b2-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="df1b2-238">Nell'elenco di applicazioni hello, selezionare **etouches**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-238">In hello applications list, select **etouches**.</span></span>

    ![Hello etouches collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="df1b2-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="df1b2-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-242">Click **Add** button.</span></span> <span data-ttu-id="df1b2-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="df1b2-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df1b2-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df1b2-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="df1b2-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="df1b2-248">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df1b2-248">Test single sign-on</span></span>


<span data-ttu-id="df1b2-249">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="df1b2-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df1b2-250">Quando si fa clic hello etouches riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour etouches applicazione.</span><span class="sxs-lookup"><span data-stu-id="df1b2-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df1b2-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="df1b2-251">Additional resources</span></span>

* [<span data-ttu-id="df1b2-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df1b2-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df1b2-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df1b2-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

