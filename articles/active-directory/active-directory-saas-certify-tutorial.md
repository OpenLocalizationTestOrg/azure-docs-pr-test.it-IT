---
title: 'Esercitazione: Integrazione di Azure Active Directory con Certify | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Certify.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="43c34-103">Esercitazione: Integrazione di Azure Active Directory con Certify</span><span class="sxs-lookup"><span data-stu-id="43c34-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="43c34-104">Questa esercitazione descrive come integrare Certify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43c34-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43c34-105">L'integrazione di Certify con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c34-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43c34-106">È possibile controllare in Azure AD chi può accedere a Certify</span><span class="sxs-lookup"><span data-stu-id="43c34-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="43c34-107">È possibile abilitare gli utenti per l'accesso automatico a Certify (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c34-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43c34-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="43c34-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="43c34-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43c34-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43c34-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="43c34-110">Prerequisites</span></span>

<span data-ttu-id="43c34-111">Per configurare l'integrazione di Azure AD con Certify, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c34-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="43c34-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43c34-113">Sottoscrizione di Certify abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="43c34-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43c34-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="43c34-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43c34-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c34-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43c34-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="43c34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43c34-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43c34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43c34-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="43c34-118">Scenario description</span></span>
<span data-ttu-id="43c34-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="43c34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43c34-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c34-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43c34-121">Aggiunta di Certify dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="43c34-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="43c34-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43c34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="43c34-123">Aggiunta di Certify dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="43c34-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="43c34-124">Per configurare l'integrazione di Certify in Azure AD, è necessario aggiungere Certify dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="43c34-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43c34-125">**Per aggiungere Certify dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43c34-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43c34-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="43c34-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43c34-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="43c34-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43c34-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="43c34-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="43c34-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="43c34-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="43c34-133">Nella casella di ricerca digitare **Certify**.</span><span class="sxs-lookup"><span data-stu-id="43c34-133">In the search box, type **Certify**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="43c34-135">Nel pannello dei risultati selezionare **Certify** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43c34-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43c34-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43c34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43c34-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Certify con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="43c34-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="43c34-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Certify che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c34-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="43c34-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Certify.</span><span class="sxs-lookup"><span data-stu-id="43c34-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="43c34-141">Per stabilire la relazione di collegamento, in Certify assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="43c34-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="43c34-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Certify, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c34-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43c34-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="43c34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="43c34-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43c34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43c34-145">**[Creazione di un utente test Certify](#creating-a-certify-test-user)** : per avere una controparte di Britta Simon in Certify collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c34-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="43c34-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c34-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43c34-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="43c34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43c34-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43c34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43c34-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell’applicazione Certify.</span><span class="sxs-lookup"><span data-stu-id="43c34-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="43c34-150">**Per configurare Single Sign-On di Azure AD con Certify, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43c34-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="43c34-151">Nella pagina di integrazione dell'applicazione **Certify** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="43c34-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="43c34-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="43c34-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="43c34-155">Nella sezione **URL e dominio Certify** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="43c34-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="43c34-157">Nella casella di testo **Identificatore** digitare l'URL: `https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="43c34-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="43c34-158">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (base)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="43c34-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="43c34-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="43c34-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43c34-162">Nella sezione **Configurazione di Certify** fare clic su **Configura Certify** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="43c34-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="43c34-163">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="43c34-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="43c34-165">Per configurare l'accesso Single Sign-On sul lato **Certify**, è necessario inviare il file **Certificato (base)** scaricato e l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="43c34-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="43c34-166">L’impostazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="43c34-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="43c34-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="43c34-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="43c34-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="43c34-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="43c34-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43c34-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43c34-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43c34-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="43c34-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="43c34-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="43c34-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="43c34-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43c34-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="43c34-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43c34-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="43c34-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43c34-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="43c34-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43c34-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="43c34-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43c34-182">a.</span><span class="sxs-lookup"><span data-stu-id="43c34-182">a.</span></span> <span data-ttu-id="43c34-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43c34-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43c34-184">b.</span><span class="sxs-lookup"><span data-stu-id="43c34-184">b.</span></span> <span data-ttu-id="43c34-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43c34-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43c34-186">c.</span><span class="sxs-lookup"><span data-stu-id="43c34-186">c.</span></span> <span data-ttu-id="43c34-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="43c34-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43c34-188">d.</span><span class="sxs-lookup"><span data-stu-id="43c34-188">d.</span></span> <span data-ttu-id="43c34-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="43c34-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="43c34-190">Creazione di un utente test Certify</span><span class="sxs-lookup"><span data-stu-id="43c34-190">Creating a Certify test user</span></span>

<span data-ttu-id="43c34-191">Questa sezione descrive come creare un utente chiamato Britta Simon in Certify.</span><span class="sxs-lookup"><span data-stu-id="43c34-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="43c34-192">Certify supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="43c34-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="43c34-193">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="43c34-193">There is no action item for you in this section.</span></span> <span data-ttu-id="43c34-194">Durante un tentativo di accesso a Certify verrà creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="43c34-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="43c34-195">Per creare un utente manualmente, è necessario contattare il [team di supporto di Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="43c34-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43c34-196">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43c34-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43c34-197">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Certify.</span><span class="sxs-lookup"><span data-stu-id="43c34-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![Assegna utente][200] 

<span data-ttu-id="43c34-199">**Per assegnare Britta Simon a Certify, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43c34-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="43c34-200">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="43c34-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="43c34-202">Nell'elenco delle applicazioni selezionare **Certify**.</span><span class="sxs-lookup"><span data-stu-id="43c34-202">In the applications list, select **Certify**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="43c34-204">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="43c34-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="43c34-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43c34-206">Click **Add** button.</span></span> <span data-ttu-id="43c34-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="43c34-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="43c34-209">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="43c34-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="43c34-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="43c34-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43c34-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="43c34-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43c34-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="43c34-212">Testing single sign-on</span></span>

<span data-ttu-id="43c34-213">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="43c34-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="43c34-214">Quando si fa clic sul riquadro Certify nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Certify.</span><span class="sxs-lookup"><span data-stu-id="43c34-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43c34-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="43c34-215">Additional resources</span></span>

* [<span data-ttu-id="43c34-216">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43c34-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43c34-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43c34-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

