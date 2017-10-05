---
title: 'Esercitazione: Integrazione di Azure Active Directory con 10,000ft Plans | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e 10,000ft Plans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="eaaba-103">Esercitazione: Integrazione di Azure Active Directory con 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="eaaba-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="eaaba-104">Questa esercitazione descrive come integrare 10,000ft Plans con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eaaba-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eaaba-105">L'integrazione di 10,000ft Plans con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaaba-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eaaba-106">È possibile controllare in Azure AD chi può accedere a 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="eaaba-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="eaaba-107">È possibile abilitare gli utenti per l'accesso automatico a 10,000ft Plans (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaaba-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eaaba-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaaba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eaaba-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eaaba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eaaba-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eaaba-110">Prerequisites</span></span>

<span data-ttu-id="eaaba-111">Per configurare l'integrazione di Azure AD con 10,000ft Plans, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaaba-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="eaaba-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaaba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eaaba-113">Sottoscrizione di 10,000ft Plans abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eaaba-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eaaba-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="eaaba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eaaba-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaaba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eaaba-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="eaaba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eaaba-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eaaba-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eaaba-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="eaaba-118">Scenario description</span></span>
<span data-ttu-id="eaaba-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="eaaba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eaaba-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaaba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eaaba-121">Aggiunta di 10,000ft Plans dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eaaba-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="eaaba-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaaba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="eaaba-123">Aggiunta di 10,000ft Plans dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eaaba-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="eaaba-124">Per configurare l'integrazione di 10,000ft Plans in Azure AD, è necessario aggiungere 10,000ft Plans dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="eaaba-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eaaba-125">**Per aggiungere 10,000ft Plans dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eaaba-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eaaba-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eaaba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eaaba-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eaaba-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="eaaba-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaaba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="eaaba-133">Nella casella di ricerca, digitare **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="eaaba-135">Nel pannello dei risultati selezionare **10,000ft Plans** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaaba-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eaaba-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaaba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eaaba-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 10,000ft Plans usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eaaba-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eaaba-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di 10,000ft Plans che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaaba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="eaaba-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="eaaba-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="eaaba-141">Per stabilire la relazione di collegamento, in 10,000ft Plans assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="eaaba-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eaaba-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con 10,000ft Plans, è necessario completare i passaggi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaaba-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eaaba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eaaba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eaaba-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eaaba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eaaba-145">**[Creazione di un utente test di 10,000ft Plans](#creating-a-10000ft-plans-test-user)**: per avere una controparte di Britta Simon in 10,000ft Plans collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaaba-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eaaba-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaaba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eaaba-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="eaaba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eaaba-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaaba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eaaba-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="eaaba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="eaaba-150">**Per configurare Single Sign-On di Azure AD con 10,000ft Plans, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eaaba-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="eaaba-151">Nella pagina di integrazione dell'applicazione **10,000ft Plans** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="eaaba-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="eaaba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="eaaba-155">Nella sezione **URL e dominio 10,000ft Plans** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eaaba-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="eaaba-157">a.</span><span class="sxs-lookup"><span data-stu-id="eaaba-157">a.</span></span> <span data-ttu-id="eaaba-158">Nella casella di testo **URL accesso** digitare l'URL: `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="eaaba-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="eaaba-159">b.</span><span class="sxs-lookup"><span data-stu-id="eaaba-159">b.</span></span> <span data-ttu-id="eaaba-160">Nella casella di testo **Identificatore** digitare l'URL: `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="eaaba-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eaaba-161">Il valore **Identificatore** è diverso se si dispone di un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="eaaba-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="eaaba-162">Per ottenere tale valore, contattare il [team di supporto di 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="eaaba-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="eaaba-163">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (base)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="eaaba-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="eaaba-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="eaaba-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eaaba-167">Nella sezione **Configurazione di 10,000ft Plans** fare clic su **Configura 10,000ft Plans** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eaaba-168">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="eaaba-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="eaaba-170">Per configurare l'accesso Single Sign-On sul lato **10,000ft Plans**, è necessario inviare il file **Certificato (base) scaricato, l'URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="eaaba-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="eaaba-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="eaaba-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eaaba-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="eaaba-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eaaba-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eaaba-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eaaba-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaaba-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="eaaba-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaaba-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="eaaba-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eaaba-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eaaba-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eaaba-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eaaba-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="eaaba-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eaaba-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eaaba-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eaaba-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eaaba-186">a.</span><span class="sxs-lookup"><span data-stu-id="eaaba-186">a.</span></span> <span data-ttu-id="eaaba-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eaaba-188">b.</span><span class="sxs-lookup"><span data-stu-id="eaaba-188">b.</span></span> <span data-ttu-id="eaaba-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eaaba-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eaaba-190">c.</span><span class="sxs-lookup"><span data-stu-id="eaaba-190">c.</span></span> <span data-ttu-id="eaaba-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eaaba-192">d.</span><span class="sxs-lookup"><span data-stu-id="eaaba-192">d.</span></span> <span data-ttu-id="eaaba-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="eaaba-194">Creazione di un utente test di 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="eaaba-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="eaaba-195">Questa sezione descrive come creare un utente chiamato Britta Simon in 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="eaaba-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="eaaba-196">10,000ft Plans supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eaaba-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="eaaba-197">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eaaba-197">There is no action item for you in this section.</span></span> <span data-ttu-id="eaaba-198">Durante il tentativo di accesso a 10,000ft Plans viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="eaaba-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="eaaba-199">Per creare un utente manualmente è necessario contattare il [team di supporto di 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="eaaba-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eaaba-200">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaaba-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eaaba-201">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="eaaba-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Assegna utente][200] 

<span data-ttu-id="eaaba-203">**Per assegnare Britta Simon a 10,000ft Plans, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eaaba-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="eaaba-204">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="eaaba-206">Nell'elenco delle applicazioni, selezionare **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="eaaba-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="eaaba-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="eaaba-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-210">Click **Add** button.</span></span> <span data-ttu-id="eaaba-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="eaaba-213">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="eaaba-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eaaba-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eaaba-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eaaba-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eaaba-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eaaba-216">Testing single sign-on</span></span>

<span data-ttu-id="eaaba-217">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="eaaba-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="eaaba-218">Quando si fa clic sul riquadro 10,000ft Plans nel pannello di accesso, si accederà automaticamente all'applicazione 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="eaaba-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="eaaba-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eaaba-219">Additional resources</span></span>

* [<span data-ttu-id="eaaba-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eaaba-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eaaba-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eaaba-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

