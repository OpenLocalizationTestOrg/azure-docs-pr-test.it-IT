---
title: 'Esercitazione: Integrazione di Azure Active Directory con ClickTime | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ClickTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="a7fc3-103">Esercitazione: Integrazione di Azure Active Directory con ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7fc3-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="a7fc3-104">Questa esercitazione descrive come integrare ClickTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7fc3-105">L'integrazione di ClickTime con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7fc3-106">È possibile controllare in Azure AD chi può accedere a ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7fc3-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="a7fc3-107">È possibile abilitare gli utenti per l'accesso automatico a ClickTime (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7fc3-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7fc3-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7fc3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a7fc3-110">Prerequisites</span></span>

<span data-ttu-id="a7fc3-111">Per configurare l'integrazione di Azure AD con ClickTime, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="a7fc3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7fc3-113">Sottoscrizione di ClickTime abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7fc3-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7fc3-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7fc3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7fc3-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7fc3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a7fc3-118">Scenario description</span></span>
<span data-ttu-id="a7fc3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7fc3-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7fc3-121">Aggiunta di ClickTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a7fc3-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="a7fc3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="a7fc3-123">Aggiunta di ClickTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a7fc3-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="a7fc3-124">Per configurare l'integrazione di ClickTime in Azure AD, è necessario aggiungere ClickTime dalla raccolta al proprio elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7fc3-125">**Per aggiungere ClickTime dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7fc3-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="a7fc3-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7fc3-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="a7fc3-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="a7fc3-133">Nella casella di ricerca digitare **ClickTime**, selezionare **ClickTime** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime nell'elenco risultati](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a7fc3-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a7fc3-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ClickTime in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7fc3-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7fc3-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di ClickTime che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="a7fc3-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="a7fc3-139">Per stabilire la relazione di collegamento, in ClickTime assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7fc3-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con ClickTime, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7fc3-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7fc3-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7fc3-143">**[Creare un utente test di ClickTime](#create-a-clicktime-test-user)**: per avere una controparte di Britta Simon in ClickTime collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7fc3-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7fc3-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a7fc3-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a7fc3-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="a7fc3-148">**Per configurare Single Sign-On di Azure AD con ClickTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a7fc3-149">Nella pagina di integrazione dell'applicazione **ClickTime** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="a7fc3-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="a7fc3-153">Nella sezione **URL e dominio ClickTime** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="a7fc3-155">a.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-155">a.</span></span> <span data-ttu-id="a7fc3-156">Nella casella di testo **Identificatore** digitare un URL come indicato di seguito: `https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="a7fc3-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="a7fc3-157">b.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-157">b.</span></span> <span data-ttu-id="a7fc3-158">Nella casella di testo **URL di risposta** digitare l'URL usando i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="a7fc3-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="a7fc3-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a7fc3-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7fc3-163">Nella sezione **Configurazione di ClickTime** fare clic su **Configura ClickTime** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a7fc3-164">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="a7fc3-166">In un'altra finestra del Web browser accedere al sito aziendale di ClickTime come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="a7fc3-167">Nella barra degli strumenti in alto fare clic su **Preferences** (Preferenze) e quindi su **Security Settings** (Impostazioni di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="a7fc3-168">Nella sezione di configurazione **Preferenza Single Sign-On** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="a7fc3-169">![Impostazioni di sicurezza](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Impostazioni di sicurezza")</span><span class="sxs-lookup"><span data-stu-id="a7fc3-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="a7fc3-170">a.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-170">a.</span></span>  <span data-ttu-id="a7fc3-171">Selezionare **Allow** sign-in using Single Sign-On (SSO) **Azure AD** (Consenti l'accesso Single Sign-On (SSO) con Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="a7fc3-172">b.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-172">b.</span></span> <span data-ttu-id="a7fc3-173">Nella casella di testo **Identity Provider Endpoint** (Endpoint del provider di identità) incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a7fc3-174">c.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-174">c.</span></span>  <span data-ttu-id="a7fc3-175">Aprire il **certificato con codifica Base 64** scaricato dal portale di Azure in **Blocco note**, copiarne il contenuto e quindi incollarlo nella casella di testo **X.509 Certificate** (Certificato X.509).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="a7fc3-176">d.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-176">d.</span></span>  <span data-ttu-id="a7fc3-177">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a7fc3-178">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7fc3-179">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7fc3-180">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a7fc3-181">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-181">Create an Azure AD test user</span></span>
<span data-ttu-id="a7fc3-182">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="a7fc3-184">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7fc3-185">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7fc3-187">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7fc3-189">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7fc3-191">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7fc3-193">a.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-193">a.</span></span> <span data-ttu-id="a7fc3-194">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7fc3-195">b.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-195">b.</span></span> <span data-ttu-id="a7fc3-196">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7fc3-197">c.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-197">c.</span></span> <span data-ttu-id="a7fc3-198">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7fc3-199">d.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-199">d.</span></span> <span data-ttu-id="a7fc3-200">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="a7fc3-201">Creare un utente test di ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7fc3-201">Create a ClickTime test user</span></span>

<span data-ttu-id="a7fc3-202">Per consentire agli utenti di Azure AD di accedere a ClickTime, è necessario eseguirne il provisioning in ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="a7fc3-203">Nel caso di ClickTime, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="a7fc3-204">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da ClickTime per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="a7fc3-205">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="a7fc3-206">Accedere al tenant **ClickTime** .</span><span class="sxs-lookup"><span data-stu-id="a7fc3-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="a7fc3-207">Nel barra degli strumenti in alto fare clic su **Company** (Azienda) e quindi su **People** (Persone).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="a7fc3-208">![Persone](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="a7fc3-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="a7fc3-209">Fare clic su **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="a7fc3-210">![Aggiungi persona](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Aggiungi persona")</span><span class="sxs-lookup"><span data-stu-id="a7fc3-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="a7fc3-211">Nella sezione New Person seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a7fc3-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="a7fc3-212">![Persone](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="a7fc3-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="a7fc3-213">a.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-213">a.</span></span>  <span data-ttu-id="a7fc3-214">Nella casella di testo **full name** (Nome completo) digitare il nome e cognome dell'utente, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="a7fc3-215">b.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-215">b.</span></span>  <span data-ttu-id="a7fc3-216">Nella casella di testo **email address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente come **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="a7fc3-217">È anche possibile impostare altre proprietà dell'oggetto new person.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="a7fc3-218">c.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-218">c.</span></span>  <span data-ttu-id="a7fc3-219">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a7fc3-220">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7fc3-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="a7fc3-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure, tramite la concessione dell'accesso a ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="a7fc3-223">**Per assegnare Britta Simon a ClickTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a7fc3-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a7fc3-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a7fc3-226">Nell'elenco delle applicazioni, selezionare **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-226">In the applications list, select **ClickTime**.</span></span>

    ![Collegamento di ClickTime nell'elenco delle applicazioni](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="a7fc3-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="a7fc3-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-230">Click **Add** button.</span></span> <span data-ttu-id="a7fc3-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="a7fc3-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7fc3-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7fc3-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a7fc3-236">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a7fc3-236">Test single sign-on</span></span>

<span data-ttu-id="a7fc3-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7fc3-238">Quando si fa clic sul riquadro ClickTime nel pannello di accesso, si accederà automaticamente all'applicazione ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7fc3-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="a7fc3-239">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7fc3-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7fc3-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a7fc3-240">Additional resources</span></span>

* [<span data-ttu-id="a7fc3-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7fc3-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7fc3-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7fc3-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

