---
title: 'Esercitazione: Integrazione di Azure Active Directory con QuickHelp | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="b37a6-103">Esercitazione: Integrazione di Azure Active Directory con QuickHelp</span><span class="sxs-lookup"><span data-stu-id="b37a6-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="b37a6-104">Questa esercitazione descrive come integrare QuickHelp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b37a6-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b37a6-105">L'integrazione di QuickHelp con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a6-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b37a6-106">È possibile controllare in Azure AD chi può accedere a QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="b37a6-107">È possibile abilitare gli utenti per l'accesso automatico a QuickHelp (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b37a6-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b37a6-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b37a6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b37a6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b37a6-110">Prerequisites</span></span>

<span data-ttu-id="b37a6-111">Per configurare l'integrazione di Azure AD con QuickHelp, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a6-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="b37a6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b37a6-113">Sottoscrizione di QuickHelp abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b37a6-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b37a6-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b37a6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b37a6-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b37a6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b37a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b37a6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b37a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b37a6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b37a6-118">Scenario description</span></span>
<span data-ttu-id="b37a6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b37a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b37a6-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b37a6-121">Aggiunta di QuickHelp dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b37a6-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="b37a6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b37a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="b37a6-123">Aggiunta di QuickHelp dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b37a6-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="b37a6-124">Per configurare l'integrazione di QuickHelp in Azure AD, è necessario aggiungere QuickHelp dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b37a6-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b37a6-125">**Per aggiungere QuickHelp dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b37a6-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b37a6-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b37a6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b37a6-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b37a6-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b37a6-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b37a6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b37a6-133">Nella casella di ricerca digitare **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-133">In the search box, type **QuickHelp**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="b37a6-135">Nel pannello dei risultati selezionare **QuickHelp** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b37a6-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b37a6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b37a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b37a6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con QuickHelp in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b37a6-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b37a6-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di QuickHelp che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="b37a6-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="b37a6-141">Per stabilire la relazione di collegamento, in QuickHelp assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b37a6-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con QuickHelp, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a6-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b37a6-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b37a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b37a6-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b37a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b37a6-145">**[Creazione di un utente di test di QuickHelp](#creating-a-quickhelp-test-user)**: per avere una controparte di Britta Simon in QuickHelp collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b37a6-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b37a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b37a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b37a6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b37a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b37a6-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="b37a6-150">**Per configurare Single Sign-On di Azure AD con QuickHelp, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b37a6-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="b37a6-151">Nella pagina di integrazione dell'applicazione **QuickHelp** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b37a6-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b37a6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="b37a6-155">Nella sezione **URL e dominio QuickHelp** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b37a6-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="b37a6-157">a.</span><span class="sxs-lookup"><span data-stu-id="b37a6-157">a.</span></span> <span data-ttu-id="b37a6-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://quickhelp.com/<instancename>/#/Login`.</span><span class="sxs-lookup"><span data-stu-id="b37a6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="b37a6-159">b.</span><span class="sxs-lookup"><span data-stu-id="b37a6-159">b.</span></span> <span data-ttu-id="b37a6-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="b37a6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b37a6-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b37a6-161">These values are not real.</span></span> <span data-ttu-id="b37a6-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="b37a6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b37a6-163">Per ottenere questi valori, contattare il [team di supporto client di QuickHelp](https://support.quickhelp.com/).</span><span class="sxs-lookup"><span data-stu-id="b37a6-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="b37a6-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="b37a6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="b37a6-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b37a6-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="b37a6-168">Accedere al sito aziendale di QuickHelp come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b37a6-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="b37a6-169">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On][21]

8. <span data-ttu-id="b37a6-171">Nel menu **QuickHelp Admin** fare clic su **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configura accesso Single Sign-On][22]

