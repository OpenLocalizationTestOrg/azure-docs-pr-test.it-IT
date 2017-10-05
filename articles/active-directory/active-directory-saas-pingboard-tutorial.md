---
title: 'Esercitazione: Integrazione di Azure Active Directory con PingBoard | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PingBoard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="7eb5f-103">Esercitazione: Integrazione di Azure Active Directory con PingBoard</span><span class="sxs-lookup"><span data-stu-id="7eb5f-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="7eb5f-104">Questa esercitazione descrive come integrare PingBoard con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7eb5f-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7eb5f-105">L'integrazione di PingBoard con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7eb5f-106">È possibile controllare in Azure AD chi può accedere a PingBoard</span><span class="sxs-lookup"><span data-stu-id="7eb5f-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="7eb5f-107">È possibile abilitare gli utenti per l'accesso automatico a PingBoard (Single Sign-On) con i propri account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7eb5f-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="7eb5f-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7eb5f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7eb5f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7eb5f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7eb5f-110">Prerequisites</span></span>

<span data-ttu-id="7eb5f-111">Per configurare l'integrazione di Azure AD con PingBoard, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="7eb5f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7eb5f-113">Sottoscrizione di PingBoard abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7eb5f-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7eb5f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7eb5f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7eb5f-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7eb5f-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7eb5f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7eb5f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7eb5f-118">Scenario description</span></span>
<span data-ttu-id="7eb5f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7eb5f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7eb5f-121">Aggiunta di PingBoard dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7eb5f-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="7eb5f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="7eb5f-123">Aggiunta di PingBoard dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7eb5f-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="7eb5f-124">Per configurare l'integrazione di PingBoard in Azure AD, è necessario aggiungere PingBoard dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7eb5f-125">**Per aggiungere PingBoard dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7eb5f-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7eb5f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7eb5f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7eb5f-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7eb5f-133">Nella casella di ricerca digitare **PingBoard**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-133">In the search box, type **Pingboard**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="7eb5f-135">Nel pannello dei risultati selezionare **PingBoard** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7eb5f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7eb5f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PingBoard con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7eb5f-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7eb5f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di PingBoard che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="7eb5f-140">In altre parole, si deve stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="7eb5f-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Nome utente** in PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="7eb5f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PingBoard, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7eb5f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7eb5f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7eb5f-145">**[Creazione di un utente test di PingBoard](#creating-a-pingboard-test-user)**: per avere una controparte di Britta Simon in PingBoard collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7eb5f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7eb5f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7eb5f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7eb5f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="7eb5f-150">**Per configurare l'accesso Single Sign-On di Azure AD con PingBoard, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="7eb5f-151">Nella pagina di integrazione dell'applicazione **PingBoard** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7eb5f-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="7eb5f-155">Nella sezione **URL e dominio PingBoard**, se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="7eb5f-157">a.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-157">a.</span></span> <span data-ttu-id="7eb5f-158">Nella casella di testo **Identificatore** digitare il valore `http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="7eb5f-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="7eb5f-159">b.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-159">b.</span></span> <span data-ttu-id="7eb5f-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="7eb5f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7eb5f-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7eb5f-162">È necessario aggiornare questi valori con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7eb5f-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="7eb5f-164">Per ottenere questi valori, contattare il [team di supporto clienti di PingBoard](https://support.pingboard.com/).</span><span class="sxs-lookup"><span data-stu-id="7eb5f-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="7eb5f-165">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="7eb5f-167">a.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-167">a.</span></span> <span data-ttu-id="7eb5f-168">Nella casella di testo **URL di accesso** digitare il valore come: `http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="7eb5f-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="7eb5f-169">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="7eb5f-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7eb5f-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7eb5f-173">Per configurare il SSO sul lato PingBoard, aprire una nuova finestra del browser e accedere al proprio account di PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="7eb5f-174">È necessario essere un amministratore di PingBoard per configurare il Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="7eb5f-175">Nel menu principale selezionare **App > Integrazioni**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-175">From the top menu select **Apps > Integrations**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="7eb5f-177">Nella pagina **Integrazioni**, trovare e fare clic sul riquadro di **"Azure Active Directory"**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="7eb5f-179">Nella finestra modale che segue fare clic su **"Configura"**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-179">In the modal that follows click **"Configure"**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="7eb5f-181">Nella pagina seguente, si noterà che l'"integrazione SSO di Azure è abilitata".</span><span class="sxs-lookup"><span data-stu-id="7eb5f-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="7eb5f-182">Aprire il file XML metadati scaricato in Notepad e incollare il contenuto in **IDP Metadata** (Metadati IDP).</span><span class="sxs-lookup"><span data-stu-id="7eb5f-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="7eb5f-184">Il file verrà convalidato e verrà abilitato il Single Sign-On se tutto è corretto</span><span class="sxs-lookup"><span data-stu-id="7eb5f-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7eb5f-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7eb5f-186">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7eb5f-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7eb5f-189">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7eb5f-191">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7eb5f-193">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7eb5f-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7eb5f-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7eb5f-197">a.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-197">a.</span></span> <span data-ttu-id="7eb5f-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7eb5f-199">b.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-199">b.</span></span> <span data-ttu-id="7eb5f-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7eb5f-201">c.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-201">c.</span></span> <span data-ttu-id="7eb5f-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7eb5f-203">d.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-203">d.</span></span> <span data-ttu-id="7eb5f-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="7eb5f-205">Creazione di un utente test PingBoard</span><span class="sxs-lookup"><span data-stu-id="7eb5f-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="7eb5f-206">Per consentire agli utenti di Azure AD di accedere a PingBoard, è necessario eseguirne il provisioning in PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="7eb5f-207">Nel caso di PingBoard, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="7eb5f-208">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7eb5f-209">Accedere al sito aziendale di PingBoard come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="7eb5f-210">Fare clic sul pulsante **"Add Employee"** ("Aggiungi dipendente") nella pagina **Directory**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="7eb5f-212">Nella pagina della finestra di dialogo **"Add Employee"** ("Aggiungi dipendente") eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Invita persone](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="7eb5f-214">a.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-214">a.</span></span> <span data-ttu-id="7eb5f-215">Nella casella di testo **Nome completo** digitare il nome completo di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="7eb5f-216">b.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-216">b.</span></span> <span data-ttu-id="7eb5f-217">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="7eb5f-218">c.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-218">c.</span></span> <span data-ttu-id="7eb5f-219">Nella casella di testo **Posizione** digitare la posizione di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="7eb5f-220">d.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-220">d.</span></span> <span data-ttu-id="7eb5f-221">Nell'elenco a discesa **Località**, selezionare la località di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="7eb5f-222">e.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-222">e.</span></span> <span data-ttu-id="7eb5f-223">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-223">Click **Add**.</span></span>   

4. <span data-ttu-id="7eb5f-224">Verrà visualizzata una schermata di conferma per confermare l'aggiunta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![confermare](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="7eb5f-226">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7eb5f-227">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eb5f-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7eb5f-228">In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7eb5f-230">**Per assegnare Britta Simon a PingBoard, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7eb5f-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="7eb5f-231">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7eb5f-233">Nell'elenco di applicazioni selezionare **PingBoard**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-233">In the applications list, select **Pingboard**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="7eb5f-235">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7eb5f-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-237">Click **Add** button.</span></span> <span data-ttu-id="7eb5f-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7eb5f-240">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7eb5f-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7eb5f-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7eb5f-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7eb5f-243">Testing single sign-on</span></span>

<span data-ttu-id="7eb5f-244">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7eb5f-245">Quando si fa clic sul riquadro di PingBoard nel pannello di accesso, si dovrebbe accedere automaticamente all’applicazione PingBoard.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7eb5f-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7eb5f-246">Additional resources</span></span>

* [<span data-ttu-id="7eb5f-247">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7eb5f-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7eb5f-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7eb5f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
