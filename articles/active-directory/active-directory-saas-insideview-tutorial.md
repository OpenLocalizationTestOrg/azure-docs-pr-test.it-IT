---
title: 'Esercitazione: Integrazione di Azure Active Directory con InsideView | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e InsideView.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="d15c2-103">Esercitazione: Integrazione di Azure Active Directory con InsideView</span><span class="sxs-lookup"><span data-stu-id="d15c2-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="d15c2-104">Questa esercitazione descrive come integrare InsideView con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d15c2-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d15c2-105">L'integrazione di InsideView con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d15c2-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d15c2-106">È possibile controllare in Azure AD chi può accedere a InsideView</span><span class="sxs-lookup"><span data-stu-id="d15c2-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="d15c2-107">È possibile abilitare gli utenti per l'accesso automatico a InsideView (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d15c2-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d15c2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d15c2-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d15c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d15c2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d15c2-110">Prerequisites</span></span>

<span data-ttu-id="d15c2-111">Per configurare l'integrazione di Azure AD con InsideView, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d15c2-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="d15c2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d15c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d15c2-113">Sottoscrizione di InsideView abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d15c2-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d15c2-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d15c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d15c2-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d15c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d15c2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d15c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d15c2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d15c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d15c2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d15c2-118">Scenario description</span></span>
<span data-ttu-id="d15c2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d15c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d15c2-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d15c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d15c2-121">Aggiunta di InsideView dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d15c2-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="d15c2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="d15c2-123">Aggiunta di InsideView dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d15c2-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="d15c2-124">Per configurare l'integrazione di InsideView in Azure AD, è necessario aggiungere InsideView dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d15c2-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d15c2-125">**Per aggiungere InsideView dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d15c2-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d15c2-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d15c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d15c2-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d15c2-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d15c2-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d15c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d15c2-133">Nella casella di ricerca digitare **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-133">In the search box, type **InsideView**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="d15c2-135">Nel pannello dei risultati selezionare **InsideView** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d15c2-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d15c2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d15c2-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con InsideView con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d15c2-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d15c2-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di InsideView che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d15c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="d15c2-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in InsideView.</span><span class="sxs-lookup"><span data-stu-id="d15c2-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="d15c2-141">Per stabilire la relazione di collegamento, in InsideView assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Nome utente**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d15c2-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con InsideView, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d15c2-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d15c2-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d15c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d15c2-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d15c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d15c2-145">**[Creazione di un utente test di InsideView](#creating-a-insideview-test-user)**: per avere una controparte di Britta Simon in InsideView collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d15c2-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d15c2-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d15c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d15c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d15c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d15c2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d15c2-149">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione InsideView.</span><span class="sxs-lookup"><span data-stu-id="d15c2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="d15c2-150">**Per configurare l'accesso Single Sign-On di Azure AD con InsideView, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d15c2-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="d15c2-151">Nella pagina di integrazione dell'applicazione **InsideView** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d15c2-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d15c2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="d15c2-155">Nella sezione **URL e dominio InsideView** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d15c2-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="d15c2-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="d15c2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d15c2-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="d15c2-158">This value is not real.</span></span> <span data-ttu-id="d15c2-159">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="d15c2-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="d15c2-160">Per ottenere tale valore, contattare il [team di supporto di InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="d15c2-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="d15c2-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificate (Raw)** (Certificato (base)) e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d15c2-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="d15c2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d15c2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d15c2-165">Nella sezione **Configurazione di InsideView** fare clic su **Configura InsideView** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d15c2-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d15c2-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="d15c2-168">In un'altra finestra del Web browser accedere al sito aziendale di InsideView come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d15c2-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="d15c2-169">Nella barra degli strumenti in alto fare clic su **Admin** (Amministratore), **SingleSignOn Settings** (Impostazioni Single Sign-On) e quindi su **Add SAML** (Aggiungi SAML).</span><span class="sxs-lookup"><span data-stu-id="d15c2-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="d15c2-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="d15c2-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="d15c2-171">Nella sezione **Aggiungi un nuovo SAML** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d15c2-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="d15c2-172">![Aggiungi un nuovo SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Aggiungi un nuovo SAML")</span><span class="sxs-lookup"><span data-stu-id="d15c2-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="d15c2-173">a.</span><span class="sxs-lookup"><span data-stu-id="d15c2-173">a.</span></span> <span data-ttu-id="d15c2-174">Nella casella di testo **Nome STS** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d15c2-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="d15c2-175">b.</span><span class="sxs-lookup"><span data-stu-id="d15c2-175">b.</span></span> <span data-ttu-id="d15c2-176">Nella casella di testo **SamlP/WS-Fed Unsolicited EndPoint** incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d15c2-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d15c2-177">c.</span><span class="sxs-lookup"><span data-stu-id="d15c2-177">c.</span></span> <span data-ttu-id="d15c2-178">Aprire il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **STS Certificate** (Certificato servizio token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="d15c2-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="d15c2-179">d.</span><span class="sxs-lookup"><span data-stu-id="d15c2-179">d.</span></span> <span data-ttu-id="d15c2-180">Nella casella di testo **Crm User Id Mapping** digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d15c2-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="d15c2-181">e.</span><span class="sxs-lookup"><span data-stu-id="d15c2-181">e.</span></span> <span data-ttu-id="d15c2-182">Nella casella di testo **Crm Email Mapping** digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d15c2-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="d15c2-183">f.</span><span class="sxs-lookup"><span data-stu-id="d15c2-183">f.</span></span> <span data-ttu-id="d15c2-184">Nella casella di testo **Crm First Name Mapping** digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="d15c2-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="d15c2-185">g.</span><span class="sxs-lookup"><span data-stu-id="d15c2-185">g.</span></span> <span data-ttu-id="d15c2-186">Nella casella di testo **Crm lastName Mapping** digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="d15c2-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="d15c2-187">h.</span><span class="sxs-lookup"><span data-stu-id="d15c2-187">h.</span></span> <span data-ttu-id="d15c2-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d15c2-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d15c2-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d15c2-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d15c2-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d15c2-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d15c2-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d15c2-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d15c2-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d15c2-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d15c2-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d15c2-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d15c2-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d15c2-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d15c2-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d15c2-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d15c2-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d15c2-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d15c2-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d15c2-204">a.</span><span class="sxs-lookup"><span data-stu-id="d15c2-204">a.</span></span> <span data-ttu-id="d15c2-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d15c2-206">b.</span><span class="sxs-lookup"><span data-stu-id="d15c2-206">b.</span></span> <span data-ttu-id="d15c2-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d15c2-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d15c2-208">c.</span><span class="sxs-lookup"><span data-stu-id="d15c2-208">c.</span></span> <span data-ttu-id="d15c2-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d15c2-210">d.</span><span class="sxs-lookup"><span data-stu-id="d15c2-210">d.</span></span> <span data-ttu-id="d15c2-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="d15c2-212">Creazione di un utente test di InsideView</span><span class="sxs-lookup"><span data-stu-id="d15c2-212">Creating a InsideView test user</span></span>

<span data-ttu-id="d15c2-213">Per consentire agli utenti di Azure AD di accedere a InsideView, è necessario eseguirne il provisioning in InsideView.</span><span class="sxs-lookup"><span data-stu-id="d15c2-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="d15c2-214">Nel caso di InsideView, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d15c2-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="d15c2-215">Per ottenere gli utenti o i contatti creati in InsideView, contattare il [team di supporto di InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="d15c2-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="d15c2-216">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da InsideView per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d15c2-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d15c2-217">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15c2-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d15c2-218">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a InsideView.</span><span class="sxs-lookup"><span data-stu-id="d15c2-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d15c2-220">**Per assegnare Britta Simon a InsideView, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d15c2-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="d15c2-221">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d15c2-223">Nell'elenco delle applicazioni selezionare **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-223">In the applications list, select **InsideView**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="d15c2-225">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d15c2-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d15c2-227">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-227">Click **Add** button.</span></span> <span data-ttu-id="d15c2-228">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d15c2-230">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d15c2-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d15c2-231">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d15c2-232">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d15c2-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d15c2-233">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d15c2-233">Testing single sign-on</span></span>

<span data-ttu-id="d15c2-234">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d15c2-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d15c2-235">Quando si fa clic sul riquadro InsideView nel pannello di accesso, si accede automaticamente all'applicazione InsideView.</span><span class="sxs-lookup"><span data-stu-id="d15c2-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d15c2-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d15c2-236">Additional resources</span></span>

* [<span data-ttu-id="d15c2-237">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d15c2-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d15c2-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d15c2-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

