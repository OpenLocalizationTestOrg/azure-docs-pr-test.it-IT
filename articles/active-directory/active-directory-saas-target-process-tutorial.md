---
title: 'Esercitazione: Integrazione di Azure Active Directory con TargetProcess | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TargetProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="58fc5-103">Esercitazione: Integrazione di Azure Active Directory con TargetProcess</span><span class="sxs-lookup"><span data-stu-id="58fc5-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="58fc5-104">Questa esercitazione descrive come integrare TargetProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58fc5-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58fc5-105">L'integrazione di TargetProcess con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="58fc5-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58fc5-106">È possibile controllare in Azure AD chi può accedere a TargetProcess</span><span class="sxs-lookup"><span data-stu-id="58fc5-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="58fc5-107">È possibile abilitare gli utenti per l'accesso automatico a TargetProcess (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58fc5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58fc5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="58fc5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58fc5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58fc5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="58fc5-110">Prerequisites</span></span>

<span data-ttu-id="58fc5-111">Per configurare l'integrazione di Azure AD con TargetProcess, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="58fc5-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="58fc5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58fc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58fc5-113">Sottoscrizione di TargetProcess abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="58fc5-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58fc5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="58fc5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58fc5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="58fc5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58fc5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="58fc5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58fc5-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58fc5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58fc5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="58fc5-118">Scenario description</span></span>
<span data-ttu-id="58fc5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="58fc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58fc5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="58fc5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58fc5-121">Aggiungere TargetProcess dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="58fc5-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="58fc5-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="58fc5-123">Aggiungere TargetProcess dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="58fc5-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="58fc5-124">Per configurare l'integrazione di TargetProcess in Azure AD, è necessario aggiungere TargetProcess dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="58fc5-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58fc5-125">**Per aggiungere TargetProcess dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="58fc5-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58fc5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="58fc5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58fc5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58fc5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="58fc5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="58fc5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="58fc5-133">Nella casella di ricerca digitare **TargetProcess**, selezionare **TargetProcess** dal pannello dei risultati quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58fc5-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![Aggiungere TargetProcess dalla raccolta](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="58fc5-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="58fc5-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TargetProcess Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="58fc5-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58fc5-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di TargetProcess che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58fc5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="58fc5-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="58fc5-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="58fc5-139">Per stabilire la relazione di collegamento, in TargetProcess assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="58fc5-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con TargetProcess, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="58fc5-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58fc5-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="58fc5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58fc5-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58fc5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58fc5-143">**[Creare un utente di test per TargetProcess](#create-a-targetprocess-test-user)**: per avere una controparte di Britta Simon in TargetProcess collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58fc5-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="58fc5-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58fc5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58fc5-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="58fc5-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="58fc5-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="58fc5-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="58fc5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="58fc5-148">**Per configurare l'accesso Single Sign-On di Azure AD con TargetProcess, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="58fc5-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="58fc5-149">Nella pagina di integrazione dell'applicazione **TargetProcess** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="58fc5-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="58fc5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="58fc5-153">Nella sezione **URL e dominio TargetProcess** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="58fc5-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Sezione URL e dominio TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="58fc5-155">a.</span><span class="sxs-lookup"><span data-stu-id="58fc5-155">a.</span></span> <span data-ttu-id="58fc5-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.tpondemand.com/`.</span><span class="sxs-lookup"><span data-stu-id="58fc5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="58fc5-157">b.</span><span class="sxs-lookup"><span data-stu-id="58fc5-157">b.</span></span> <span data-ttu-id="58fc5-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="58fc5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58fc5-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="58fc5-159">These values are not real.</span></span> <span data-ttu-id="58fc5-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="58fc5-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="58fc5-161">Per ottenere questi valori, contattare il [team di supporto client di TargetProcess](mailto:support@targetprocess.com).</span><span class="sxs-lookup"><span data-stu-id="58fc5-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="58fc5-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="58fc5-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="58fc5-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="58fc5-164">Click **Save** button.</span></span>

    ![Pulsante Salva](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="58fc5-166">Nella sezione **Configurazione di TargetProcess** fare clic su **Configura TargetProcess** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="58fc5-167">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="58fc5-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sezione di configurazione di TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="58fc5-169">Accedere all'applicazione TargetProcess come amministratore.</span><span class="sxs-lookup"><span data-stu-id="58fc5-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="58fc5-170">Nel menu in alto fare clic su **Impostazione**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Configurazione](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="58fc5-172">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-172">Click **Settings**.</span></span>
   
    ![Impostazioni](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="58fc5-174">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-174">Click **Single Sign-on**.</span></span>
   
    ![fare clic su Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="58fc5-176">Nella finestra di dialogo delle impostazioni Single Sign-On seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="58fc5-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="58fc5-178">a.</span><span class="sxs-lookup"><span data-stu-id="58fc5-178">a.</span></span> <span data-ttu-id="58fc5-179">Fare clic su **Abilita Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="58fc5-180">b.</span><span class="sxs-lookup"><span data-stu-id="58fc5-180">b.</span></span> <span data-ttu-id="58fc5-181">Nella casella di testo **Sign on URL** (URL di accesso) incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58fc5-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="58fc5-182">c.</span><span class="sxs-lookup"><span data-stu-id="58fc5-182">c.</span></span> <span data-ttu-id="58fc5-183">Aprire il certificato scaricato nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo **Certificato** .</span><span class="sxs-lookup"><span data-stu-id="58fc5-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="58fc5-184">d.</span><span class="sxs-lookup"><span data-stu-id="58fc5-184">d.</span></span> <span data-ttu-id="58fc5-185">Fare clic su **Abilita Provisioning JIT**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="58fc5-186">e.</span><span class="sxs-lookup"><span data-stu-id="58fc5-186">e.</span></span> <span data-ttu-id="58fc5-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="58fc5-188">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="58fc5-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="58fc5-189">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="58fc5-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58fc5-190">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58fc5-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="58fc5-191">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-191">Create an Azure AD test user</span></span>
<span data-ttu-id="58fc5-192">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58fc5-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="58fc5-194">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="58fc5-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58fc5-195">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="58fc5-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58fc5-197">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="58fc5-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Per visualizzare l'elenco degli utenti](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58fc5-199">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58fc5-201">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="58fc5-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Sezione Utente](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58fc5-203">a.</span><span class="sxs-lookup"><span data-stu-id="58fc5-203">a.</span></span> <span data-ttu-id="58fc5-204">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58fc5-205">b.</span><span class="sxs-lookup"><span data-stu-id="58fc5-205">b.</span></span> <span data-ttu-id="58fc5-206">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="58fc5-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58fc5-207">c.</span><span class="sxs-lookup"><span data-stu-id="58fc5-207">c.</span></span> <span data-ttu-id="58fc5-208">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="58fc5-209">d.</span><span class="sxs-lookup"><span data-stu-id="58fc5-209">d.</span></span> <span data-ttu-id="58fc5-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="58fc5-211">Creare un utente test per TargetProcess</span><span class="sxs-lookup"><span data-stu-id="58fc5-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="58fc5-212">Questa sezione descrive come creare un utente chiamato Britta Simon in TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="58fc5-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="58fc5-213">TargetProcess supporta il provisioning JIT (just-in-time),</span><span class="sxs-lookup"><span data-stu-id="58fc5-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="58fc5-214">È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="58fc5-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="58fc5-215">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="58fc5-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="58fc5-216">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fc5-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="58fc5-217">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="58fc5-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Assegna utente][200] 

<span data-ttu-id="58fc5-219">**Per assegnare Britta Simon a TargetProcess, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="58fc5-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="58fc5-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="58fc5-222">Selezionare **TargetProcess**dall'elenco di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="58fc5-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess nell'elenco di app](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="58fc5-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="58fc5-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="58fc5-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-226">Click **Add** button.</span></span> <span data-ttu-id="58fc5-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="58fc5-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="58fc5-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="58fc5-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58fc5-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="58fc5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="58fc5-232">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="58fc5-232">Test single sign-on</span></span>

<span data-ttu-id="58fc5-233">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="58fc5-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="58fc5-234">Quando si fa clic sul riquadro TargetProcess nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="58fc5-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="58fc5-235">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58fc5-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58fc5-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="58fc5-236">Additional resources</span></span>

* [<span data-ttu-id="58fc5-237">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58fc5-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58fc5-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58fc5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

