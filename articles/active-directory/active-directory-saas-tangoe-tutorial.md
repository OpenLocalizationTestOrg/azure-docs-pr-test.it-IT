---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tangoe Command Premium Mobile | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Tangoe comando Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="28628-103">Esercitazione: Integrazione di Azure Active Directory con Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="28628-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="28628-104">In questa esercitazione, è illustrato come toointegrate Tangoe comando Premium per dispositivi mobili con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28628-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28628-105">Integrazione Tangoe comando Premium mobili con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="28628-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28628-106">È possibile controllare in Azure AD che ha accesso tooTangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="28628-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="28628-107">È possibile abilitare l'utenti tooautomatically get connesso tooTangoe comando Premium Mobile (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28628-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28628-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28628-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28628-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28628-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="28628-110">Prerequisites</span></span>

<span data-ttu-id="28628-111">integrazione di Azure AD con Tangoe comando Premium Mobile tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="28628-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="28628-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28628-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28628-113">Sottoscrizione di Tangoe Command Premium Mobile abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="28628-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28628-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="28628-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28628-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="28628-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28628-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="28628-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28628-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28628-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28628-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="28628-118">Scenario description</span></span>
<span data-ttu-id="28628-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="28628-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28628-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="28628-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28628-121">Aggiungere Tangoe comando Premium Mobile dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="28628-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="28628-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="28628-123">Aggiungere Tangoe comando Premium Mobile dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="28628-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="28628-124">integrazione hello tooconfigure di Tangoe comando Premium Mobile in Azure AD, è necessario tooadd Tangoe comando Premium Mobile dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="28628-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28628-125">**tooadd Tangoe comando Premium Mobile dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="28628-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28628-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="28628-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28628-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="28628-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28628-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="28628-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="28628-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="28628-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="28628-133">Nella casella di ricerca hello, digitare **Tangoe comando Premium Mobile**selezionare **Tangoe comando Premium Mobile** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="28628-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="28628-134">Aggiungere Tangoe Command Premium Mobile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="28628-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="28628-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="28628-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tangoe Command Premium Mobile con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28628-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28628-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Tangoe comando Premium Mobile è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28628-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="28628-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Tangoe comando Premium Mobile deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="28628-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="28628-139">In Tangoe comando Premium Mobile, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="28628-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="28628-140">tooconfigure e prova AD Azure single sign-on con Tangoe comando Premium Mobile, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="28628-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28628-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="28628-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28628-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28628-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28628-143">**[Creare un utente test Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave un equivalente di Britta Simon in Tangoe comando Premium Mobile che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="28628-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28628-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="28628-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28628-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="28628-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="28628-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="28628-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Tangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="28628-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="28628-148">**tooconfigure AD Azure single sign-on con Tangoe comando Premium Mobile, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="28628-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="28628-149">Nel portale di Azure su hello hello **Tangoe comando Premium Mobile** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="28628-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="28628-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="28628-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="28628-153">In hello **Tangoe comando Premium Mobile dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="28628-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![URL e dominio Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="28628-155">a.</span><span class="sxs-lookup"><span data-stu-id="28628-155">a.</span></span> <span data-ttu-id="28628-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="28628-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="28628-157">b.</span><span class="sxs-lookup"><span data-stu-id="28628-157">b.</span></span> <span data-ttu-id="28628-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="28628-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28628-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="28628-159">These values are not real.</span></span> <span data-ttu-id="28628-160">Aggiornare questi valori con l'URL di risposta effettivo hello e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="28628-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="28628-161">Contatto [team di supporto Client di dispositivi mobili Premium comando Tangoe](https://www.tangoe.com/contact-2/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="28628-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="28628-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="28628-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="28628-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="28628-164">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="28628-166">In hello **configurazione per dispositivi mobili Premium comando Tangoe** fare clic su **configurare Tangoe comando Premium Mobile** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="28628-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="28628-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="28628-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sezione di configurazione di Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="28628-169">tooget SSO è configurato per l'applicazione, contattare il [team di supporto Client di dispositivi mobili Tangoe comando Premium](https://www.tangoe.com/contact-2/) e fornire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="28628-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="28628-170">file di metadati scaricato Hello</span><span class="sxs-lookup"><span data-stu-id="28628-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="28628-171">Hello **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="28628-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="28628-172">Hello **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="28628-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="28628-173">Hello **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="28628-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="28628-174">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="28628-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28628-175">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="28628-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28628-176">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28628-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="28628-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-177">Create an Azure AD test user</span></span>
<span data-ttu-id="28628-178">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="28628-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="28628-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="28628-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28628-181">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="28628-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28628-183">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="28628-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28628-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="28628-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Add user](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28628-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="28628-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28628-189">a.</span><span class="sxs-lookup"><span data-stu-id="28628-189">a.</span></span> <span data-ttu-id="28628-190">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28628-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28628-191">b.</span><span class="sxs-lookup"><span data-stu-id="28628-191">b.</span></span> <span data-ttu-id="28628-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28628-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28628-193">c.</span><span class="sxs-lookup"><span data-stu-id="28628-193">c.</span></span> <span data-ttu-id="28628-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="28628-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28628-195">d.</span><span class="sxs-lookup"><span data-stu-id="28628-195">d.</span></span> <span data-ttu-id="28628-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="28628-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="28628-197">Creare un utente di test di Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="28628-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="28628-198">In questa sezione viene creato un utente chiamato Britta Simon in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="28628-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="28628-199">Applicazione Tangoe comando Premium Mobile deve tutti toobe agli utenti di hello eseguito il provisioning in un'applicazione hello prima di eseguire Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="28628-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="28628-200">Pertanto si prega di lavoro con hello [team di supporto Client di dispositivi mobili Premium comando Tangoe](https://www.tangoe.com/contact-2/) tooprovision tutti questi utenti in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="28628-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="28628-201">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28628-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="28628-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="28628-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Assegna utente][200] 

<span data-ttu-id="28628-204">**tooassign Britta Simon tooTangoe Mobile Premium di comando, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="28628-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="28628-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="28628-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="28628-207">Nell'elenco di applicazioni hello, selezionare **Tangoe comando Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="28628-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile nell'elenco delle app](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="28628-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="28628-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="28628-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="28628-211">Click **Add** button.</span></span> <span data-ttu-id="28628-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="28628-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="28628-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="28628-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28628-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="28628-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28628-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="28628-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="28628-217">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="28628-217">Test single sign-on</span></span>

<span data-ttu-id="28628-218">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="28628-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="28628-219">Quando si fa clic su riquadro Tangoe comando Premium Mobile hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Tangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="28628-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="28628-220">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28628-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="28628-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="28628-221">Additional resources</span></span>

* [<span data-ttu-id="28628-222">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28628-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28628-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28628-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

