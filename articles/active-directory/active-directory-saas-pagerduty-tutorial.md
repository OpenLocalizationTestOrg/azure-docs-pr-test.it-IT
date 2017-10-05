---
title: 'Esercitazione: Integrazione di Azure Active Directory con PagerDuty | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="67e91-103">Esercitazione: integrazione di Azure Active Directory con PagerDuty</span><span class="sxs-lookup"><span data-stu-id="67e91-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="67e91-104">Questa esercitazione descrive come integrare PagerDuty con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67e91-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67e91-105">L'integrazione di PagerDuty con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67e91-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67e91-106">È possibile controllare in Azure AD chi può accedere a PagerDuty</span><span class="sxs-lookup"><span data-stu-id="67e91-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="67e91-107">È possibile abilitare gli utenti per l'accesso automatico a PagerDuty (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67e91-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67e91-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67e91-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67e91-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67e91-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67e91-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67e91-110">Prerequisites</span></span>

<span data-ttu-id="67e91-111">Per configurare l'integrazione di Azure AD con PagerDuty, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67e91-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="67e91-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67e91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67e91-113">Sottoscrizione di PagerDuty abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67e91-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67e91-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="67e91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67e91-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="67e91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67e91-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="67e91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67e91-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67e91-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67e91-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="67e91-118">Scenario description</span></span>
<span data-ttu-id="67e91-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="67e91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67e91-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="67e91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67e91-121">Aggiunta di PagerDuty dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="67e91-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="67e91-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67e91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="67e91-123">Aggiunta di PagerDuty dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="67e91-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="67e91-124">Per configurare l'integrazione di PagerDuty in Azure AD, è necessario aggiungere PagerDuty dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="67e91-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67e91-125">**Per aggiungere PagerDuty dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67e91-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67e91-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="67e91-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="67e91-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="67e91-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67e91-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67e91-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="67e91-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="67e91-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="67e91-133">Nella casella di ricerca digitare **PagerDuty**, selezionare **PagerDuty** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67e91-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="67e91-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67e91-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="67e91-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PagerDuty in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="67e91-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="67e91-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di PagerDuty che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67e91-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="67e91-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="67e91-139">Per stabilire la relazione di collegamento, in PagerDuty assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="67e91-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="67e91-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con PagerDuty, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="67e91-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67e91-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67e91-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67e91-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67e91-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67e91-143">**[Creare un utente test di PagerDuty](#create-a-pagerduty-test-user)**: per avere una controparte di Britta Simon in PagerDuty collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67e91-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67e91-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67e91-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67e91-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="67e91-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="67e91-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67e91-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="67e91-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="67e91-148">**Per configurare Single Sign-On di Azure AD con PagerDuty, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67e91-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="67e91-149">Nella pagina di integrazione dell'applicazione **PagerDuty** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="67e91-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="67e91-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="67e91-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="67e91-153">Nella sezione **URL e dominio PagerDuty** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67e91-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="67e91-155">a.</span><span class="sxs-lookup"><span data-stu-id="67e91-155">a.</span></span> <span data-ttu-id="67e91-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.pagerduty.com`.</span><span class="sxs-lookup"><span data-stu-id="67e91-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="67e91-157">b.</span><span class="sxs-lookup"><span data-stu-id="67e91-157">b.</span></span> <span data-ttu-id="67e91-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="67e91-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67e91-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="67e91-159">These values are not real.</span></span> <span data-ttu-id="67e91-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="67e91-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="67e91-161">Per ottenere questi valori, contattare il [team di supporto clienti di PagerDuty](https://www.pagerduty.com/support/).</span><span class="sxs-lookup"><span data-stu-id="67e91-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="67e91-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="67e91-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="67e91-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="67e91-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67e91-166">Nella sezione **Configurazione di PagerDuty** fare clic su **Configura PagerDuty** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="67e91-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="67e91-167">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="67e91-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="67e91-169">In un'altra finestra del Web browser accedere al sito aziendale di Pagerduty come amministratore.</span><span class="sxs-lookup"><span data-stu-id="67e91-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="67e91-170">Nel menu in alto fare clic su **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="67e91-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="67e91-171">![Impostazioni account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="67e91-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="67e91-172">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="67e91-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="67e91-173">![Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="67e91-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="67e91-174">Nella pagina **Attiva Single Sign-on (SSO)** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67e91-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="67e91-175">![Abilitare l'accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Abilitare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="67e91-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="67e91-176">a.</span><span class="sxs-lookup"><span data-stu-id="67e91-176">a.</span></span> <span data-ttu-id="67e91-177">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **X.509 Certificate** (Certificato X.509).</span><span class="sxs-lookup"><span data-stu-id="67e91-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="67e91-178">b.</span><span class="sxs-lookup"><span data-stu-id="67e91-178">b.</span></span> <span data-ttu-id="67e91-179">Nella casella di testo **Login URL** (URL di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67e91-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="67e91-180">c.</span><span class="sxs-lookup"><span data-stu-id="67e91-180">c.</span></span> <span data-ttu-id="67e91-181">Nella casella di testo **Logout URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67e91-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="67e91-182">d.</span><span class="sxs-lookup"><span data-stu-id="67e91-182">d.</span></span> <span data-ttu-id="67e91-183">Selezionare **Attiva Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="67e91-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="67e91-184">e.</span><span class="sxs-lookup"><span data-stu-id="67e91-184">e.</span></span> <span data-ttu-id="67e91-185">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="67e91-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="67e91-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="67e91-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67e91-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="67e91-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67e91-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67e91-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="67e91-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67e91-189">Create an Azure AD test user</span></span>

<span data-ttu-id="67e91-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67e91-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="67e91-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67e91-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67e91-193">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="67e91-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67e91-195">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="67e91-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67e91-197">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="67e91-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67e91-199">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67e91-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67e91-201">a.</span><span class="sxs-lookup"><span data-stu-id="67e91-201">a.</span></span> <span data-ttu-id="67e91-202">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67e91-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67e91-203">b.</span><span class="sxs-lookup"><span data-stu-id="67e91-203">b.</span></span> <span data-ttu-id="67e91-204">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67e91-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67e91-205">c.</span><span class="sxs-lookup"><span data-stu-id="67e91-205">c.</span></span> <span data-ttu-id="67e91-206">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="67e91-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67e91-207">d.</span><span class="sxs-lookup"><span data-stu-id="67e91-207">d.</span></span> <span data-ttu-id="67e91-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="67e91-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="67e91-209">Creare un utente test PagerDuty</span><span class="sxs-lookup"><span data-stu-id="67e91-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="67e91-210">Per consentire agli utenti di Azure AD di accedere a PagerDuty, è necessario eseguirne il provisioning in PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="67e91-211">Nel caso di PagerDuty, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="67e91-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="67e91-212">È possibile usare qualsiasi altro strumento di creazione di account utente di Pagerduty o le API fornite da Pagerduty per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="67e91-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="67e91-213">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67e91-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="67e91-214">Accedere al tenant **Pagerduty** .</span><span class="sxs-lookup"><span data-stu-id="67e91-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="67e91-215">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="67e91-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="67e91-216">Fare clic su **Aggiungi utenti**.</span><span class="sxs-lookup"><span data-stu-id="67e91-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="67e91-217">![Aggiungere utenti](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="67e91-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="67e91-218">Nella finestra di dialogo **Invite Users** (Invita utenti) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67e91-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="67e91-219">![Invitare il team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invitare il team")</span><span class="sxs-lookup"><span data-stu-id="67e91-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="67e91-220">a.</span><span class="sxs-lookup"><span data-stu-id="67e91-220">a.</span></span> <span data-ttu-id="67e91-221">Digitare il **nome e il cognome** dell'utente, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="67e91-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="67e91-222">b.</span><span class="sxs-lookup"><span data-stu-id="67e91-222">b.</span></span> <span data-ttu-id="67e91-223">Immettere l'indirizzo **e-mail** univoco dell'utente, come **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="67e91-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="67e91-224">c.</span><span class="sxs-lookup"><span data-stu-id="67e91-224">c.</span></span> <span data-ttu-id="67e91-225">Fare clic su **Add** (Aggiungi) e quindi su **Send Invites** (Invia inviti).</span><span class="sxs-lookup"><span data-stu-id="67e91-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="67e91-226">Tutti gli utenti aggiunti riceveranno un invito per creare un account PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="67e91-227">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67e91-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="67e91-228">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="67e91-230">**Per assegnare Britta Simon a PagerDuty, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67e91-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="67e91-231">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67e91-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="67e91-233">Nell'elenco di applicazioni selezionare **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="67e91-233">In the applications list, select **PagerDuty**.</span></span>

    ![Collegamento PagerDuty nell'elenco Applicazioni](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="67e91-235">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="67e91-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="67e91-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67e91-237">Click **Add** button.</span></span> <span data-ttu-id="67e91-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67e91-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="67e91-240">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="67e91-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67e91-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67e91-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67e91-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67e91-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="67e91-243">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67e91-243">Test single sign-on</span></span>

<span data-ttu-id="67e91-244">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="67e91-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="67e91-245">Quando si fa clic sul riquadro PagerDuty nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="67e91-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="67e91-246">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67e91-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67e91-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="67e91-247">Additional resources</span></span>

* [<span data-ttu-id="67e91-248">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67e91-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67e91-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67e91-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

