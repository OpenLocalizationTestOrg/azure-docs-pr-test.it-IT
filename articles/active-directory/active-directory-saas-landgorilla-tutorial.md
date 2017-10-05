---
title: 'Esercitazione: Integrazione di Azure Active Directory con Land Gorilla Client| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Land Gorilla.
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="e870d-103">Esercitazione: Integrazione di Azure Active Directory con Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="e870d-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="e870d-104">Questa esercitazione descrive come integrare Land Gorilla Client con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e870d-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e870d-105">L'integrazione di Land Gorilla Client con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e870d-106">È possibile controllare in Azure AD chi può accedere a Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="e870d-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="e870d-107">È possibile abilitare gli utenti per l'accesso automatico a Land Gorilla Client (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e870d-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="e870d-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e870d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e870d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e870d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e870d-110">Prerequisites</span></span>

<span data-ttu-id="e870d-111">Per configurare l'integrazione di Azure AD con Land Gorilla Client, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="e870d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e870d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e870d-113">Sottoscrizione di Land Gorilla Client abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e870d-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="e870d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e870d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e870d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e870d-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e870d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e870d-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e870d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e870d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e870d-118">Scenario description</span></span>
<span data-ttu-id="e870d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e870d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e870d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e870d-121">Aggiunta di Land Gorilla Client dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e870d-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="e870d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="e870d-123">Aggiungere Land Gorilla Client dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e870d-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="e870d-124">Per configurare l'integrazione di Land Gorilla Client in Azure AD, è necessario aggiungere Land Gorilla Client dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e870d-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e870d-125">**Per aggiungere Land Gorilla Client dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e870d-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e870d-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e870d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e870d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e870d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e870d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e870d-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e870d-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e870d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e870d-133">Digitare **Land Gorilla Client** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e870d-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="e870d-135">Nel pannello dei risultati selezionare **Land Gorilla Client** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e870d-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e870d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e870d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Land Gorilla Client in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e870d-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e870d-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Land Gorilla Client che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e870d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="e870d-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="e870d-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="e870d-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="e870d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="e870d-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Land Gorilla Client, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e870d-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e870d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e870d-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con un gruppo limitato.</span><span class="sxs-lookup"><span data-stu-id="e870d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="e870d-145">**[Creazione di un utente test di Land Gorilla](#creating-a-land-gorilla-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e870d-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="e870d-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e870d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e870d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="e870d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e870d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e870d-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="e870d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="e870d-150">**Per configurare l'accesso Single Sign-On di Azure AD con Land Gorilla Client, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e870d-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="e870d-151">Nella pagina di integrazione dell'applicazione **Land Gorilla Client** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e870d-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e870d-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e870d-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="e870d-155">Nella sezione **URL e dominio Land Gorilla Client** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e870d-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="e870d-157">a.</span><span class="sxs-lookup"><span data-stu-id="e870d-157">a.</span></span> <span data-ttu-id="e870d-158">Nella casella di testo **Identificatore** digitare il valore usando uno dei modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e870d-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="e870d-159">b.</span><span class="sxs-lookup"><span data-stu-id="e870d-159">b.</span></span> <span data-ttu-id="e870d-160">Nella casella di testo **URL di risposta** digitare un URL corrispondente al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="e870d-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="e870d-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="e870d-161">Please note that these are not the real values.</span></span> <span data-ttu-id="e870d-162">È necessario aggiornare questi valori con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="e870d-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e870d-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="e870d-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="e870d-164">Contattare il [team di Land Gorilla Client](https://www.landgorilla.com/support/) per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="e870d-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="e870d-165">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="e870d-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="e870d-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e870d-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="e870d-169">Per completare la configurazione SSO per l'applicazione sul lato Land Gorilla, contattare il [team di supporto di Land Gorilla Client](https://www.landgorilla.com/support/) specificando il file **XML metadati** scaricato.</span><span class="sxs-lookup"><span data-stu-id="e870d-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e870d-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e870d-171">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e870d-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e870d-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870d-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e870d-174">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e870d-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e870d-176">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="e870d-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e870d-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="e870d-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e870d-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e870d-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e870d-182">a.</span><span class="sxs-lookup"><span data-stu-id="e870d-182">a.</span></span> <span data-ttu-id="e870d-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e870d-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e870d-184">b.</span><span class="sxs-lookup"><span data-stu-id="e870d-184">b.</span></span> <span data-ttu-id="e870d-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e870d-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e870d-186">c.</span><span class="sxs-lookup"><span data-stu-id="e870d-186">c.</span></span> <span data-ttu-id="e870d-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="e870d-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e870d-188">d.</span><span class="sxs-lookup"><span data-stu-id="e870d-188">d.</span></span> <span data-ttu-id="e870d-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e870d-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="e870d-190">Creare un utente test di Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="e870d-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="e870d-191">Collaborare con il [team di supporto di Land Gorilla](https://www.landgorilla.com/support/) per aggiungere gli utenti alla piattaforma Land Gorilla.</span><span class="sxs-lookup"><span data-stu-id="e870d-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e870d-192">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870d-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e870d-193">In questa sezione viene concesso a Britta Simon l'accesso a Land Gorilla Client per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="e870d-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e870d-195">**Per assegnare Britta Simon a Land Gorilla Client, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e870d-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="e870d-196">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e870d-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e870d-198">Nell'elenco di applicazioni selezionare **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="e870d-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="e870d-200">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e870d-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e870d-202">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e870d-202">Click **Add** button.</span></span> <span data-ttu-id="e870d-203">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e870d-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e870d-205">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="e870d-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e870d-206">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e870d-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e870d-207">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e870d-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="e870d-208">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e870d-208">Testing single sign-on</span></span>

<span data-ttu-id="e870d-209">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e870d-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e870d-210">Quando si fa clic sul riquadro Land Gorilla Client nel Pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="e870d-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e870d-211">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e870d-211">Additional resources</span></span>

* [<span data-ttu-id="e870d-212">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e870d-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e870d-213">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e870d-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