9. <span data-ttu-id="b37a6-173">Fare clic su **Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="b37a6-174">Nella pagina **Authentication Settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b37a6-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configura accesso Single Sign-On][23]
   
    <span data-ttu-id="b37a6-176">a.</span><span class="sxs-lookup"><span data-stu-id="b37a6-176">a.</span></span> <span data-ttu-id="b37a6-177">Come **tipo SSO**, selezionare **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="b37a6-178">b.</span><span class="sxs-lookup"><span data-stu-id="b37a6-178">b.</span></span> <span data-ttu-id="b37a6-179">Per caricare il file dei metadati di Azure scaricato, fare clic su **Sfoglia**, passare al file e quindi fare clic su **Carica metadati**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="b37a6-180">c.</span><span class="sxs-lookup"><span data-stu-id="b37a6-180">c.</span></span> <span data-ttu-id="b37a6-181">Nella casella di testo **Email** (Posta elettronica) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="b37a6-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="b37a6-182">d.</span><span class="sxs-lookup"><span data-stu-id="b37a6-182">d.</span></span> <span data-ttu-id="b37a6-183">Nella casella di testo **Nome** digitare `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="b37a6-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="b37a6-184">e.</span><span class="sxs-lookup"><span data-stu-id="b37a6-184">e.</span></span> <span data-ttu-id="b37a6-185">Nella casella di testo **Cognome** digitare `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="b37a6-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="b37a6-186">f.</span><span class="sxs-lookup"><span data-stu-id="b37a6-186">f.</span></span> <span data-ttu-id="b37a6-187">Nella **barra delle azioni**, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b37a6-188">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b37a6-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b37a6-189">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b37a6-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b37a6-190">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b37a6-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b37a6-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b37a6-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="b37a6-192">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a6-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b37a6-194">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b37a6-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b37a6-195">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b37a6-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b37a6-197">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b37a6-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b37a6-199">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b37a6-201">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b37a6-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b37a6-203">a.</span><span class="sxs-lookup"><span data-stu-id="b37a6-203">a.</span></span> <span data-ttu-id="b37a6-204">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b37a6-205">b.</span><span class="sxs-lookup"><span data-stu-id="b37a6-205">b.</span></span> <span data-ttu-id="b37a6-206">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b37a6-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b37a6-207">c.</span><span class="sxs-lookup"><span data-stu-id="b37a6-207">c.</span></span> <span data-ttu-id="b37a6-208">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b37a6-209">d.</span><span class="sxs-lookup"><span data-stu-id="b37a6-209">d.</span></span> <span data-ttu-id="b37a6-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="b37a6-211">Creazione di un utente test di QuickHelp</span><span class="sxs-lookup"><span data-stu-id="b37a6-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="b37a6-212">Questa sezione descrive come creare un utente chiamato Britta Simon in QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="b37a6-213">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di QuickHelp che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="b37a6-214">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="b37a6-215">QuickHelp supporta il provisioning just-in-time.</span><span class="sxs-lookup"><span data-stu-id="b37a6-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="b37a6-216">Ciò significa che, se necessario, un account utente viene creato automaticamente in QuickHelp e che l'account è collegato all'account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b37a6-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="b37a6-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b37a6-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b37a6-218">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b37a6-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b37a6-219">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b37a6-221">**Per assegnare Britta Simon a QuickHelp, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b37a6-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="b37a6-222">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b37a6-224">Nell'elenco delle applicazioni selezionare **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-224">In the applications list, select **QuickHelp**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="b37a6-226">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b37a6-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b37a6-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-228">Click **Add** button.</span></span> <span data-ttu-id="b37a6-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b37a6-231">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b37a6-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b37a6-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b37a6-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b37a6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b37a6-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b37a6-234">Testing single sign-on</span></span>

<span data-ttu-id="b37a6-235">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b37a6-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="b37a6-236">Quando si fa clic sul riquadro QuickHelp nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="b37a6-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b37a6-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b37a6-237">Additional resources</span></span>

* [<span data-ttu-id="b37a6-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b37a6-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b37a6-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b37a6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
