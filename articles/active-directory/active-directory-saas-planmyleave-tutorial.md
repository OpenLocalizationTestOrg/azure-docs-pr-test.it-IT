---
title: 'Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="432f2-103">Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="432f2-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="432f2-104">Questa esercitazione descrive come integrare PlanMyLeave con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="432f2-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="432f2-105">L'integrazione di PlanMyLeave con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="432f2-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="432f2-106">È possibile controllare in Azure AD chi può accedere a PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="432f2-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="432f2-107">È possibile abilitare gli utenti per l'accesso automatico a PlanMyLeave (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="432f2-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="432f2-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="432f2-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="432f2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="432f2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="432f2-110">Prerequisites</span></span>

<span data-ttu-id="432f2-111">Per configurare l'integrazione di Azure AD con PlanMyLeave, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="432f2-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="432f2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="432f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="432f2-113">Sottoscrizione di PlanMyLeave abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="432f2-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="432f2-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="432f2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="432f2-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="432f2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="432f2-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="432f2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="432f2-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="432f2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="432f2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="432f2-118">Scenario description</span></span>
<span data-ttu-id="432f2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="432f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="432f2-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="432f2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="432f2-121">Aggiunta di PlanMyLeave dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="432f2-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="432f2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="432f2-123">Aggiunta di PlanMyLeave dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="432f2-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="432f2-124">Per configurare l'integrazione di PlanMyLeave in Azure AD, è necessario aggiungere PlanMyLeave dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="432f2-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="432f2-125">**Per aggiungere PlanMyLeave dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="432f2-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="432f2-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="432f2-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="432f2-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="432f2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="432f2-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="432f2-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="432f2-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="432f2-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="432f2-133">Nella casella di ricerca digitare **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="432f2-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="432f2-135">Nel pannello dei risultati selezionare **PlanMyLeave** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="432f2-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="432f2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="432f2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PlanMyLeave in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="432f2-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="432f2-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di PlanMyLeave che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="432f2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="432f2-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="432f2-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="432f2-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PlanMyLeave, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="432f2-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="432f2-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="432f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="432f2-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="432f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="432f2-145">**[Creazione di un utente test di PlanMyLeave](#creating-a-planmyleave-test-user)**: per avere una controparte di Britta Simon in PlanMyLeave collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="432f2-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="432f2-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="432f2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="432f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="432f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="432f2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="432f2-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="432f2-150">**Per configurare l'accesso Single Sign-On di Azure AD con PlanMyLeave, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="432f2-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="432f2-151">Nella pagina di integrazione dell'applicazione **PlanMyLeave** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="432f2-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="432f2-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="432f2-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="432f2-155">Nella sezione **URL e dominio PlanMyLeave** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="432f2-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="432f2-157">a.</span><span class="sxs-lookup"><span data-stu-id="432f2-157">a.</span></span> <span data-ttu-id="432f2-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="432f2-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="432f2-159">b.</span><span class="sxs-lookup"><span data-stu-id="432f2-159">b.</span></span> <span data-ttu-id="432f2-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="432f2-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="432f2-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="432f2-161">Please note that these are not the real values.</span></span> <span data-ttu-id="432f2-162">È necessario aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="432f2-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="432f2-163">Per ottenere questi valori, contattare il [team di supporto di PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="432f2-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="432f2-164">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="432f2-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="432f2-166">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="432f2-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="432f2-167">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="432f2-167">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="432f2-169">Nella sezione **Certificato di firma SAML** selezionare **Make new certificate active** (Rendi attivo il nuovo certificato) e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="432f2-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="432f2-171">Nella finestra popup **Rollover certificate** (Certificato di rollover) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="432f2-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="432f2-173">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="432f2-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="432f2-175">Nella sezione **Configurazione di PlanMyLeave** fare clic su **Configura PlanMyLeave** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="432f2-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="432f2-178">In un'altra finestra del browser Web accedere al tenant di PlanMyLeave come amministratore.</span><span class="sxs-lookup"><span data-stu-id="432f2-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="432f2-179">Passare a **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="432f2-179">Go to **System Setup**.</span></span> <span data-ttu-id="432f2-180">Quindi nella sezione **Gestione sicurezza** fare clic su **Company SAML settings** (Impostazioni SAML azienda).</span><span class="sxs-lookup"><span data-stu-id="432f2-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="432f2-182">Nella sezione **SAML Settings** (Impostazioni SAML) fare clic sull'icona dell'editor.</span><span class="sxs-lookup"><span data-stu-id="432f2-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="432f2-184">Nella sezione **Update SAML Settings** (Aggiorna impostazioni SAML) eseguire i seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="432f2-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="432f2-186">a.</span><span class="sxs-lookup"><span data-stu-id="432f2-186">a.</span></span>  <span data-ttu-id="432f2-187">Nella casella di testo **Login URL** (URL di accesso) inserire il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) dalla finestra di configurazione dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="432f2-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="432f2-188">b.</span><span class="sxs-lookup"><span data-stu-id="432f2-188">b.</span></span>  <span data-ttu-id="432f2-189">Aprire il certificato scaricato nel Blocco note, copiarne solo il contenuto fra ---Begin Certificate--- ed ---End certificate---- negli Appunti e incollarlo nella casella di testo **Certificato**.</span><span class="sxs-lookup"><span data-stu-id="432f2-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="432f2-190">c.</span><span class="sxs-lookup"><span data-stu-id="432f2-190">c.</span></span> <span data-ttu-id="432f2-191">Impostare "**Is Enable**" su "**Yes**".</span><span class="sxs-lookup"><span data-stu-id="432f2-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="432f2-192">d.</span><span class="sxs-lookup"><span data-stu-id="432f2-192">d.</span></span> <span data-ttu-id="432f2-193">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="432f2-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="432f2-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="432f2-195">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="432f2-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="432f2-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="432f2-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="432f2-198">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="432f2-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="432f2-200">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="432f2-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="432f2-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="432f2-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="432f2-204">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="432f2-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="432f2-206">a.</span><span class="sxs-lookup"><span data-stu-id="432f2-206">a.</span></span> <span data-ttu-id="432f2-207">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="432f2-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="432f2-208">b.</span><span class="sxs-lookup"><span data-stu-id="432f2-208">b.</span></span> <span data-ttu-id="432f2-209">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="432f2-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="432f2-210">c.</span><span class="sxs-lookup"><span data-stu-id="432f2-210">c.</span></span> <span data-ttu-id="432f2-211">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="432f2-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="432f2-212">d.</span><span class="sxs-lookup"><span data-stu-id="432f2-212">d.</span></span> <span data-ttu-id="432f2-213">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="432f2-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="432f2-214">Creazione di un utente test di PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="432f2-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="432f2-215">Questa sezione descrive come creare un utente chiamato Britta Simon in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="432f2-216">PlanMyLeave supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="432f2-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="432f2-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="432f2-217">There is no action item for you in this section.</span></span> <span data-ttu-id="432f2-218">Durante un tentativo di accesso a PlanMyLeave verrà creato un nuovo utente se questo non è già esistente.</span><span class="sxs-lookup"><span data-stu-id="432f2-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="432f2-219">Per creare un utente manualmente, è necessario contattare il [team di supporto di PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="432f2-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="432f2-220">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="432f2-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="432f2-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure, concedendole l'accesso a PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Assegna utente][200] 

<span data-ttu-id="432f2-223">**Per assegnare Britta Simon a PlanMyLeave, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="432f2-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="432f2-224">Nel portale di gestione di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="432f2-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="432f2-226">Nell'elenco di applicazioni selezionare **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="432f2-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="432f2-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="432f2-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="432f2-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="432f2-230">Click **Add** button.</span></span> <span data-ttu-id="432f2-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="432f2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="432f2-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="432f2-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="432f2-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="432f2-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="432f2-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="432f2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="432f2-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="432f2-236">Testing single sign-on</span></span>

<span data-ttu-id="432f2-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="432f2-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="432f2-238">Quando si fa clic sul riquadro PlanMyLeave nel pannello di accesso, si accederà automaticamente all'applicazione PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="432f2-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="432f2-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="432f2-239">Additional resources</span></span>

* [<span data-ttu-id="432f2-240">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="432f2-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="432f2-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="432f2-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png