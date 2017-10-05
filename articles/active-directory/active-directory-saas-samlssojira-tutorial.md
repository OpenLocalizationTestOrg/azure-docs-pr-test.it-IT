---
title: 'Esercitazione: integrazione di Azure Active Directory con SAML SSO for Jira di resolution GmbH | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAML SSO for Jira di resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="a2e20-103">Esercitazione: integrazione di Azure Active Directory con SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="a2e20-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="a2e20-104">Questa esercitazione spiega come integrare SAML SSO for Jira di resolution GmbH con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2e20-105">L'integrazione di SAML SSO for Jira di resolution GmbH con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2e20-106">È possibile controllare in Azure AD chi ha accesso a SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="a2e20-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="a2e20-107">È possibile abilitare gli utenti per l'accesso automatico a SAML SSO for Jira di resolution GmbH, ovvero per il Single Sign-On, con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2e20-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2e20-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a2e20-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2e20-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2e20-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a2e20-110">Prerequisites</span></span>

<span data-ttu-id="a2e20-111">Per configurare l'integrazione di Azure AD con SAML SSO for Jira di resolution GmbH, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="a2e20-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2e20-113">Una sottoscrizione attiva del Single Sign-On di SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="a2e20-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2e20-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a2e20-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2e20-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2e20-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a2e20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2e20-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2e20-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2e20-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a2e20-118">Scenario description</span></span>
<span data-ttu-id="a2e20-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a2e20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2e20-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2e20-121">Aggiunta di SAML SSO for Jira di resolution GmbH dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a2e20-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="a2e20-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="a2e20-123">Aggiunta di SAML SSO for Jira di resolution GmbH dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a2e20-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="a2e20-124">Per configurare l'integrazione di SAML SSO for Jira di resolution GmbH in Azure AD, è necessario aggiungere SAML SSO for Jira di resolution GmbH dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a2e20-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2e20-125">**Per aggiungere SAML SSO for Jira di resolution GmbH dalla raccolta, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2e20-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2e20-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a2e20-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2e20-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2e20-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a2e20-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2e20-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a2e20-133">Nella casella di ricerca digitare **SAML SSO for Jira di resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="a2e20-135">Nel pannello dei risultati selezionare **SAML SSO for Jira by resolution GmbH** (SAML SSO for Jira di resolution GmbH) e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2e20-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2e20-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2e20-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Jira di resolution GmbH con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a2e20-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2e20-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere il nome della controparte di SAML SSO for Jira di resolution GmbH che corrisponde all'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="a2e20-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAML SSO for Jira di resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="a2e20-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="a2e20-141">Per stabilire la relazione di collegamento, in SAML SSO for Jira di resolution GmbH assegnare il valore del **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2e20-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SAML SSO for Jira di resolution GmbH, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2e20-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a2e20-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a2e20-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2e20-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2e20-145">**[Creazione di un utente di test di SAML SSO for Jira di resolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**: per avere una controparte di Britta Simon in SAML SSO for Jira di resolution GmbH che sia collegata alla rappresentazione di Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2e20-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2e20-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2e20-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a2e20-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2e20-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2e20-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAML SSO for Jira di resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="a2e20-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="a2e20-150">**Per configurare l'accesso Single Sign-On di Azure AD con SAML SSO for Jira di resolution GmbH, seguire la procedura illustrata di seguito:**</span><span class="sxs-lookup"><span data-stu-id="a2e20-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="a2e20-151">Nella pagina di integrazione dell'applicazione **SAML SSO for Jira di resolution GmbH** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a2e20-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a2e20-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="a2e20-155">Nella sezione **SAML SSO for Jira by resolution GmbH Domain and URLs** (Dominio e URL di SAML SSO for Jira di resolution GmbH) se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="a2e20-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="a2e20-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2e20-157">a.</span></span> <span data-ttu-id="a2e20-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="a2e20-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="a2e20-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2e20-159">b.</span></span> <span data-ttu-id="a2e20-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="a2e20-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="a2e20-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="a2e20-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a2e20-162">se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="a2e20-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="a2e20-164">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="a2e20-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a2e20-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a2e20-165">These values are not real.</span></span> <span data-ttu-id="a2e20-166">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="a2e20-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a2e20-167">Contattare il [team di supporto del client di SAML SSO for Jira di resolution GmbH](https://www.resolution.de/go/support) per ottenere i valori.</span><span class="sxs-lookup"><span data-stu-id="a2e20-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="a2e20-168">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="a2e20-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="a2e20-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a2e20-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a2e20-172">In un'altra finestra del Web browser accedere al **portale di amministrazione di SAML SSO for Jira di resolution GmbH** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a2e20-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="a2e20-173">Passare il puntatore del mouse sulla rotellina e scegliere **Add-ons** (Componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="a2e20-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="a2e20-175">Si verrà reindirizzati alla pagina di Administrator Access (Accesso come amministratore).</span><span class="sxs-lookup"><span data-stu-id="a2e20-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="a2e20-176">Immettere la **password** e fare clic sul pulsante **Confirm** (Conferma).</span><span class="sxs-lookup"><span data-stu-id="a2e20-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="a2e20-178">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="a2e20-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="a2e20-179">Cercare **SAML Single Sign On (SSO) for JIRA** e fare clic su **Install** (Installa) per installare il nuovo plug-in di SAML.</span><span class="sxs-lookup"><span data-stu-id="a2e20-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="a2e20-181">Viene avviata l'installazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="a2e20-181">The plugin installation will start.</span></span> <span data-ttu-id="a2e20-182">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-182">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="a2e20-185">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-185">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="a2e20-187">Fare clic su **Configure** (Configura) per configurare il nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="a2e20-187">Click **Configure** to configure the new plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="a2e20-189">Nella pagina **SAML SingleSignOn Plugin Configuration** (Configurazione del plug-in SAML SingleSignOn) fare clic sul pulsante **Add additional Identity Provider** (Aggiungi provider di identità aggiuntivi) per configurare le impostazioni del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="a2e20-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="a2e20-191">In questa pagina eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a2e20-191">Perform following steps on this page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="a2e20-193">a.</span><span class="sxs-lookup"><span data-stu-id="a2e20-193">a.</span></span> <span data-ttu-id="a2e20-194">Aggiungere il **nome** del provider di identità, ad esempio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="a2e20-195">b.</span><span class="sxs-lookup"><span data-stu-id="a2e20-195">b.</span></span> <span data-ttu-id="a2e20-196">Aggiungere la **descrizione** del provider di identità, ad esempio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e20-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="a2e20-197">c.</span><span class="sxs-lookup"><span data-stu-id="a2e20-197">c.</span></span> <span data-ttu-id="a2e20-198">Fare clic su **XML** e selezionare il file **Metadata** (Metadati) scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e20-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a2e20-199">d.</span><span class="sxs-lookup"><span data-stu-id="a2e20-199">d.</span></span> <span data-ttu-id="a2e20-200">Fare clic sul pulsante **Load** (Carica).</span><span class="sxs-lookup"><span data-stu-id="a2e20-200">Click **Load** button.</span></span>

    <span data-ttu-id="a2e20-201">e.</span><span class="sxs-lookup"><span data-stu-id="a2e20-201">e.</span></span> <span data-ttu-id="a2e20-202">Legge i metadati IdP e popola i campi come evidenziato nella schermata.</span><span class="sxs-lookup"><span data-stu-id="a2e20-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="a2e20-203">Fare clic sul pulsante **Save settings** (Salva impostazioni) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e20-203">Click **Save settings** button to save the settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="a2e20-205">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a2e20-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2e20-206">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a2e20-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2e20-207">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2e20-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2e20-208">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2e20-209">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e20-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a2e20-211">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2e20-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2e20-212">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a2e20-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2e20-214">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a2e20-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2e20-216">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2e20-218">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a2e20-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2e20-220">a.</span><span class="sxs-lookup"><span data-stu-id="a2e20-220">a.</span></span> <span data-ttu-id="a2e20-221">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2e20-222">b.</span><span class="sxs-lookup"><span data-stu-id="a2e20-222">b.</span></span> <span data-ttu-id="a2e20-223">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2e20-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2e20-224">c.</span><span class="sxs-lookup"><span data-stu-id="a2e20-224">c.</span></span> <span data-ttu-id="a2e20-225">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a2e20-226">d.</span><span class="sxs-lookup"><span data-stu-id="a2e20-226">d.</span></span> <span data-ttu-id="a2e20-227">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="a2e20-228">Creazione di un utente di test di SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="a2e20-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="a2e20-229">Per consentire agli utenti di Azure AD di accedere a SAML SSO for Jira di resolution GmbH, è necessario eseguire il provisioning in SAML SSO for Jira di resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="a2e20-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="a2e20-230">In SAML SSO for Jira di resolution GmbH il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a2e20-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="a2e20-231">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a2e20-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a2e20-232">Accedere al sito aziendale di SAML SSO for Jira di resolution GmbH come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a2e20-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="a2e20-233">Passare il puntatore del mouse e fare clic su **User management** (Gestione utenti).</span><span class="sxs-lookup"><span data-stu-id="a2e20-233">Hover on cog and click the **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="a2e20-235">Si verrà reindirizzati alla pagina Administrator Access (Accesso amministratore) per inserire la **Password** e fare clic sul pulsante **Confirm** (Conferma).</span><span class="sxs-lookup"><span data-stu-id="a2e20-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="a2e20-237">Nella sezione della scheda **User management** (Gestione utenti) fare clic su **Create user** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="a2e20-237">Under **User management** tab section, click **create user**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="a2e20-239">Nella pagina della finestra di dialogo **"Create New User"** (Crea nuovo utente) effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2e20-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="a2e20-241">a.</span><span class="sxs-lookup"><span data-stu-id="a2e20-241">a.</span></span> <span data-ttu-id="a2e20-242">Nella casella di testo **Email address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a2e20-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a2e20-243">b.</span><span class="sxs-lookup"><span data-stu-id="a2e20-243">b.</span></span> <span data-ttu-id="a2e20-244">Nella casella di testo **Full Name** (Nome completo) digitare il nome completo dell'utente, ad esempio Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2e20-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="a2e20-245">c.</span><span class="sxs-lookup"><span data-stu-id="a2e20-245">c.</span></span> <span data-ttu-id="a2e20-246">Nella casella di testo **Username** (Nome utente) digitare l'indirizzo di posta elettronica di un utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a2e20-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a2e20-247">d.</span><span class="sxs-lookup"><span data-stu-id="a2e20-247">d.</span></span> <span data-ttu-id="a2e20-248">Nella casella di testo **Password** digitare la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2e20-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="a2e20-249">e.</span><span class="sxs-lookup"><span data-stu-id="a2e20-249">e.</span></span> <span data-ttu-id="a2e20-250">Fare clic su **Create User** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="a2e20-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a2e20-251">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e20-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a2e20-252">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAML SSO for Jira di resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="a2e20-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a2e20-254">**Per aggiungere Britta Simon a SAML SSO for Jira di resolution GmbH, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2e20-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="a2e20-255">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a2e20-257">Nell'elenco delle applicazioni selezionare **SAML SSO for Jira by resolution GmbH** (SAML SSO for Jira di resolution GmbH).</span><span class="sxs-lookup"><span data-stu-id="a2e20-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="a2e20-259">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a2e20-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a2e20-261">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-261">Click **Add** button.</span></span> <span data-ttu-id="a2e20-262">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a2e20-264">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a2e20-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a2e20-265">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2e20-266">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2e20-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2e20-267">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a2e20-267">Testing single sign-on</span></span>

<span data-ttu-id="a2e20-268">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a2e20-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a2e20-269">Quando si fa clic sul riquadro di SAML SSO for Jira di resolution GmbH nel pannello di accesso, si effettua automaticamente l'accesso all'applicazione SAML SSO for Jira di resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="a2e20-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="a2e20-270">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2e20-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2e20-271">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a2e20-271">Additional resources</span></span>

* [<span data-ttu-id="a2e20-272">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2e20-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2e20-273">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2e20-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

