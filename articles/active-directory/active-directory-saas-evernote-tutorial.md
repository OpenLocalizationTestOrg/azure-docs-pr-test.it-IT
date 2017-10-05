---
title: 'Esercitazione: Integrazione di Azure Active Directory con Evernote | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory ed Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="27df1-103">Esercitazione: Integrazione di Azure Active Directory con Evernote</span><span class="sxs-lookup"><span data-stu-id="27df1-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="27df1-104">Questa esercitazione descrive come integrare Evernote con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27df1-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27df1-105">L'integrazione di Evernote con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="27df1-106">È possibile controllare in Azure AD chi può accedere a Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="27df1-107">È possibile abilitare gli utenti per l'accesso automatico a Evernote (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27df1-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27df1-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="27df1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="27df1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27df1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27df1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27df1-110">Prerequisites</span></span>

<span data-ttu-id="27df1-111">Per configurare l'integrazione di Azure AD con Evernote, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="27df1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27df1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27df1-113">Sottoscrizione di Evernote abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="27df1-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27df1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="27df1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27df1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27df1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="27df1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27df1-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27df1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27df1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="27df1-118">Scenario description</span></span>
<span data-ttu-id="27df1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="27df1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27df1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27df1-121">Aggiunta di Evernote dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="27df1-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="27df1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="27df1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="27df1-123">Aggiunta di Evernote dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="27df1-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="27df1-124">Per configurare l'integrazione di Evernote in Azure AD, è necessario aggiungere Evernote dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="27df1-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="27df1-125">**Per aggiungere Evernote dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="27df1-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="27df1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="27df1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="27df1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="27df1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="27df1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="27df1-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="27df1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="27df1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="27df1-133">Nella casella di ricerca digitare **Evernote**, selezionare **Evernote** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="27df1-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote nell'elenco risultati](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27df1-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="27df1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="27df1-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Evernote in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27df1-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27df1-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Evernote che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27df1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="27df1-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="27df1-139">Per stabilire la relazione di collegamento, in Evernote assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="27df1-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="27df1-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Evernote, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="27df1-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="27df1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="27df1-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27df1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27df1-143">**[Creare un utente test di Evernote](#create-an-evernote-test-user)**: per avere una controparte di Britta Simon in Evernote collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27df1-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="27df1-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27df1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27df1-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="27df1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27df1-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="27df1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="27df1-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="27df1-148">**Per configurare Single Sign-On di Azure AD con Evernote, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="27df1-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="27df1-149">Nella pagina di integrazione dell'applicazione **Evernote** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="27df1-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="27df1-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="27df1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="27df1-153">Nella sezione **URL e dominio Evernote** seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da IdP:</span><span class="sxs-lookup"><span data-stu-id="27df1-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="27df1-155">Nella casella di testo **Identificatore** digitare l'URL: `https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="27df1-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="27df1-156">Selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="27df1-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="27df1-158">Nella casella di testo **URL di accesso** digitare l'URL: `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="27df1-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="27df1-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="27df1-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="27df1-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="27df1-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="27df1-163">Nella sezione **Configurazione di Evernote** fare clic su **Configura Evernote** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="27df1-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="27df1-164">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="27df1-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="27df1-166">In un'altra finestra del Web browser accedere al sito aziendale di Evernote come amministratore.</span><span class="sxs-lookup"><span data-stu-id="27df1-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="27df1-167">Passare a **Admin Console** (Console di amministrazione)</span><span class="sxs-lookup"><span data-stu-id="27df1-167">Go to **'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="27df1-169">Da **Admin Console** (Console di amministrazione), andare a **Security** (Sicurezza) e selezionare **Single Sign-On** (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="27df1-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="27df1-171">Configurare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="27df1-171">Configure the following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="27df1-173">a.</span><span class="sxs-lookup"><span data-stu-id="27df1-173">a.</span></span>  <span data-ttu-id="27df1-174">**Enable SSO** (Abilita SSO): SSO è abilitato per impostazione predefinita. Fare clic su **Disable Single Sign-on** (Disabilita Single Sign-on) per rimuovere il requisito SSO.</span><span class="sxs-lookup"><span data-stu-id="27df1-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="27df1-175">b.</span><span class="sxs-lookup"><span data-stu-id="27df1-175">b.</span></span> <span data-ttu-id="27df1-176">Incollare il valore di **SAML Single sign-on Service URL** (URL servizio Single Sign-On SAML), copiato dal portale di Azure, nella casella di testo **SAML HTTP Request URL** (URL di richiesta HTTP SAML).</span><span class="sxs-lookup"><span data-stu-id="27df1-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="27df1-177">c.</span><span class="sxs-lookup"><span data-stu-id="27df1-177">c.</span></span> <span data-ttu-id="27df1-178">Aprire il certificato scaricato da Azure AD in blocco note e copiare il contenuto incluso tra "BEGIN CERTIFICATE" ed "END CERTIFICATE" nella casella di testo **X.509 Certificate** (Certificato x. 509).</span><span class="sxs-lookup"><span data-stu-id="27df1-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="27df1-179">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="27df1-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="27df1-180">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="27df1-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="27df1-181">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="27df1-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="27df1-182">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27df1-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27df1-183">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="27df1-183">Create an Azure AD test user</span></span>

<span data-ttu-id="27df1-184">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="27df1-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="27df1-186">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="27df1-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="27df1-187">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="27df1-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="27df1-189">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="27df1-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="27df1-191">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="27df1-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="27df1-193">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="27df1-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27df1-195">a.</span><span class="sxs-lookup"><span data-stu-id="27df1-195">a.</span></span> <span data-ttu-id="27df1-196">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27df1-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27df1-197">b.</span><span class="sxs-lookup"><span data-stu-id="27df1-197">b.</span></span> <span data-ttu-id="27df1-198">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27df1-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="27df1-199">c.</span><span class="sxs-lookup"><span data-stu-id="27df1-199">c.</span></span> <span data-ttu-id="27df1-200">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="27df1-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="27df1-201">d.</span><span class="sxs-lookup"><span data-stu-id="27df1-201">d.</span></span> <span data-ttu-id="27df1-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="27df1-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="27df1-203">Creare un utente test di Evernote</span><span class="sxs-lookup"><span data-stu-id="27df1-203">Create an Evernote test user</span></span>

<span data-ttu-id="27df1-204">Per consentire agli utenti di Azure AD di accedere a Evernote, è necessario eseguirne il provisioning in Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="27df1-205">Nel caso di Evernote, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="27df1-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="27df1-206">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="27df1-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="27df1-207">Accedere al sito aziendale di Evernote come amministratore.</span><span class="sxs-lookup"><span data-stu-id="27df1-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="27df1-208">Fare clic su di **Admin Console** (Console di amministrazione).</span><span class="sxs-lookup"><span data-stu-id="27df1-208">Click the **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="27df1-210">Da **Admin Console** (Console di amministrazione), andare a **Add users** (Aggiungi utenti).</span><span class="sxs-lookup"><span data-stu-id="27df1-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="27df1-212">**Add team members**(Aggiungi membri del team): nella casella di testo **Email** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'account utente e fare clic su **Invite** (Invita).</span><span class="sxs-lookup"><span data-stu-id="27df1-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="27df1-214">Dopo l'invio dell'invito, il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica per accettare l'invito.</span><span class="sxs-lookup"><span data-stu-id="27df1-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="27df1-215">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="27df1-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="27df1-216">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="27df1-218">**Per assegnare Britta Simon a Evernote, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="27df1-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="27df1-219">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="27df1-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="27df1-221">Nell'elenco delle applicazioni selezionare **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="27df1-221">In the applications list, select **Evernote**.</span></span>

    ![Collegamento di Evernote nell'elenco delle applicazioni](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="27df1-223">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="27df1-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="27df1-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="27df1-225">Click **Add** button.</span></span> <span data-ttu-id="27df1-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="27df1-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="27df1-228">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="27df1-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="27df1-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="27df1-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27df1-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="27df1-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="27df1-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="27df1-231">Test single sign-on</span></span>

<span data-ttu-id="27df1-232">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="27df1-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="27df1-233">Quando si fa clic sul riquadro Evernote nel pannello di accesso, si dovrebbe accedere all'applicazione Evernote.</span><span class="sxs-lookup"><span data-stu-id="27df1-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="27df1-234">L'accesso avverrà con un account aziendale, ma è necessario accedere con l'account personale.</span><span class="sxs-lookup"><span data-stu-id="27df1-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27df1-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="27df1-235">Additional resources</span></span>

* [<span data-ttu-id="27df1-236">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27df1-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27df1-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27df1-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

