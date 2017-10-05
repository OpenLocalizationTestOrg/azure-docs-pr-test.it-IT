---
title: 'Esercitazione: Integrazione di Azure Active Directory con GitHub | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="484ac-103">Esercitazione: Integrazione di Azure Active Directory con GitHub</span><span class="sxs-lookup"><span data-stu-id="484ac-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="484ac-104">Questa esercitazione descrive come integrare GitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="484ac-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="484ac-105">L'integrazione di GitHub con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="484ac-106">È possibile controllare in Azure AD chi può accedere a GitHub</span><span class="sxs-lookup"><span data-stu-id="484ac-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="484ac-107">È possibile abilitare gli utenti per l'accesso automatico a GitHub (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="484ac-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="484ac-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="484ac-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="484ac-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="484ac-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="484ac-110">Prerequisites</span></span>

<span data-ttu-id="484ac-111">Per configurare l'integrazione di Azure AD con GitHub, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="484ac-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="484ac-113">Sottoscrizione di GitHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="484ac-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="484ac-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="484ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="484ac-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="484ac-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="484ac-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="484ac-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="484ac-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="484ac-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="484ac-118">Scenario description</span></span>
<span data-ttu-id="484ac-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="484ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="484ac-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="484ac-121">Aggiunta di GitHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="484ac-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="484ac-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="484ac-123">Aggiunta di GitHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="484ac-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="484ac-124">Per configurare l'integrazione di GitHub in Azure AD, è necessario aggiungere GitHub dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="484ac-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="484ac-125">**Per aggiungere GitHub dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="484ac-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="484ac-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="484ac-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="484ac-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="484ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="484ac-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="484ac-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="484ac-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="484ac-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="484ac-133">Nella casella di ricerca digitare **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="484ac-133">In the search box, type **GitHub.com**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="484ac-135">Nel pannello dei risultati selezionare **GitHub** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="484ac-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="484ac-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="484ac-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GitHub in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="484ac-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="484ac-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di GitHub che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="484ac-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="484ac-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** in GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="484ac-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con GitHub, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="484ac-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="484ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="484ac-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="484ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="484ac-145">**[Creazione di un utente test di GitHub](#creating-a-GitHub-test-user)**: per avere una controparte di Britta Simon in GitHub collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484ac-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="484ac-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="484ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="484ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="484ac-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="484ac-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="484ac-150">**Per configurare Single Sign-On di Azure AD con GitHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="484ac-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="484ac-151">Nella pagina di integrazione dell'applicazione **GitHub** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="484ac-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="484ac-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="484ac-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="484ac-155">Nella sezione **URL e dominio GitHub** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="484ac-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="484ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="484ac-157">a.</span></span> <span data-ttu-id="484ac-158">Nella casella di testo **URL di accesso** digitare il valore come: `https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="484ac-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="484ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="484ac-159">b.</span></span> <span data-ttu-id="484ac-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="484ac-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="484ac-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="484ac-161">Please note that these are not the real values.</span></span> <span data-ttu-id="484ac-162">È necessario aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="484ac-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="484ac-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="484ac-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="484ac-164">Passare alla sezione Admin di GitHub per recuperare questi valori.</span><span class="sxs-lookup"><span data-stu-id="484ac-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="484ac-165">Nella sezione **User Attributes** (Attributi utente) selezionare **User Identifier** (Identificatore utente) come user.mail.</span><span class="sxs-lookup"><span data-stu-id="484ac-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="484ac-167">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="484ac-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="484ac-169">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="484ac-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="484ac-170">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="484ac-170">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="484ac-172">Nella sezione **Certificato di firma SAML** selezionare **Make new certificate active** (Rendi attivo il nuovo certificato) e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="484ac-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="484ac-174">Nella finestra popup **Rollover certificate** (Certificato di rollover) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="484ac-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="484ac-176">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="484ac-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="484ac-178">Nella sezione **GitHub Configuration** (Configurazione GitHub) fare clic su **Configure GitHub** (Configura GitHub) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="484ac-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="484ac-181">In un'altra finestra del Web browser accedere al sito aziendale di GitHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="484ac-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="484ac-182">Passare a **Settings** (Impostazioni) e fare clic su **Security** (Sicurezza).</span><span class="sxs-lookup"><span data-stu-id="484ac-182">Navigate to **Settings** and click **Security**</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="484ac-184">Selezionare la casella **Enable SAML authentication** (Abilita autenticazione SAML) mostrando i campi di configurazione dell'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="484ac-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="484ac-185">Usare quindi il valore URL di Single Sign-On per aggiornare l'URL di Single Sign-On nella configurazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484ac-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="484ac-187">Configurare i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="484ac-187">Configure the following fields:</span></span>

    <span data-ttu-id="484ac-188">a.</span><span class="sxs-lookup"><span data-stu-id="484ac-188">a.</span></span> <span data-ttu-id="484ac-189">**URL di accesso**: immettere il **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) nella sezione **Configura GitHub** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="484ac-190">b.</span><span class="sxs-lookup"><span data-stu-id="484ac-190">b.</span></span> <span data-ttu-id="484ac-191">**Autorità di certificazione**: immettere l'**ID entità SAML** dalla sezione **Configura GitHub** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="484ac-192">c.</span><span class="sxs-lookup"><span data-stu-id="484ac-192">c.</span></span> <span data-ttu-id="484ac-193">**Public Certificate** (Certificato pubblico): aprire il certificato scaricato da Azure AD in blocco note e copiare il contenuto incluso tra "BEGIN CERTIFICATE" ed "END CERTIFICATE".</span><span class="sxs-lookup"><span data-stu-id="484ac-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="484ac-195">Fare clic su **Test SAML configuration** (Test configurazione SAML) per confermare l'assenza di errori di convalida o errori durante l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="484ac-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="484ac-197">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="484ac-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="484ac-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="484ac-199">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="484ac-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="484ac-201">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="484ac-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="484ac-202">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="484ac-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="484ac-204">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="484ac-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="484ac-206">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="484ac-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="484ac-208">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="484ac-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="484ac-210">a.</span><span class="sxs-lookup"><span data-stu-id="484ac-210">a.</span></span> <span data-ttu-id="484ac-211">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="484ac-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="484ac-212">b.</span><span class="sxs-lookup"><span data-stu-id="484ac-212">b.</span></span> <span data-ttu-id="484ac-213">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="484ac-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="484ac-214">c.</span><span class="sxs-lookup"><span data-stu-id="484ac-214">c.</span></span> <span data-ttu-id="484ac-215">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="484ac-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="484ac-216">d.</span><span class="sxs-lookup"><span data-stu-id="484ac-216">d.</span></span> <span data-ttu-id="484ac-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="484ac-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="484ac-218">Creazione di un utente test GitHub</span><span class="sxs-lookup"><span data-stu-id="484ac-218">Creating a GitHub test user</span></span>

