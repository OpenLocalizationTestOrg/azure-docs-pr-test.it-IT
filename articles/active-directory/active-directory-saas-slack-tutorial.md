---
title: 'Esercitazione: Integrazione di Azure Active Directory con Slack | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Slack.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="0a98e-103">Esercitazione: Integrazione di Azure Active Directory con Slack</span><span class="sxs-lookup"><span data-stu-id="0a98e-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="0a98e-104">Questa esercitazione descrive come integrare Slack con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a98e-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a98e-105">L'integrazione di Slack con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a98e-106">È possibile controllare in Azure AD chi può accedere a Slack</span><span class="sxs-lookup"><span data-stu-id="0a98e-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="0a98e-107">È possibile abilitare gli utenti per l'accesso automatico a Slack (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a98e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a98e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a98e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a98e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a98e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a98e-110">Prerequisites</span></span>

<span data-ttu-id="0a98e-111">Per configurare l'integrazione di Azure AD con Slack, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="0a98e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a98e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a98e-113">Sottoscrizione di Slack abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a98e-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a98e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a98e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a98e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0a98e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a98e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a98e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a98e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0a98e-118">Scenario description</span></span>
<span data-ttu-id="0a98e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0a98e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a98e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a98e-121">Aggiunta di Slack dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0a98e-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="0a98e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="0a98e-123">Aggiunta di Slack dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0a98e-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="0a98e-124">Per configurare l'integrazione di Slack in Azure AD, è necessario aggiungere Slack dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0a98e-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a98e-125">**Per aggiungere Slack dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a98e-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a98e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0a98e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a98e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a98e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0a98e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0a98e-133">Nella casella di ricerca digitare **Slack**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-133">In the search box, type **Slack**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="0a98e-135">Nel pannello dei risultati selezionare **Slack** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a98e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a98e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Slack con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a98e-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a98e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Slack che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a98e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="0a98e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="0a98e-141">Per stabilire la relazione di collegamento, in Slack assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a98e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Slack, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a98e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0a98e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a98e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a98e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a98e-145">**[Creazione di un utente di test di Slack](#creating-a-slack-test-user)**: per avere una controparte di Britta Simon in Slack collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a98e-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a98e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a98e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a98e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0a98e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a98e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a98e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="0a98e-150">**Per configurare l'accesso Single Sign-On di Azure AD con Slack, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a98e-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="0a98e-151">Nella pagina di integrazione dell'applicazione **Slack** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0a98e-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0a98e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="0a98e-155">Nella sezione **URL e dominio Slack** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a98e-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="0a98e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a98e-157">a.</span></span> <span data-ttu-id="0a98e-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.slack.com`.</span><span class="sxs-lookup"><span data-stu-id="0a98e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="0a98e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a98e-159">b.</span></span> <span data-ttu-id="0a98e-160">Nella casella di testo **Identificatore** digitare l'URL: `https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="0a98e-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a98e-161">Poiché non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="0a98e-161">The value is not real.</span></span> <span data-ttu-id="0a98e-162">È necessario aggiornare il valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="0a98e-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="0a98e-163">Per ottenere il valore, contattare il [team di supporto di Slack](https://slack.com/help/contact)</span><span class="sxs-lookup"><span data-stu-id="0a98e-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="0a98e-164">L'applicazione Slack prevede che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="0a98e-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0a98e-165">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-165">Configure the following claims for this application.</span></span> <span data-ttu-id="0a98e-166">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0a98e-167">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-167">The following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="0a98e-169">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** selezionare **user.mail** come **Identificatore utente**. Per ogni riga illustrata nella tabella seguente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a98e-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="0a98e-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="0a98e-170">Attribute Name</span></span> | <span data-ttu-id="0a98e-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="0a98e-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0a98e-172">first_name</span><span class="sxs-lookup"><span data-stu-id="0a98e-172">first_name</span></span> | <span data-ttu-id="0a98e-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0a98e-173">user.givenname</span></span> |
    | <span data-ttu-id="0a98e-174">last_name</span><span class="sxs-lookup"><span data-stu-id="0a98e-174">last_name</span></span> | <span data-ttu-id="0a98e-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="0a98e-175">user.surname</span></span> |
    | <span data-ttu-id="0a98e-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="0a98e-176">User.Email</span></span> | <span data-ttu-id="0a98e-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="0a98e-177">user.mail</span></span> |  
    | <span data-ttu-id="0a98e-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="0a98e-178">User.Username</span></span> | <span data-ttu-id="0a98e-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0a98e-179">user.userprincipalname</span></span> |

    <span data-ttu-id="0a98e-180">a.</span><span class="sxs-lookup"><span data-stu-id="0a98e-180">a.</span></span> <span data-ttu-id="0a98e-181">Fare clic su **Attributo** per aprire la finestra di dialogo **Modifica attributo** ed eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a98e-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="0a98e-183">a.</span><span class="sxs-lookup"><span data-stu-id="0a98e-183">a.</span></span> <span data-ttu-id="0a98e-184">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="0a98e-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0a98e-185">b.</span><span class="sxs-lookup"><span data-stu-id="0a98e-185">b.</span></span> <span data-ttu-id="0a98e-186">Nell'elenco **Valore** selezionare il valore dell'attributo indicato per quella riga.</span><span class="sxs-lookup"><span data-stu-id="0a98e-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0a98e-187">c.</span><span class="sxs-lookup"><span data-stu-id="0a98e-187">c.</span></span> <span data-ttu-id="0a98e-188">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="0a98e-188">Click **OK**</span></span>

6. <span data-ttu-id="0a98e-189">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="0a98e-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="0a98e-191">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0a98e-191">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0a98e-193">Nella sezione **Configurazione di Slack** fare clic su **Configura Slack** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a98e-194">Copiare **l'ID entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="0a98e-196">In un'altra finestra del browser Web accedere al sito aziendale di Slack come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0a98e-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="0a98e-197">Accedere a **Microsoft Azure AD**, quindi andare su **Impostazioni team**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="0a98e-199">Nella sezione **Impostazioni team** fare clic sulla scheda **Autenticazione**, quindi fare clic su **Cambia impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="0a98e-201">Nella finestra di dialogo **Impostazioni di autenticazione SAML** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a98e-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="0a98e-203">a.</span><span class="sxs-lookup"><span data-stu-id="0a98e-203">a.</span></span>  <span data-ttu-id="0a98e-204">Nella casella di testo **Endpoint SAML 2.0 (HTTP)** incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a98e-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a98e-205">b.</span><span class="sxs-lookup"><span data-stu-id="0a98e-205">b.</span></span>  <span data-ttu-id="0a98e-206">Nella casella di testo **Autorità di certificazione del provider di identità** incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a98e-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a98e-207">c.</span><span class="sxs-lookup"><span data-stu-id="0a98e-207">c.</span></span>  <span data-ttu-id="0a98e-208">Aprire il certificato scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato pubblico**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="0a98e-209">d.</span><span class="sxs-lookup"><span data-stu-id="0a98e-209">d.</span></span> <span data-ttu-id="0a98e-210">Configurare le tre impostazioni riportate sopra nel modo appropriato per il proprio team Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="0a98e-211">Per altre informazioni sulle impostazioni, vedere la **guida alla configurazione dell'accesso SSO di Slack** disponibile a questo indirizzo:</span><span class="sxs-lookup"><span data-stu-id="0a98e-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="0a98e-212">e.</span><span class="sxs-lookup"><span data-stu-id="0a98e-212">e.</span></span>  <span data-ttu-id="0a98e-213">Fare clic su **Salva configurazione**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="0a98e-214">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0a98e-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a98e-215">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0a98e-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a98e-216">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a98e-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a98e-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a98e-218">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a98e-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0a98e-220">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a98e-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a98e-221">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0a98e-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a98e-223">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0a98e-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a98e-225">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a98e-227">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a98e-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a98e-229">a.</span><span class="sxs-lookup"><span data-stu-id="0a98e-229">a.</span></span> <span data-ttu-id="0a98e-230">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a98e-231">b.</span><span class="sxs-lookup"><span data-stu-id="0a98e-231">b.</span></span> <span data-ttu-id="0a98e-232">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a98e-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a98e-233">c.</span><span class="sxs-lookup"><span data-stu-id="0a98e-233">c.</span></span> <span data-ttu-id="0a98e-234">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a98e-235">d.</span><span class="sxs-lookup"><span data-stu-id="0a98e-235">d.</span></span> <span data-ttu-id="0a98e-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="0a98e-237">Creazione di un utente test di Slack</span><span class="sxs-lookup"><span data-stu-id="0a98e-237">Creating a Slack test user</span></span>

<span data-ttu-id="0a98e-238">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="0a98e-239">Slack supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0a98e-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0a98e-240">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0a98e-240">There is no action item for you in this section.</span></span> <span data-ttu-id="0a98e-241">Durante un tentativo di accesso a Slack viene creato un nuovo utente, se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="0a98e-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="0a98e-242">Per creare un utente manualmente, è necessario contattare il [team di supporto di Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="0a98e-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a98e-243">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a98e-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a98e-244">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0a98e-246">**Per assegnare Britta Simon a Slack, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a98e-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="0a98e-247">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0a98e-249">Nell'elenco delle applicazioni selezionare **Slack**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-249">In the applications list, select **Slack**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="0a98e-251">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0a98e-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0a98e-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-253">Click **Add** button.</span></span> <span data-ttu-id="0a98e-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0a98e-256">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0a98e-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a98e-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a98e-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a98e-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a98e-259">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a98e-259">Testing single sign-on</span></span>

<span data-ttu-id="0a98e-260">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0a98e-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a98e-261">Quando si fa clic sul riquadro Slack nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Slack.</span><span class="sxs-lookup"><span data-stu-id="0a98e-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a98e-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0a98e-262">Additional resources</span></span>

* [<span data-ttu-id="0a98e-263">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a98e-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a98e-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a98e-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

