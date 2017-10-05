---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learning Seat LMS | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Learning Seat LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="e7fb0-103">Esercitazione: Integrazione di Azure Active Directory con Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="e7fb0-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="e7fb0-104">Questa esercitazione descrive come integrare Learning Seat LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7fb0-105">L'integrazione di Learning Seat LMS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7fb0-106">È possibile controllare in Azure AD chi può accedere a Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="e7fb0-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="e7fb0-107">È possibile abilitare gli utenti per l'accesso automatico a Learning Seat LMS (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="e7fb0-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7fb0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7fb0-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e7fb0-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7fb0-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e7fb0-111">Prerequisites</span></span>

<span data-ttu-id="e7fb0-112">Per configurare l'integrazione di Azure AD con Learning Seat LMS, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="e7fb0-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e7fb0-114">Sottoscrizione di Learning Seat LMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7fb0-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7fb0-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7fb0-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7fb0-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7fb0-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7fb0-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e7fb0-119">Scenario description</span></span>
<span data-ttu-id="e7fb0-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7fb0-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7fb0-122">Aggiunta di Learning Seat LMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e7fb0-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="e7fb0-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7fb0-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="e7fb0-124">Aggiunta di Learning Seat LMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e7fb0-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="e7fb0-125">Per configurare l'integrazione di Learning Seat LMS in Azure AD, è necessario aggiungere Learning Seat LMS dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7fb0-126">**Per aggiungere Learning Seat LMS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7fb0-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7fb0-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7fb0-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7fb0-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e7fb0-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e7fb0-134">Nella casella di ricerca digitare **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="e7fb0-136">Nel pannello dei risultati selezionare **Learning Seat LMS** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7fb0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7fb0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7fb0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Learning Seat LMS usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7fb0-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7fb0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Learning Seat LMS corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="e7fb0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="e7fb0-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="e7fb0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Learning Seat LMS, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7fb0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7fb0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7fb0-145">**[Creazione di un utente di test di Learning Seat LMS](#creating-a-learnconnect-test-user)**: per avere una controparte di Britta Simon in Learning Seat LMS collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7fb0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7fb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7fb0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7fb0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7fb0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="e7fb0-150">**Per configurare l'accesso Single Sign-On di Azure AD con Learning Seat LMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7fb0-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="e7fb0-151">Nella pagina di integrazione dell'applicazione **Learning Seat LMS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e7fb0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="e7fb0-155">Nella sezione **URL e dominio Learning Seat LMS** se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="e7fb0-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-157">a.</span></span> <span data-ttu-id="e7fb0-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="e7fb0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="e7fb0-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-159">b.</span></span> <span data-ttu-id="e7fb0-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="e7fb0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="e7fb0-161">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="e7fb0-163">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="e7fb0-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e7fb0-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="e7fb0-164">These values are not the real values.</span></span> <span data-ttu-id="e7fb0-165">è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="e7fb0-166">Per ottenere questi valori, contattare il [team di supporto clienti di Learning Seat](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="e7fb0-167">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="e7fb0-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e7fb0-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e7fb0-171">Per configurare l'accesso Single Sign-On sul lato **Learning Seat LMS**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Learning Seat LMS](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="e7fb0-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7fb0-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7fb0-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7fb0-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7fb0-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="e7fb0-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e7fb0-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7fb0-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7fb0-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7fb0-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7fb0-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7fb0-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7fb0-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7fb0-187">a.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-187">a.</span></span> <span data-ttu-id="e7fb0-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7fb0-189">b.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-189">b.</span></span> <span data-ttu-id="e7fb0-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7fb0-191">c.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-191">c.</span></span> <span data-ttu-id="e7fb0-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7fb0-193">d.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-193">d.</span></span> <span data-ttu-id="e7fb0-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="e7fb0-195">Creazione di un utente di test di Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="e7fb0-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="e7fb0-196">In questa sezione viene creato un utente di nome Britta Simon in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="e7fb0-197">Contattare il [team di supporto di Learning Seat](http://help.learningseatlms.com/help) con tutte le informazioni dell'utente per aggiungere gli utenti all'applicazione Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7fb0-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7fb0-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7fb0-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e7fb0-201">**Per assegnare Britta Simon a Learning Seat LMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7fb0-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="e7fb0-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e7fb0-204">Nell'elenco delle applicazioni selezionare **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="e7fb0-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e7fb0-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-208">Click **Add** button.</span></span> <span data-ttu-id="e7fb0-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e7fb0-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7fb0-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7fb0-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7fb0-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7fb0-214">Testing single sign-on</span></span>

<span data-ttu-id="e7fb0-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="e7fb0-216">Quando si fa clic sul riquadro Learning Seat LMS nel pannello di accesso, si accederà automaticamente all'applicazione Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="e7fb0-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="e7fb0-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="e7fb0-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7fb0-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e7fb0-218">Additional resources</span></span>

* [<span data-ttu-id="e7fb0-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7fb0-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7fb0-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7fb0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

