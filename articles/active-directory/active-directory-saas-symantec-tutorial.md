---
title: 'Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e servizio di sicurezza Web Symantec (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="3e511-103">Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="3e511-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="3e511-104">In questa esercitazione si apprenderà come toointegrate il servizio di sicurezza Web Symantec (WSS) account con il proprio account Azure Active Directory (Azure AD) in modo da WSS può autenticare un utente finale il provisioning in hello Azure AD utilizzando l'autenticazione SAML e applicare l'utente o regole di livello dei criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3e511-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="3e511-105">Integrazione del servizio di sicurezza Web Symantec (WSS) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3e511-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e511-106">Gestire tutti gli utenti finali di hello e i gruppi utilizzati per l'account WSS dal portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e511-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="3e511-107">Consentire tooauthenticate gli utenti finali di hello WSS utilizzando le proprie credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e511-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="3e511-108">Abilitare l'applicazione hello di utente e gruppo di regole di livello dei criteri definite nell'account di WSS.</span><span class="sxs-lookup"><span data-stu-id="3e511-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="3e511-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e511-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e511-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e511-110">Prerequisites</span></span>

<span data-ttu-id="3e511-111">tooconfigure integrazione di Azure AD con Symantec Web Security Service (WSS), è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3e511-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="3e511-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e511-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e511-113">Account Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="3e511-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="3e511-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un account WSS utilizzato a scopo di produzione.</span><span class="sxs-lookup"><span data-stu-id="3e511-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="3e511-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3e511-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e511-116">Non usare per i test un account WSS attualmente in uso nell'ambiente di produzione, a meno che ciò non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3e511-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="3e511-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e511-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e511-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3e511-118">Scenario description</span></span>
<span data-ttu-id="3e511-119">In questa esercitazione, configurare il AD Azure tooenable single sign-on tooWSS utilizzando le credenziali utente finale di hello definite nell'account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e511-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="3e511-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3e511-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e511-121">Aggiunta di applicazione di servizio di sicurezza Web Symantec (WSS) hello dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e511-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="3e511-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e511-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="3e511-123">Aggiunta del servizio di sicurezza Web Symantec (WSS) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e511-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="3e511-124">integrazione di hello di tooconfigure Symantec Web Security Service (WSS) in Azure AD, è necessario tooadd Symantec Web Security Service (WSS) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3e511-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e511-125">**tooadd Symantec Web Security Service (WSS) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e511-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e511-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e511-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="3e511-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3e511-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e511-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e511-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="3e511-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e511-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="3e511-133">Nella casella di ricerca hello, digitare **Symantec Web Security Service (WSS)**selezionare **Symantec Web Security Service (WSS)** dal pannello risultati quindi fare clic su **Aggiungi** hello tooadd pulsante applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e511-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Web Security Service (WSS) nell'elenco risultati hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3e511-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e511-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3e511-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS) usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e511-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e511-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Symantec Web Security Service (WSS) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e511-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="3e511-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Symantec Web Security Service (WSS) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3e511-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="3e511-139">In Symantec Web Security Service (WSS), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="3e511-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e511-140">tooconfigure e test di Azure AD single sign-on con Symantec Web Security Service (WSS), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3e511-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e511-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3e511-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e511-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e511-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e511-143">**[Creare un utente di test del servizio di sicurezza Web Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente di Britta Simon in Symantec Web Security Service (WSS) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3e511-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e511-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e511-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e511-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e511-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3e511-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e511-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3e511-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione del servizio di sicurezza Web Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="3e511-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="3e511-148">**tooconfigure AD Azure single sign-on con Symantec Web Security Service (WSS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e511-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="3e511-149">Nel portale di Azure su hello hello **Symantec Web Security Service (WSS)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e511-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="3e511-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e511-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="3e511-153">In hello **URL e dominio del servizio (WSS) sicurezza Web Symantec** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e511-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="3e511-155">a.</span><span class="sxs-lookup"><span data-stu-id="3e511-155">a.</span></span> <span data-ttu-id="3e511-156">In hello **identificatore** casella di testo, digitare l'URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="3e511-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="3e511-157">b.</span><span class="sxs-lookup"><span data-stu-id="3e511-157">b.</span></span> <span data-ttu-id="3e511-158">In hello **URL di risposta** casella di testo, digitare l'URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="3e511-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e511-159">Contattare hello [team di supporto Client di servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) se i valori hello per hello **identificatore** e **URL di risposta** non funzionano per qualche motivo.</span><span class="sxs-lookup"><span data-stu-id="3e511-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="3e511-160">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3e511-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="3e511-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e511-162">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3e511-164">tooconfigure single sign-on sul hello lato servizio di sicurezza Web Symantec (WSS), consultare la documentazione online di toohello WSS.</span><span class="sxs-lookup"><span data-stu-id="3e511-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="3e511-165">Hello scaricato **Metadata XML** file sarà necessario toobe importati nel portale WSS hello.</span><span class="sxs-lookup"><span data-stu-id="3e511-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="3e511-166">Contatto hello [team di supporto del servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) assistenza con la configurazione nel portale WSS hello hello.</span><span class="sxs-lookup"><span data-stu-id="3e511-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="3e511-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="3e511-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e511-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3e511-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e511-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e511-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3e511-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e511-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3e511-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e511-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="3e511-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e511-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e511-174">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3e511-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3e511-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3e511-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3e511-178">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e511-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3e511-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e511-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3e511-182">a.</span><span class="sxs-lookup"><span data-stu-id="3e511-182">a.</span></span> <span data-ttu-id="3e511-183">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e511-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e511-184">b.</span><span class="sxs-lookup"><span data-stu-id="3e511-184">b.</span></span> <span data-ttu-id="3e511-185">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e511-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3e511-186">c.</span><span class="sxs-lookup"><span data-stu-id="3e511-186">c.</span></span> <span data-ttu-id="3e511-187">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="3e511-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3e511-188">d.</span><span class="sxs-lookup"><span data-stu-id="3e511-188">d.</span></span> <span data-ttu-id="3e511-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3e511-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="3e511-190">Creare un utente di test di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="3e511-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="3e511-191">In questa sezione viene creato un utente di nome Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="3e511-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="3e511-192">nome utente di fine corrispondente Hello può essere creato manualmente nel portale WSS hello o è possibile attendere hello utenti o gruppi è stato eseguito il provisioning nel portale di hello Azure AD sincronizzati toobe toohello WSS dopo pochi minuti (~ 15 minuti).</span><span class="sxs-lookup"><span data-stu-id="3e511-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="3e511-193">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3e511-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="3e511-194">indirizzo IP pubblico di Hello del computer di utenti hello, che sarà siti Web toobrowse usato è inoltre necessario toobe il provisioning nel portale di hello Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="3e511-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3e511-195">. [Fare clic qui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget del computer pubblico IPaddress.</span><span class="sxs-lookup"><span data-stu-id="3e511-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3e511-196">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e511-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3e511-197">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSymantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="3e511-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="3e511-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e511-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="3e511-200">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e511-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3e511-202">Nell'elenco di applicazioni hello, selezionare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="3e511-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![collegamento di Hello Symantec Web Security Service (WSS) nell'elenco delle applicazioni hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="3e511-204">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e511-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="3e511-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e511-206">Click **Add** button.</span></span> <span data-ttu-id="3e511-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e511-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="3e511-209">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3e511-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e511-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e511-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e511-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e511-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3e511-212">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e511-212">Test single sign-on</span></span>

<span data-ttu-id="3e511-213">In questa sezione verrà testato funzionalità hello single sign-on dopo aver configurato il toouse account WSS Azure AD per l'autenticazione SAML.</span><span class="sxs-lookup"><span data-stu-id="3e511-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="3e511-214">Dopo aver configurato il traffico tooproxy del browser web tooWSS, quando si apre il browser e prova toobrowse tooa sito, quindi si verrà reindirizzati pagina toohello Azure sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e511-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="3e511-215">Immettere le credenziali di hello dell'utente finale di prova hello che è stato eseguito il provisioning in hello Azure AD (vale a dire BrittaSimon) e la password associata.</span><span class="sxs-lookup"><span data-stu-id="3e511-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="3e511-216">Una volta autenticato, sarà in grado di toobrowse sito Web di toohello scelto.</span><span class="sxs-lookup"><span data-stu-id="3e511-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="3e511-217">È necessario creare una regola dei criteri in hello WSS lato tooblock BrittaSimon dal sito tooa particolare è possibile vedere hello WSS blocco pagina quando si tenta di toobrowse toothat sito come utente BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e511-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e511-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3e511-218">Additional resources</span></span>

* [<span data-ttu-id="3e511-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e511-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e511-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e511-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

