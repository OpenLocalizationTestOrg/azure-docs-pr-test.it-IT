---
title: 'Esercitazione: Integrazione di Azure Active Directory con Origami | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Origami
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="30665-103">Esercitazione: Integrazione di Azure Active Directory con Origami</span><span class="sxs-lookup"><span data-stu-id="30665-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="30665-104">Questa esercitazione descrive come integrare Origami con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30665-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30665-105">L'integrazione di Origami con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="30665-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="30665-106">È possibile controllare in Azure AD chi può accedere a Origami</span><span class="sxs-lookup"><span data-stu-id="30665-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="30665-107">È possibile abilitare gli utenti perché possano accedere automaticamente a Origami (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30665-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30665-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="30665-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30665-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30665-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30665-110">Prerequisites</span></span>

<span data-ttu-id="30665-111">Per configurare l'integrazione di Azure AD con Origami, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="30665-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="30665-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30665-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30665-113">Sottoscrizione di Origami abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="30665-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30665-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="30665-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30665-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="30665-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30665-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="30665-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30665-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30665-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30665-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="30665-118">Scenario description</span></span>
<span data-ttu-id="30665-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="30665-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30665-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="30665-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30665-121">Aggiunta di Origami dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="30665-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="30665-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="30665-123">Aggiunta di Origami dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="30665-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="30665-124">Per configurare l'integrazione di Origami in Azure AD, è necessario aggiungere Origami dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="30665-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="30665-125">**Per aggiungere Origami dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30665-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="30665-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="30665-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30665-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="30665-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="30665-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="30665-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="30665-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="30665-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="30665-133">Nella casella di ricerca digitare **Origami**.</span><span class="sxs-lookup"><span data-stu-id="30665-133">In the search box, type **Origami**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="30665-135">Nel pannello dei risultati selezionare **Origami** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="30665-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30665-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30665-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Origami con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="30665-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30665-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Origami che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30665-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="30665-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Origami.</span><span class="sxs-lookup"><span data-stu-id="30665-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="30665-141">Per stabilire la relazione di collegamento, in Origami assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="30665-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="30665-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Origami, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="30665-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="30665-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="30665-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="30665-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30665-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30665-145">**[Creazione di un utente test di Origami](#creating-an-origami-test-user)**: per avere una controparte di Britta Simon in Origami collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30665-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="30665-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30665-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30665-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="30665-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30665-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30665-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Origami.</span><span class="sxs-lookup"><span data-stu-id="30665-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="30665-150">**Per configurare l'accesso Single Sign-On di Azure AD con Origami, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30665-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="30665-151">Nella pagina di integrazione dell'applicazione **Origami** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="30665-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="30665-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="30665-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="30665-155">Nella sezione **URL e dominio Origami** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="30665-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="30665-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="30665-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30665-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="30665-158">The value is not real.</span></span> <span data-ttu-id="30665-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="30665-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="30665-160">Per ottenere tale valore, contattare il [team di supporto clienti di Origami](https://wordpress.org/support/theme/origami).</span><span class="sxs-lookup"><span data-stu-id="30665-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="30665-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="30665-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="30665-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="30665-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30665-165">Nella sezione **Configurazione di Origami** fare clic su **Configura Origami** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="30665-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="30665-166">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="30665-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="30665-168">Accedere all'account Origami con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="30665-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="30665-169">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="30665-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="30665-171">Nella pagina della finestra di dialogo Single Sign On Setup (Imposta accesso Single Sign-On) eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="30665-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="30665-173">a.</span><span class="sxs-lookup"><span data-stu-id="30665-173">a.</span></span> <span data-ttu-id="30665-174">Selezionare **Abilita Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="30665-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="30665-175">b.</span><span class="sxs-lookup"><span data-stu-id="30665-175">b.</span></span> <span data-ttu-id="30665-176">Nella casella di testo **URL della pagina di accesso del provider di identità** incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30665-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="30665-177">c.</span><span class="sxs-lookup"><span data-stu-id="30665-177">c.</span></span> <span data-ttu-id="30665-178">Nella casella di testo **URL della pagina di disconnessione del provider di identità** incollare il valore di **URL disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30665-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="30665-179">d.</span><span class="sxs-lookup"><span data-stu-id="30665-179">d.</span></span> <span data-ttu-id="30665-180">Fare clic su **Sfoglia** per caricare il certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30665-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="30665-181">e.</span><span class="sxs-lookup"><span data-stu-id="30665-181">e.</span></span> <span data-ttu-id="30665-182">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="30665-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="30665-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="30665-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="30665-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="30665-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="30665-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30665-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30665-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="30665-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30665-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="30665-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30665-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="30665-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="30665-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30665-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="30665-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30665-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="30665-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30665-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="30665-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30665-198">a.</span><span class="sxs-lookup"><span data-stu-id="30665-198">a.</span></span> <span data-ttu-id="30665-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30665-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30665-200">b.</span><span class="sxs-lookup"><span data-stu-id="30665-200">b.</span></span> <span data-ttu-id="30665-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30665-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30665-202">c.</span><span class="sxs-lookup"><span data-stu-id="30665-202">c.</span></span> <span data-ttu-id="30665-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="30665-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="30665-204">d.</span><span class="sxs-lookup"><span data-stu-id="30665-204">d.</span></span> <span data-ttu-id="30665-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="30665-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="30665-206">Creazione di un utente test in Origami</span><span class="sxs-lookup"><span data-stu-id="30665-206">Creating an Origami test user</span></span>

<span data-ttu-id="30665-207">In questa sezione viene creato un utente di nome Britta Simon in Origami.</span><span class="sxs-lookup"><span data-stu-id="30665-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="30665-208">Accedere all'account Origami con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="30665-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="30665-209">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="30665-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="30665-211">Nella finestra di dialogo **Users and Security** (Utenti e sicurezza) fare clic su **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="30665-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="30665-213">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="30665-213">Click **Add New User**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="30665-215">Nella finestra di dialogo Add New User seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="30665-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="30665-217">a.</span><span class="sxs-lookup"><span data-stu-id="30665-217">a.</span></span> <span data-ttu-id="30665-218">Nella casella di testo **Username** (Nome utente) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="30665-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="30665-219">b.</span><span class="sxs-lookup"><span data-stu-id="30665-219">b.</span></span> <span data-ttu-id="30665-220">Nella casella di testo **Password** digitare una password.</span><span class="sxs-lookup"><span data-stu-id="30665-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="30665-221">c.</span><span class="sxs-lookup"><span data-stu-id="30665-221">c.</span></span> <span data-ttu-id="30665-222">Nella casella di testo **Conferma password** digitare di nuovo la password.</span><span class="sxs-lookup"><span data-stu-id="30665-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="30665-223">d.</span><span class="sxs-lookup"><span data-stu-id="30665-223">d.</span></span> <span data-ttu-id="30665-224">Nella casella di testo **First Name** (Nome) immettere il nome dell'utente, ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="30665-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="30665-225">e.</span><span class="sxs-lookup"><span data-stu-id="30665-225">e.</span></span> <span data-ttu-id="30665-226">Nella casella di testo **Last Name** (Cognome) immettere il cognome dell'utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="30665-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="30665-227">f.</span><span class="sxs-lookup"><span data-stu-id="30665-227">f.</span></span> <span data-ttu-id="30665-228">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="30665-228">Click **Save**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="30665-230">Assegnare i **ruoli utente** e l'**accesso client** all'utente.</span><span class="sxs-lookup"><span data-stu-id="30665-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="30665-232">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30665-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="30665-233">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Origami.</span><span class="sxs-lookup"><span data-stu-id="30665-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Assegna utente][200] 

<span data-ttu-id="30665-235">**Per assegnare Britta Simon a Origami, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30665-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="30665-236">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="30665-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="30665-238">Nell'elenco di applicazioni, selezionare **Origami**.</span><span class="sxs-lookup"><span data-stu-id="30665-238">In the applications list, select **Origami**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="30665-240">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="30665-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="30665-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="30665-242">Click **Add** button.</span></span> <span data-ttu-id="30665-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="30665-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="30665-245">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="30665-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="30665-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="30665-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30665-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="30665-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30665-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="30665-248">Testing single sign-on</span></span>

<span data-ttu-id="30665-249">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="30665-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="30665-250">Quando si fa clic sul riquadro Origami nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Origami.</span><span class="sxs-lookup"><span data-stu-id="30665-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30665-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="30665-251">Additional resources</span></span>

* [<span data-ttu-id="30665-252">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30665-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30665-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30665-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

