---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workday | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workday.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="a0b71-103">Esercitazione: Integrazione di Azure Active Directory con Workday</span><span class="sxs-lookup"><span data-stu-id="a0b71-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="a0b71-104">Questa esercitazione descrive come integrare Workday con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0b71-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0b71-105">L'integrazione di Workday con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0b71-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0b71-106">È possibile controllare in Azure AD chi può accedere a Workday</span><span class="sxs-lookup"><span data-stu-id="a0b71-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="a0b71-107">È possibile abilitare gli utenti per l'accesso automatico a Workday (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0b71-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0b71-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0b71-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0b71-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0b71-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a0b71-110">Prerequisites</span></span>

<span data-ttu-id="a0b71-111">Per configurare l'integrazione di Azure AD con Workday, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0b71-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="a0b71-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0b71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0b71-113">Sottoscrizione di Workday abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0b71-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0b71-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a0b71-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0b71-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0b71-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0b71-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a0b71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0b71-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0b71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0b71-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a0b71-118">Scenario description</span></span>
<span data-ttu-id="a0b71-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a0b71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0b71-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0b71-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0b71-121">Aggiunta di Workday dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0b71-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="a0b71-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="a0b71-123">Aggiunta di Workday dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0b71-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="a0b71-124">Per configurare l'integrazione di Workday in Azure AD, è necessario aggiungere Workday dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a0b71-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0b71-125">**Per aggiungere Workday dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0b71-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0b71-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0b71-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0b71-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0b71-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a0b71-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0b71-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a0b71-133">Nella casella di ricerca digitare **Workday**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-133">In the search box, type **Workday**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="a0b71-135">Nel pannello dei risultati selezionare **Workday** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0b71-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0b71-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0b71-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workday in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a0b71-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0b71-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Workday che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0b71-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="a0b71-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workday.</span><span class="sxs-lookup"><span data-stu-id="a0b71-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="a0b71-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Workday.</span><span class="sxs-lookup"><span data-stu-id="a0b71-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="a0b71-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Workday, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0b71-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0b71-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a0b71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0b71-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0b71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0b71-145">**[Creazione di un utente di test di Workday](#creating-a-workday-test-user)**: per avere una controparte di Britta Simon in Workday collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0b71-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0b71-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0b71-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0b71-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a0b71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0b71-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0b71-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On con l'applicazione Workday.</span><span class="sxs-lookup"><span data-stu-id="a0b71-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="a0b71-150">**Per configurare l'accesso Single Sign-On di Azure AD con Workday, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0b71-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="a0b71-151">Nella pagina di integrazione dell'applicazione **Workday** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a0b71-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a0b71-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="a0b71-155">Nella sezione **URL e dominio Workday** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0b71-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="a0b71-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-157">a.</span></span> <span data-ttu-id="a0b71-158">Nella casella di testo **URL di accesso** digitare il valore come: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="a0b71-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="a0b71-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-159">b.</span></span> <span data-ttu-id="a0b71-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="a0b71-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0b71-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a0b71-161">These values are not the real.</span></span> <span data-ttu-id="a0b71-162">è necessario aggiornarli con l'URL di accesso e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="a0b71-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="a0b71-163">L'URL di risposta deve avere un sottodominio, ad esempio www, wd2, wd3, wd3-impl, wd5, wd5-impl.</span><span class="sxs-lookup"><span data-stu-id="a0b71-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="a0b71-164">Usare qualcosa come "*http://www.myworkday.com*" funziona mentre "*http://myworkday.com*" non funziona.</span><span class="sxs-lookup"><span data-stu-id="a0b71-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="a0b71-165">Per ottenere tali valori, contattare il [team di supporto clienti di Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="a0b71-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="a0b71-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="a0b71-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="a0b71-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a0b71-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0b71-170">Nella sezione **Configurazione di Workday** fare clic su **Configura Workday** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0b71-171">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a0b71-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="a0b71-172">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="a0b71-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="a0b71-173">In un'altra finestra del Web browser accedere al sito aziendale di Workday come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0b71-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="a0b71-174">Passare a **Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="a0b71-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="a0b71-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="a0b71-176">Passare a **Account Administration**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="a0b71-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="a0b71-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="a0b71-178">Passare a **Edit Tenant Setup – Security**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="a0b71-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span><span class="sxs-lookup"><span data-stu-id="a0b71-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="a0b71-180">Nella sezione **Redirection URLs** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0b71-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a0b71-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span><span class="sxs-lookup"><span data-stu-id="a0b71-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="a0b71-182">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-182">a.</span></span> <span data-ttu-id="a0b71-183">Fare clic su **Aggiungi riga**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="a0b71-184">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-184">b.</span></span> <span data-ttu-id="a0b71-185">Nelle caselle di testo **URL di reindirizzamento dell'accesso** e **URL di reindirizzamento dispositivi mobili** digitare l'**URL di accesso** immesso nella sezione **URL e dominio Workday** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0b71-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="a0b71-186">c.</span><span class="sxs-lookup"><span data-stu-id="a0b71-186">c.</span></span> <span data-ttu-id="a0b71-187">Nella finestra **Configura accesso** del portale di Azure copiare l'**URL di accesso** e incollarlo nella casella di testo **URL di reindirizzamento disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="a0b71-188">d.</span><span class="sxs-lookup"><span data-stu-id="a0b71-188">d.</span></span>  <span data-ttu-id="a0b71-189">Nella casella di testo **Environment** digitare il nome dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a0b71-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="a0b71-190">Il valore dell'attributo Environment è collegato al valore dell'URL del tenant:</span><span class="sxs-lookup"><span data-stu-id="a0b71-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="a0b71-191">-Se il nome di dominio dell'URL tenant di Workday inizia con impl (ad esempio *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), l'attributo **Environment** deve essere impostato su Implementation.</span><span class="sxs-lookup"><span data-stu-id="a0b71-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="a0b71-192">-Se il nome di dominio inizia con altro, è necessario contattare il [team di supporto clienti di Workday](https://www.workday.com/en-us/partners-services/services/support.html) per ottenere il valore **Environment** corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a0b71-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="a0b71-193">Nella sezione **SAML Setup** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0b71-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a0b71-194">![Configurazione SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="a0b71-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="a0b71-195">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-195">a.</span></span>  <span data-ttu-id="a0b71-196">Selezionare **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="a0b71-197">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-197">b.</span></span>  <span data-ttu-id="a0b71-198">Fare clic su **Aggiungi riga**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="a0b71-199">Nella sezione SAML Identity Providers seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0b71-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="a0b71-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="a0b71-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="a0b71-201">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-201">a.</span></span> <span data-ttu-id="a0b71-202">Nella casella di testo Identity Provider Name digitare il nome del provider, ad esempio *SPInitiatedSSO*.</span><span class="sxs-lookup"><span data-stu-id="a0b71-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="a0b71-203">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-203">b.</span></span> <span data-ttu-id="a0b71-204">Nella finestra **Configura accesso** del portale di Azure copiare l'**ID entità SAML** e incollarlo nella casella dell'**autorità emittente**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="a0b71-205">c.</span><span class="sxs-lookup"><span data-stu-id="a0b71-205">c.</span></span> <span data-ttu-id="a0b71-206">Selezionare **Enable Workday Initiated Logout** (Abilita disconnessione avviata da Workday).</span><span class="sxs-lookup"><span data-stu-id="a0b71-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="a0b71-207">d.</span><span class="sxs-lookup"><span data-stu-id="a0b71-207">d.</span></span> <span data-ttu-id="a0b71-208">Nella finestra **Configura accesso** del portale di Azure copiare l'**URL di accesso** e incollarlo nella casella dell'**URL di richiesta disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="a0b71-209">e.</span><span class="sxs-lookup"><span data-stu-id="a0b71-209">e.</span></span> <span data-ttu-id="a0b71-210">Fare clic su **Certificato di chiave pubblica del provider di identità** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="a0b71-211">![Creare](./media/active-directory-saas-workday-tutorial/IC782928.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="a0b71-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="a0b71-212">f.</span><span class="sxs-lookup"><span data-stu-id="a0b71-212">f.</span></span> <span data-ttu-id="a0b71-213">Fare clic su **Crea chiave pubblica x509**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="a0b71-214">![Creare](./media/active-directory-saas-workday-tutorial/IC782929.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="a0b71-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="a0b71-215">Nella sezione **Visualizza chiave pubblica x509** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a0b71-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="a0b71-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span><span class="sxs-lookup"><span data-stu-id="a0b71-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="a0b71-217">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-217">a.</span></span> <span data-ttu-id="a0b71-218">Nella casella di testo **Name** digitare un nome per il certificato, ad esempio *PPE\_SP*.</span><span class="sxs-lookup"><span data-stu-id="a0b71-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="a0b71-219">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-219">b.</span></span> <span data-ttu-id="a0b71-220">Nella casella di testo **Valid From** digitare il valore dell'attributo di inizio validità del certificato.</span><span class="sxs-lookup"><span data-stu-id="a0b71-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="a0b71-221">c.</span><span class="sxs-lookup"><span data-stu-id="a0b71-221">c.</span></span>  <span data-ttu-id="a0b71-222">Nella casella di testo **Valid To** digitare il valore dell'attributo di fine validità del certificato.</span><span class="sxs-lookup"><span data-stu-id="a0b71-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="a0b71-223">Per individuare la data di inizio e di fine validità, fare doppio clic sul certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="a0b71-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="a0b71-224">Le date sono elencate nella scheda **Details** .</span><span class="sxs-lookup"><span data-stu-id="a0b71-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="a0b71-225">d.</span><span class="sxs-lookup"><span data-stu-id="a0b71-225">d.</span></span>  <span data-ttu-id="a0b71-226">Aprire il certificato con codifica Base 64 nel Blocco note e quindi copiarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="a0b71-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="a0b71-227">e.</span><span class="sxs-lookup"><span data-stu-id="a0b71-227">e.</span></span>  <span data-ttu-id="a0b71-228">Nella casella di testo **Certificate** incollare il valore copiato negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="a0b71-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="a0b71-229">f.</span><span class="sxs-lookup"><span data-stu-id="a0b71-229">f.</span></span>  <span data-ttu-id="a0b71-230">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-230">Click **OK**.</span></span>

15. <span data-ttu-id="a0b71-231">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a0b71-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="a0b71-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span><span class="sxs-lookup"><span data-stu-id="a0b71-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="a0b71-233">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-233">a.</span></span>  <span data-ttu-id="a0b71-234">Abilitare **x509 Private Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="a0b71-235">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-235">b.</span></span>  <span data-ttu-id="a0b71-236">Nella casella di testo **Service Provider ID** digitare **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="a0b71-237">c.</span><span class="sxs-lookup"><span data-stu-id="a0b71-237">c.</span></span>  <span data-ttu-id="a0b71-238">Selezionare **Abilita autenticazione SAML SP initiated**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="a0b71-239">d.</span><span class="sxs-lookup"><span data-stu-id="a0b71-239">d.</span></span>  <span data-ttu-id="a0b71-240">Nella finestra **Configura accesso** del portale di Azure copiare l'**URL del servizio Single Sign-On SAML** e quindi incollarlo nella casella dell'**URL del servizio SSO IdP**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="a0b71-241">e.</span><span class="sxs-lookup"><span data-stu-id="a0b71-241">e.</span></span> <span data-ttu-id="a0b71-242">Selezionare **Do Not Deflate SP-initiated Authentication Request**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="a0b71-243">f.</span><span class="sxs-lookup"><span data-stu-id="a0b71-243">f.</span></span> <span data-ttu-id="a0b71-244">In **Authentication Request Signature Method** selezionare **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="a0b71-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span><span class="sxs-lookup"><span data-stu-id="a0b71-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="a0b71-246">g.</span><span class="sxs-lookup"><span data-stu-id="a0b71-246">g.</span></span> <span data-ttu-id="a0b71-247">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="a0b71-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="a0b71-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="a0b71-249">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a0b71-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0b71-250">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a0b71-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0b71-251">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0b71-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0b71-252">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0b71-253">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0b71-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a0b71-255">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a0b71-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0b71-256">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0b71-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0b71-258">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a0b71-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0b71-260">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0b71-262">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0b71-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0b71-264">a.</span><span class="sxs-lookup"><span data-stu-id="a0b71-264">a.</span></span> <span data-ttu-id="a0b71-265">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0b71-266">b.</span><span class="sxs-lookup"><span data-stu-id="a0b71-266">b.</span></span> <span data-ttu-id="a0b71-267">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0b71-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0b71-268">c.</span><span class="sxs-lookup"><span data-stu-id="a0b71-268">c.</span></span> <span data-ttu-id="a0b71-269">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0b71-270">d.</span><span class="sxs-lookup"><span data-stu-id="a0b71-270">d.</span></span> <span data-ttu-id="a0b71-271">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="a0b71-272">Creazione di un utente test di Workday</span><span class="sxs-lookup"><span data-stu-id="a0b71-272">Creating a Workday test user</span></span>

<span data-ttu-id="a0b71-273">Per eseguire il provisioning di un utente test in Workday, è necessario contattare il [team di supporto clienti di Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="a0b71-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="a0b71-274">Il [team di supporto clienti di Workday](https://www.workday.com/en-us/partners-services/services/support.html) provvederà a creare l'utente.</span><span class="sxs-lookup"><span data-stu-id="a0b71-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0b71-275">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0b71-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0b71-276">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Workday.</span><span class="sxs-lookup"><span data-stu-id="a0b71-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a0b71-278">**Per assegnare Britta Simon a Workday, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0b71-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="a0b71-279">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a0b71-281">Nell'elenco di applicazioni selezionare **Workday**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-281">In the applications list, select **Workday**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="a0b71-283">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a0b71-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a0b71-285">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-285">Click **Add** button.</span></span> <span data-ttu-id="a0b71-286">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a0b71-288">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a0b71-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0b71-289">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0b71-290">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0b71-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0b71-291">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0b71-291">Testing single sign-on</span></span>

<span data-ttu-id="a0b71-292">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a0b71-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a0b71-293">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0b71-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0b71-294">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a0b71-294">Additional resources</span></span>

* [<span data-ttu-id="a0b71-295">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0b71-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0b71-296">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0b71-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a0b71-297">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="a0b71-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

