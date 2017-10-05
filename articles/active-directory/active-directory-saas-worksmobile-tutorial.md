---
title: 'Esercitazione: Integrazione di Azure Active Directory con WORKS MOBILE | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e WORKS MOBILE.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="f9e67-103">Esercitazione: Integrazione di Azure Active Directory con WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="f9e67-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="f9e67-104">Questa esercitazione descrive come integrare WORKS MOBILE con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9e67-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9e67-105">L'integrazione di WORKS MOBILE con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9e67-106">È possibile controllare in Azure AD chi può accedere a WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="f9e67-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="f9e67-107">È possibile abilitare gli utenti per l'accesso automatico a WORKS MOBILE (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9e67-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9e67-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9e67-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9e67-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9e67-110">Prerequisites</span></span>

<span data-ttu-id="f9e67-111">Per configurare l'integrazione di Azure AD con WORKS MOBILE, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="f9e67-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9e67-113">Sottoscrizione di WORKS MOBILE abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f9e67-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9e67-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f9e67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9e67-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9e67-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f9e67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9e67-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9e67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9e67-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f9e67-118">Scenario description</span></span>
<span data-ttu-id="f9e67-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f9e67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9e67-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9e67-121">Aggiunta di WORKS MOBILE dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f9e67-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="f9e67-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="f9e67-123">Aggiunta di WORKS MOBILE dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f9e67-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="f9e67-124">Per configurare l'integrazione di WORKS MOBILE in Azure AD, è necessario aggiungere WORKS MOBILE dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f9e67-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9e67-125">**Per aggiungere WORKS MOBILE dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f9e67-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9e67-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f9e67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9e67-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9e67-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f9e67-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f9e67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f9e67-133">Nella casella di ricerca digitare **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="f9e67-135">Nel pannello dei risultati selezionare **WORKS MOBILE** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f9e67-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9e67-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9e67-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con WORKS MOBILE usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f9e67-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9e67-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di WORKS MOBILE che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="f9e67-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="f9e67-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="f9e67-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con WORKS MOBILE, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9e67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f9e67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9e67-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9e67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9e67-145">**[Creazione di un utente di test di WORKS MOBILE](#creating-a-works-mobile-test-user)**: per avere una controparte di Britta Simon in WORKS MOBILE collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e67-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9e67-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9e67-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f9e67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9e67-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9e67-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="f9e67-150">**Per configurare l'accesso Single Sign-On di Azure AD con WORKS MOBILE, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f9e67-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="f9e67-151">Nella pagina di integrazione dell'applicazione **WORKS MOBILE** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f9e67-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f9e67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="f9e67-155">Nella sezione **URL e dominio WORKS MOBILE** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f9e67-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="f9e67-157">a.</span><span class="sxs-lookup"><span data-stu-id="f9e67-157">a.</span></span> <span data-ttu-id="f9e67-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.worksmobile.com/jp/myservice`.</span><span class="sxs-lookup"><span data-stu-id="f9e67-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="f9e67-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9e67-159">b.</span></span> <span data-ttu-id="f9e67-160">Nella casella di testo **Identificatore** digitare il valore `worksmobile.com`.</span><span class="sxs-lookup"><span data-stu-id="f9e67-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9e67-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f9e67-161">This value is not real.</span></span> <span data-ttu-id="f9e67-162">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="f9e67-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f9e67-163">Per ottenere questo valore, contattare il [team di supporto clienti di WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com).</span><span class="sxs-lookup"><span data-stu-id="f9e67-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="f9e67-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (base)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f9e67-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="f9e67-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f9e67-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9e67-168">Nella sezione **Configurazione di WORKS MOBILE** fare clic su **Configura WORKS MOBILE** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f9e67-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f9e67-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="f9e67-171">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il [team di supporto di WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) e fornire le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e67-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="f9e67-172">• **File del certificato** scaricato</span><span class="sxs-lookup"><span data-stu-id="f9e67-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="f9e67-173">• **URL servizio Single Sign-On SAML**</span><span class="sxs-lookup"><span data-stu-id="f9e67-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="f9e67-174">• **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="f9e67-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="f9e67-175">• **URL di disconnessione**</span><span class="sxs-lookup"><span data-stu-id="f9e67-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="f9e67-176">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9e67-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9e67-177">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f9e67-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9e67-178">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9e67-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9e67-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9e67-180">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e67-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f9e67-182">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f9e67-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9e67-183">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f9e67-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9e67-185">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f9e67-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9e67-187">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9e67-189">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f9e67-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9e67-191">a.</span><span class="sxs-lookup"><span data-stu-id="f9e67-191">a.</span></span> <span data-ttu-id="f9e67-192">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9e67-193">b.</span><span class="sxs-lookup"><span data-stu-id="f9e67-193">b.</span></span> <span data-ttu-id="f9e67-194">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f9e67-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9e67-195">c.</span><span class="sxs-lookup"><span data-stu-id="f9e67-195">c.</span></span> <span data-ttu-id="f9e67-196">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9e67-197">d.</span><span class="sxs-lookup"><span data-stu-id="f9e67-197">d.</span></span> <span data-ttu-id="f9e67-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="f9e67-199">Creazione di un utente test WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="f9e67-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="f9e67-200">In questa sezione viene creato un utente di nome Britta Simon in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="f9e67-201">Collaborare con il [team di supporto di WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) per aggiungere gli utenti alla piattaforma WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9e67-202">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9e67-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9e67-203">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f9e67-205">**Per assegnare Britta Simon a WORKS MOBILE, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f9e67-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="f9e67-206">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f9e67-208">Selezionare **WORKS MOBILE**dall'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f9e67-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="f9e67-210">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f9e67-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f9e67-212">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-212">Click **Add** button.</span></span> <span data-ttu-id="f9e67-213">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f9e67-215">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f9e67-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9e67-216">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9e67-217">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f9e67-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9e67-218">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f9e67-218">Testing single sign-on</span></span>

<span data-ttu-id="f9e67-219">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f9e67-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f9e67-220">Quando si fa clic sul riquadro WORKS MOBILE nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="f9e67-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="f9e67-221">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9e67-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f9e67-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f9e67-222">Additional resources</span></span>

* [<span data-ttu-id="f9e67-223">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9e67-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9e67-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9e67-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

