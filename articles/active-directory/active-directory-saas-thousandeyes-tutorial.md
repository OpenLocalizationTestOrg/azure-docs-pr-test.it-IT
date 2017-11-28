---
title: 'Esercitazione: Integrazione di Azure Active Directory con ThousandEyes | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 392add7d5f0a55598b8b90760f5c3f2d1e67ac02
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="60845-103">Esercitazione: Integrazione di Azure Active Directory con ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="60845-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="60845-104">Questa esercitazione descrive come integrare ThousandEyes con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60845-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60845-105">L'integrazione di ThousandEyes con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="60845-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60845-106">È possibile controllare in Azure AD chi può accedere a ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="60845-107">È possibile abilitare gli utenti per l'accesso automatico a ThousandEyes (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60845-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60845-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60845-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60845-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60845-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60845-110">Prerequisites</span></span>

<span data-ttu-id="60845-111">Per configurare l'integrazione di Azure AD con ThousandEyes, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="60845-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="60845-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60845-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60845-113">Una sottoscrizione di ThousandEyes abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60845-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60845-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="60845-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60845-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="60845-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60845-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="60845-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60845-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60845-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60845-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="60845-118">Scenario description</span></span>
<span data-ttu-id="60845-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="60845-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60845-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="60845-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60845-121">Aggiunta di ThousandEyes dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="60845-121">Adding ThousandEyes from the gallery</span></span>
2. <span data-ttu-id="60845-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60845-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="60845-123">Aggiunta di ThousandEyes dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="60845-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="60845-124">Per configurare l'integrazione di ThousandEyes in Azure AD, è necessario aggiungere ThousandEyes dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="60845-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60845-125">**Per aggiungere ThousandEyes dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60845-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60845-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="60845-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60845-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="60845-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60845-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60845-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="60845-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="60845-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="60845-133">Nella casella di ricerca digitare **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="60845-133">In the search box, type **ThousandEyes**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="60845-135">Nel pannello dei risultati selezionare **ThousandEyes** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="60845-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60845-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60845-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60845-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ThousandEyes usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60845-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60845-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di ThousandEyes che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60845-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="60845-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="60845-141">Per stabilire la relazione di collegamento, in ThousandEyes assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="60845-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60845-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con ThousandEyes, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="60845-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60845-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="60845-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60845-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60845-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60845-145">**[Creazione di un utente test per ThousandEyes](#creating-a-thousandeyes-test-user)**: per avere una controparte di Britta Simon in ThousandEyes collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60845-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60845-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60845-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60845-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="60845-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60845-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60845-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60845-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="60845-150">**Per configurare Single Sign-On di Azure AD con ThousandEyes, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60845-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="60845-151">Nella pagina di integrazione dell'applicazione **ThousandEyes** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="60845-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="60845-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="60845-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="60845-155">Nella sezione **URL e dominio ThousandEyes** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="60845-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="60845-157">Nella casella di testo **URL di accesso** digitare l'URL come: `https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="60845-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="60845-158">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="60845-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="60845-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="60845-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60845-162">Nella sezione **Configurazione di ThousandEyes** fare clic su **Configura ThousandEyes** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="60845-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60845-163">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="60845-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="60845-165">In un'altra finestra del browser Web accedere al sito aziendale di **ThousandEyes** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="60845-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="60845-166">Nel menu in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="60845-166">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="60845-167">![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="60845-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="60845-168">Fare clic su **Account**</span><span class="sxs-lookup"><span data-stu-id="60845-168">Click **Account**</span></span>
   
    <span data-ttu-id="60845-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="60845-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="60845-170">Fare clic sulla scheda **Security & Authentication** (Sicurezza e autenticazione).</span><span class="sxs-lookup"><span data-stu-id="60845-170">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="60845-171">![Sicurezza e autenticazione](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security e autenticazione")</span><span class="sxs-lookup"><span data-stu-id="60845-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="60845-172">Nella sezione **Setup Single Sign-On** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="60845-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="60845-173">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="60845-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="60845-174">a.</span><span class="sxs-lookup"><span data-stu-id="60845-174">a.</span></span> <span data-ttu-id="60845-175">Selezionare **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="60845-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="60845-176">b.</span><span class="sxs-lookup"><span data-stu-id="60845-176">b.</span></span> <span data-ttu-id="60845-177">Nella casella di testo **Login Page URL** (URL pagina di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="60845-178">c.</span><span class="sxs-lookup"><span data-stu-id="60845-178">c.</span></span> <span data-ttu-id="60845-179">Nella casella di testo **Logout Page URL** (URL pagina di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="60845-180">d.</span><span class="sxs-lookup"><span data-stu-id="60845-180">d.</span></span> <span data-ttu-id="60845-181">Nella casella di testo **Autorità di certificazione del provider di identità** incollare l'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="60845-182">e.</span><span class="sxs-lookup"><span data-stu-id="60845-182">e.</span></span> <span data-ttu-id="60845-183">In **Certificato di verifica** fare clic su **Scegli file** e quindi caricare il certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="60845-184">f.</span><span class="sxs-lookup"><span data-stu-id="60845-184">f.</span></span> <span data-ttu-id="60845-185">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="60845-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="60845-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="60845-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60845-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="60845-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60845-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60845-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60845-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60845-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="60845-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60845-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="60845-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60845-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60845-193">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="60845-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60845-195">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="60845-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60845-197">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="60845-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60845-199">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="60845-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60845-201">a.</span><span class="sxs-lookup"><span data-stu-id="60845-201">a.</span></span> <span data-ttu-id="60845-202">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60845-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60845-203">b.</span><span class="sxs-lookup"><span data-stu-id="60845-203">b.</span></span> <span data-ttu-id="60845-204">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60845-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60845-205">c.</span><span class="sxs-lookup"><span data-stu-id="60845-205">c.</span></span> <span data-ttu-id="60845-206">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="60845-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60845-207">d.</span><span class="sxs-lookup"><span data-stu-id="60845-207">d.</span></span> <span data-ttu-id="60845-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="60845-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="60845-209">Creazione di un utente di test di ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="60845-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="60845-210">Per consentire agli utenti di Azure AD di accedere a ThousandEyes, è necessario eseguirne il provisioning in ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-210">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="60845-211">Nel caso di ThousandEyes, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="60845-211">In the case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="60845-212">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da ThousandEyes per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60845-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="60845-213">**Per eseguire il provisioning di un account utente a ThousandEyes, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60845-213">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="60845-214">Accedere al sito aziendale di ThousandEyes come amministratore.</span><span class="sxs-lookup"><span data-stu-id="60845-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="60845-215">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="60845-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="60845-216">![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="60845-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="60845-217">Fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="60845-217">Click **Account**.</span></span>
   
    <span data-ttu-id="60845-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="60845-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="60845-219">Fare clic sulla scheda **Accounts & Users** (Account e utenti).</span><span class="sxs-lookup"><span data-stu-id="60845-219">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="60845-220">![Account e utenti](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Account e utenti")</span><span class="sxs-lookup"><span data-stu-id="60845-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="60845-221">Nella sezione **Add Users & Accounts** (Account e utenti) eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="60845-221">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="60845-222">![Aggiungere account utente](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Aggiungere account utente")</span><span class="sxs-lookup"><span data-stu-id="60845-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="60845-223">a.</span><span class="sxs-lookup"><span data-stu-id="60845-223">a.</span></span> <span data-ttu-id="60845-224">Nella casella di testo **Name** (Nome) digitare il nome dell'utente, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="60845-224">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="60845-225">b.</span><span class="sxs-lookup"><span data-stu-id="60845-225">b.</span></span> <span data-ttu-id="60845-226">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica di un utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="60845-226">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="60845-227">b.</span><span class="sxs-lookup"><span data-stu-id="60845-227">b.</span></span> <span data-ttu-id="60845-228">Fare clic su **Add New User to Account**.</span><span class="sxs-lookup"><span data-stu-id="60845-228">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="60845-229">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare e attivare l'account.</span><span class="sxs-lookup"><span data-stu-id="60845-229">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60845-230">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60845-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60845-231">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![Assegna utente][200] 

<span data-ttu-id="60845-233">**Per assegnare Britta Simon a ThousandEyes, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60845-233">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="60845-234">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60845-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="60845-236">Nell'elenco di applicazioni selezionare **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="60845-236">In the applications list, select **ThousandEyes**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="60845-238">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="60845-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="60845-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="60845-240">Click **Add** button.</span></span> <span data-ttu-id="60845-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60845-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="60845-243">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="60845-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60845-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60845-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60845-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60845-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60845-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60845-246">Testing single sign-on</span></span>

<span data-ttu-id="60845-247">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="60845-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60845-248">Quando si fa clic sul riquadro ThousandEyes nel pannello di accesso, si dovrebbe automaticamente accedere all'applicazione ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="60845-248">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="60845-249">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60845-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60845-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="60845-250">Additional resources</span></span>

* [<span data-ttu-id="60845-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60845-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60845-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60845-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

