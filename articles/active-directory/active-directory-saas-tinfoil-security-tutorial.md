---
title: 'Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="69b10-103">Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="69b10-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="69b10-104">In questa esercitazione, è illustrato come toointegrate TINFOIL SECURITY con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69b10-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69b10-105">Integrazione di TINFOIL SECURITY con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="69b10-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="69b10-106">È possibile controllare in Azure AD che ha accesso tooTINFOIL, sicurezza</span><span class="sxs-lookup"><span data-stu-id="69b10-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="69b10-107">È possibile abilitare l'utenti tooautomatically get connesso tooTINFOIL sicurezza (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69b10-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="69b10-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="69b10-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="69b10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69b10-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69b10-110">Prerequisites</span></span>

<span data-ttu-id="69b10-111">integrazione di Azure AD con TINFOIL SECURITY tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="69b10-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="69b10-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69b10-113">Sottoscrizione di TINFOIL SECURITY abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="69b10-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="69b10-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="69b10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="69b10-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="69b10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69b10-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="69b10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="69b10-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69b10-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="69b10-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="69b10-118">Scenario description</span></span>
<span data-ttu-id="69b10-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="69b10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69b10-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="69b10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69b10-121">Aggiungere TINFOIL SECURITY dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="69b10-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="69b10-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="69b10-123">Aggiungere TINFOIL SECURITY dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="69b10-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="69b10-124">integrazione hello tooconfigure di TINFOIL SECURITY in Azure AD, è necessario tooadd TINFOIL SECURITY dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="69b10-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="69b10-125">**tooadd TINFOIL SECURITY dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="69b10-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="69b10-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="69b10-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="69b10-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="69b10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="69b10-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="69b10-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="69b10-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="69b10-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="69b10-133">Nella casella di ricerca hello, digitare **TINFOIL SECURITY**selezionare **TINFOIL SECURITY** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="69b10-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY dalla raccolta](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="69b10-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="69b10-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TINFOIL SECURITY con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="69b10-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="69b10-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TINFOIL SECURITY è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b10-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="69b10-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TINFOIL SECURITY richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="69b10-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="69b10-139">In TINFOIL SECURITY, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="69b10-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="69b10-140">tooconfigure e prova AD Azure single sign-on con TINFOIL SECURITY, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="69b10-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="69b10-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="69b10-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="69b10-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="69b10-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="69b10-143">**[Creare un utente di test di TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un equivalente di Britta Simon in TINFOIL SECURITY che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="69b10-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="69b10-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="69b10-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69b10-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="69b10-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="69b10-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="69b10-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="69b10-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="69b10-148">**Azure AD tooconfigure single sign-on con TINFOIL SECURITY, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="69b10-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="69b10-149">Nel portale di Azure su hello hello **TINFOIL SECURITY** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="69b10-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="69b10-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="69b10-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="69b10-153">In hello **TINFOIL SECURITY dominio e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="69b10-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="69b10-155">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore.</span><span class="sxs-lookup"><span data-stu-id="69b10-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="69b10-157">mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="69b10-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="69b10-158">![Attributi](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="69b10-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="69b10-159">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="69b10-159">Attribute Name</span></span>    |   <span data-ttu-id="69b10-160">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="69b10-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="69b10-161">accountid</span><span class="sxs-lookup"><span data-stu-id="69b10-161">accountid</span></span> | <span data-ttu-id="69b10-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="69b10-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="69b10-163">a.</span><span class="sxs-lookup"><span data-stu-id="69b10-163">a.</span></span> <span data-ttu-id="69b10-164">Fare clic su **Aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="69b10-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="69b10-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="69b10-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="69b10-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="69b10-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="69b10-167">b.</span><span class="sxs-lookup"><span data-stu-id="69b10-167">b.</span></span> <span data-ttu-id="69b10-168">In hello **nome dell'attributo** casella tipo **accountid**.</span><span class="sxs-lookup"><span data-stu-id="69b10-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="69b10-169">c.</span><span class="sxs-lookup"><span data-stu-id="69b10-169">c.</span></span> <span data-ttu-id="69b10-170">In hello **valore dell'attributo** casella di testo, incollare hello ID valore dell'account che verrà visualizzato in un secondo momento esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="69b10-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="69b10-171">d.</span><span class="sxs-lookup"><span data-stu-id="69b10-171">d.</span></span> <span data-ttu-id="69b10-172">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="69b10-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="69b10-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="69b10-173">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="69b10-175">In hello **TINFOIL SECURITY Configuration** fare clic su **configurare TINFOIL SECURITY** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="69b10-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="69b10-176">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="69b10-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="69b10-178">In un'altra finestra del Web browser accedere al sito aziendale TINFOIL SECURITY come amministratore.</span><span class="sxs-lookup"><span data-stu-id="69b10-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="69b10-179">Nella barra degli strumenti hello in primo piano hello, fare clic su **Account personale**.</span><span class="sxs-lookup"><span data-stu-id="69b10-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="69b10-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="69b10-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="69b10-181">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="69b10-181">Click **Security**.</span></span>
   
    <span data-ttu-id="69b10-182">![Sicurezza](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="69b10-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="69b10-183">In hello **Single Sign-On** configurazione eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="69b10-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="69b10-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="69b10-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="69b10-185">a.</span><span class="sxs-lookup"><span data-stu-id="69b10-185">a.</span></span> <span data-ttu-id="69b10-186">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="69b10-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="69b10-187">b.</span><span class="sxs-lookup"><span data-stu-id="69b10-187">b.</span></span> <span data-ttu-id="69b10-188">Fare clic su **Configurazione manuale**.</span><span class="sxs-lookup"><span data-stu-id="69b10-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="69b10-189">c.</span><span class="sxs-lookup"><span data-stu-id="69b10-189">c.</span></span> <span data-ttu-id="69b10-190">In **SAML Post URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="69b10-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="69b10-191">d.</span><span class="sxs-lookup"><span data-stu-id="69b10-191">d.</span></span> <span data-ttu-id="69b10-192">In **SAML Certificate Fingerprint** casella di testo, hello Incolla valore **identificazione personale** che è stato copiato da **certificato di firma SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="69b10-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="69b10-193">e.</span><span class="sxs-lookup"><span data-stu-id="69b10-193">e.</span></span> <span data-ttu-id="69b10-194">Copia **Your Account ID** valore e incollare il valore di hello in **valore dell'attributo** casella di testo in **Aggiungi attributo** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="69b10-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="69b10-195">f.</span><span class="sxs-lookup"><span data-stu-id="69b10-195">f.</span></span> <span data-ttu-id="69b10-196">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="69b10-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="69b10-197">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="69b10-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="69b10-198">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="69b10-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="69b10-199">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="69b10-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="69b10-200">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-200">Create an Azure AD test user</span></span>
<span data-ttu-id="69b10-201">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="69b10-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="69b10-203">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="69b10-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="69b10-204">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="69b10-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69b10-206">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="69b10-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="69b10-207">Utenti e gruppi -> Tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="69b10-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69b10-208">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="69b10-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Utente](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69b10-210">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="69b10-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69b10-212">a.</span><span class="sxs-lookup"><span data-stu-id="69b10-212">a.</span></span> <span data-ttu-id="69b10-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="69b10-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69b10-214">b.</span><span class="sxs-lookup"><span data-stu-id="69b10-214">b.</span></span> <span data-ttu-id="69b10-215">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="69b10-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69b10-216">c.</span><span class="sxs-lookup"><span data-stu-id="69b10-216">c.</span></span> <span data-ttu-id="69b10-217">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="69b10-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="69b10-218">d.</span><span class="sxs-lookup"><span data-stu-id="69b10-218">d.</span></span> <span data-ttu-id="69b10-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="69b10-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="69b10-220">Creare un utente test di TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="69b10-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="69b10-221">In ordine tooenable Azure AD utenti toolog a TINFOIL SECURITY, è necessario eseguirne il provisioning in TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="69b10-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="69b10-222">Nel caso di hello di TINFOIL SECURITY, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="69b10-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="69b10-223">**tooget viene eseguito il provisioning, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="69b10-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="69b10-224">Se l'utente hello fa parte di un account aziendale, è necessario troppo[contattare il team di supporto di TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) account utente di hello tooget creato.</span><span class="sxs-lookup"><span data-stu-id="69b10-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="69b10-225">Se l'utente di hello è un normale utente SaaS di TINFOIL SECURITY, utente hello aggiungere tooany un collaboratore del sito hello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="69b10-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="69b10-226">Questo trigger toosend un processo specificato toohello un invito tramite posta elettronica toocreate un nuovo account utente TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="69b10-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="69b10-227">È possibile usare qualsiasi altro TINFOIL SECURITY utente account strumento di creazione o le API fornite da TINFOIL SECURITY tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b10-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="69b10-228">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="69b10-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="69b10-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTINFOIL sicurezza.</span><span class="sxs-lookup"><span data-stu-id="69b10-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Assegna utente][200] 

<span data-ttu-id="69b10-231">**tooassign Britta Simon tooTINFOIL protezione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="69b10-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="69b10-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="69b10-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="69b10-234">Nell'elenco di applicazioni hello, selezionare **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="69b10-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![selezionare TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="69b10-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="69b10-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="69b10-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="69b10-238">Click **Add** button.</span></span> <span data-ttu-id="69b10-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="69b10-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="69b10-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="69b10-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="69b10-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="69b10-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69b10-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="69b10-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="69b10-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="69b10-244">Test single sign-on</span></span>

<span data-ttu-id="69b10-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="69b10-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="69b10-246">Quando si fa clic su riquadro TINFOIL SECURITY hello in hello Pannello di accesso, è necessario ottenere applicazione TINFOIL SECURITY tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="69b10-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="69b10-247">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="69b10-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69b10-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="69b10-248">Additional resources</span></span>

* [<span data-ttu-id="69b10-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69b10-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69b10-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69b10-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