<span data-ttu-id="484ac-219">Per consentire agli utenti di Azure AD di accedere a GitHub, è necessario eseguirne il provisioning in GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="484ac-220">Nel caso di GitHub, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="484ac-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="484ac-221">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="484ac-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="484ac-222">Accedere al sito aziendale di GitHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="484ac-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="484ac-223">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="484ac-223">Click **People**.</span></span>

    <span data-ttu-id="484ac-224">![Persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="484ac-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="484ac-225">Fare clic su **Invite member** (Invita membro).</span><span class="sxs-lookup"><span data-stu-id="484ac-225">Click **Invite member**.</span></span>

    <span data-ttu-id="484ac-226">![Invitare utenti](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="484ac-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="484ac-227">Nella finestra di dialogo **Invite member** (Invita membro) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="484ac-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="484ac-228">a.</span><span class="sxs-lookup"><span data-stu-id="484ac-228">a.</span></span> <span data-ttu-id="484ac-229">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="484ac-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="484ac-230">![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="484ac-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="484ac-231">b.</span><span class="sxs-lookup"><span data-stu-id="484ac-231">b.</span></span> <span data-ttu-id="484ac-232">Fare clic su **Send Invitation** (Invia invito).</span><span class="sxs-lookup"><span data-stu-id="484ac-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="484ac-233">![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="484ac-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="484ac-234">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="484ac-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="484ac-235">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="484ac-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="484ac-236">In questa sezione Britta Simon viene abilitata per l'uso di Single Sign-On di Azure concedendole l'accesso a GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="484ac-238">**Per assegnare Britta Simon a GitHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="484ac-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="484ac-239">Nel portale di gestione di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="484ac-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="484ac-241">Nell'elenco di applicazioni selezionare **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="484ac-241">In the applications list, select **GitHub.com**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="484ac-243">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="484ac-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="484ac-245">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="484ac-245">Click **Add** button.</span></span> <span data-ttu-id="484ac-246">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="484ac-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="484ac-248">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="484ac-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="484ac-249">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="484ac-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="484ac-250">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="484ac-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="484ac-251">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="484ac-251">Testing single sign-on</span></span>

<span data-ttu-id="484ac-252">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="484ac-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="484ac-253">Quando si fa clic sul riquadro GitHub nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione GitHub.</span><span class="sxs-lookup"><span data-stu-id="484ac-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="484ac-254">L'accesso avverrà con un account aziendale, ma è necessario accedere con l'account personale.</span><span class="sxs-lookup"><span data-stu-id="484ac-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="484ac-255">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="484ac-255">Additional resources</span></span>

* [<span data-ttu-id="484ac-256">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="484ac-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="484ac-257">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="484ac-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
