---
title: 'Esercitazione: Eseguire l''integrazione di Azure Active Directory con vxMaintain | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="ea3b5-103">Esercitazione: Eseguire l'integrazione di Azure Active Directory con vxMaintain</span><span class="sxs-lookup"><span data-stu-id="ea3b5-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="ea3b5-104">Questa esercitazione descrive come integrare vxMaintain con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea3b5-105">Questa integrazione offre diversi vantaggi importanti.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-105">This integration provides several important benefits.</span></span> <span data-ttu-id="ea3b5-106">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-106">You can:</span></span>

- <span data-ttu-id="ea3b5-107">È possibile controllare in Azure AD chi può accedere a vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="ea3b5-108">È possibile abilitare gli utenti per l'accesso automatico a vxMaintain (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="ea3b5-109">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="ea3b5-110">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea3b5-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ea3b5-111">Prerequisites</span></span>

<span data-ttu-id="ea3b5-112">Per configurare l'integrazione di Azure AD con vxMaintain, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="ea3b5-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ea3b5-114">Sottoscrizione di vxMaintain abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="ea3b5-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea3b5-115">Per testare i passaggi di questa esercitazione non è consigliabile usare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="ea3b5-116">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ea3b5-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea3b5-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea3b5-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ea3b5-119">Scenario description</span></span>
<span data-ttu-id="ea3b5-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ea3b5-121">Lo scenario descritto in questa esercitazione prevede le due procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="ea3b5-122">Aggiunta di vxMaintain dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ea3b5-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="ea3b5-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="ea3b5-124">Aggiungere vxMaintain dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ea3b5-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="ea3b5-125">Per configurare l'integrazione di vxMaintain in Azure AD, è necessario aggiungere vxMaintain dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea3b5-126">Per aggiungere vxMaintain dalla raccolta, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="ea3b5-127">Nel [portale di Azure](https://portal.azure.com) fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="ea3b5-129">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Riquadro "Applicazioni aziendali"][2]
    
3. <span data-ttu-id="ea3b5-131">Per aggiungere un'applicazione, fare clic su **Nuova applicazione** nella finestra di dialogo **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![Pulsante "Nuova applicazione"][3]

4. <span data-ttu-id="ea3b5-133">Nella casella di ricerca digitare **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-133">In the search box, type **vxMaintain**.</span></span>

    ![Elenco a discesa "Modalità Single Sign-On"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="ea3b5-135">Nell'elenco risultati, selezionare **vxMaintain** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Collegamento di vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ea3b5-137">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ea3b5-138">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con vxMaintain usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ea3b5-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea3b5-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di vxMaintain corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="ea3b5-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="ea3b5-141">Per stabilire la relazione di collegamento, in vxMaintain assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="ea3b5-142">Per configurare e testare l'accesso SSO di Azure AD con vxMaintain, è necessario completare le procedure di base seguenti.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ea3b5-143">Configurare l'accesso SSO di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="ea3b5-144">In questa sezione è possibile abilitare l'accesso SSO di Azure AD nel portale di Azure e configurare l'accesso SSO nell'applicazione vxMaintain seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="ea3b5-145">Nella pagina di integrazione dell'applicazione **vxMaintain** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Comando "Single Sign-On"][4]

2. <span data-ttu-id="ea3b5-147">Nell'elenco a discesa **Modalità Single Sign-On** selezionare **Accesso basato su SAML** per abilitare l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Comando "Accesso basato su SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="ea3b5-149">In **URL e dominio vxMaintain** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![Sezione URL e dominio vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="ea3b5-151">a.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-151">a.</span></span> <span data-ttu-id="ea3b5-152">Nella casella **Identificatore** digitare un URL con la sintassi seguente: `https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="ea3b5-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="ea3b5-153">b.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-153">b.</span></span> <span data-ttu-id="ea3b5-154">Nella casella **URL di risposta** digitare un URL con la sintassi seguente: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="ea3b5-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea3b5-155">I valori precedenti non sono valori reali.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-155">The preceding values are not real.</span></span> <span data-ttu-id="ea3b5-156">Aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="ea3b5-157">Per ottenere questi valori, contattare il [team di supporto di vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="ea3b5-158">In **Certificato di firma SAML** selezionare **XML metadati** e quindi salvare il file di metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![Sezione "Certificato di firma SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="ea3b5-160">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-160">Select **Save**.</span></span>

    ![Pulsante Salva](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea3b5-162">Per configurare l'accesso SSO di **vxMaintain**, inviare il file **XML metadati** scaricato al [team di supporto di vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="ea3b5-163">Durante la configurazione dell'app, nel [portale di Azure](https://portal.azure.com) è disponibile un riepilogo delle istruzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ea3b5-164">Dopo aver aggiunto l'app dalla sezione **Active Directory** > **Applicazioni aziendali**, selezionare la scheda **Single Sign-On** e accedere alla documentazione incorporata dalla sezione **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="ea3b5-165">Per altre informazioni sulla funzionalità di documentazione incorporata vedere [Gestione dell'accesso Single Sign-On per le app aziendali](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ea3b5-166">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-166">Create an Azure AD test user</span></span>
<span data-ttu-id="ea3b5-167">In questa sezione si crea un utente di test Britta Simon nel portale di Azure seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Utente di test di Azure AD][100]

1. <span data-ttu-id="ea3b5-169">Nel **portale di Azure** fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Pulsante "Azure Active Directory"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea3b5-171">Per visualizzare un elenco di utenti, passare a **Utenti e gruppi** > **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="ea3b5-172">![Collegamento "Tutti gli utenti"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="ea3b5-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="ea3b5-173">Verrà visualizzata la finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="ea3b5-174">Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea3b5-176">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-176">In the **User** dialog box, do the following:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea3b5-178">a.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-178">a.</span></span> <span data-ttu-id="ea3b5-179">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea3b5-180">b.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-180">b.</span></span> <span data-ttu-id="ea3b5-181">Nella casella **Nome utente** digitare l'indirizzo e-mail dell'utente di test Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="ea3b5-182">c.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-182">c.</span></span> <span data-ttu-id="ea3b5-183">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore generato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="ea3b5-184">d.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-184">d.</span></span> <span data-ttu-id="ea3b5-185">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="ea3b5-186">Creare un utente di test di vxMaintain</span><span class="sxs-lookup"><span data-stu-id="ea3b5-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="ea3b5-187">In questa sezione viene creato un utente di test di nome Britta Simon in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="ea3b5-188">Collaborare con il [team di supporto di vxMaintain](http://www.verisae.com/contact-us) per aggiungere gli utenti alla piattaforma vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="ea3b5-189">Prima di usare l'accesso SSO, creare e attivare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ea3b5-190">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="ea3b5-191">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="ea3b5-192">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ea3b5-192">To do so, do the following:</span></span>

![Utente di test nell'elenco Nome visualizzato][200] 

1. <span data-ttu-id="ea3b5-194">Nella visualizzazione **Applicazioni** del portale di Azure passare a visualizzazione **Directory** > **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Collegamento "Tutte le applicazioni"][201] 

2. <span data-ttu-id="ea3b5-196">Nell'elenco **Applicazioni** selezionare **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![Collegamento di vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="ea3b5-198">Nel riquadro sinistro fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-198">In the left pane, select **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="ea3b5-200">Fare clic su **Aggiungi** e quindi nel riquadro **Aggiungi assegnazione** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][203]

5. <span data-ttu-id="ea3b5-202">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco **Utenti** e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="ea3b5-203">Nella finestra di dialogo **Aggiungi assegnazione** selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="ea3b5-204">Testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea3b5-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="ea3b5-205">In questa sezione viene testata la configurazione dell'accesso SSO di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="ea3b5-206">Quando si fa clic sul riquadro **vxMaintain** nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="ea3b5-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="ea3b5-207">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea3b5-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea3b5-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea3b5-208">Next steps</span></span>

* [<span data-ttu-id="ea3b5-209">Elenco di esercitazioni sull'integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea3b5-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea3b5-210">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea3b5-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

