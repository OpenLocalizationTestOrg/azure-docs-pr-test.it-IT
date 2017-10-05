---
title: 'Esercitazione: Integrazione di Azure Active Directory con Nexonia | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Nexonia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="51bfb-103">Esercitazione: Integrazione di Azure Active Directory con Nexonia</span><span class="sxs-lookup"><span data-stu-id="51bfb-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="51bfb-104">In questa esercitazione è descritto come integrare Nexonia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51bfb-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51bfb-105">L'integrazione di Nexonia con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="51bfb-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51bfb-106">È possibile controllare in Azure AD chi può accedere a Nexonia</span><span class="sxs-lookup"><span data-stu-id="51bfb-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="51bfb-107">È possibile abilitare gli utenti per l'accesso automatico a Nexonia (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51bfb-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bfb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="51bfb-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="51bfb-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="51bfb-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51bfb-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51bfb-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="51bfb-111">Prerequisites</span></span>

<span data-ttu-id="51bfb-112">Per configurare l'integrazione di Azure AD con Nexonia, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="51bfb-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="51bfb-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51bfb-113">An Azure AD subscription</span></span>
- <span data-ttu-id="51bfb-114">Sottoscrizione di Nexonia abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="51bfb-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51bfb-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="51bfb-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51bfb-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="51bfb-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51bfb-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="51bfb-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51bfb-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51bfb-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51bfb-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="51bfb-119">Scenario description</span></span>
<span data-ttu-id="51bfb-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="51bfb-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51bfb-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="51bfb-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51bfb-122">Aggiunta di Nexonia dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="51bfb-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="51bfb-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="51bfb-124">Aggiunta di Nexonia dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="51bfb-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="51bfb-125">Per configurare l'integrazione di Nexonia in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="51bfb-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51bfb-126">**Per aggiungere Nexonia dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="51bfb-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51bfb-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="51bfb-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51bfb-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51bfb-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="51bfb-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="51bfb-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="51bfb-134">Nella casella di ricerca digitare **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-134">In the search box, type **Nexonia**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="51bfb-136">Nel pannello dei risultati selezionare **Nexonia** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="51bfb-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51bfb-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51bfb-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Nexonia in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="51bfb-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51bfb-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Nexonia che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51bfb-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="51bfb-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="51bfb-142">Per stabilire la relazione di collegamento, in Nexonia assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="51bfb-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Nexonia, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="51bfb-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51bfb-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="51bfb-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51bfb-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51bfb-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51bfb-146">**[Creazione di un utente test di Nexonia](#creating-a-nexonia-test-user)**: per avere una controparte di Britta Simon in Nexonia collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="51bfb-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51bfb-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51bfb-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51bfb-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="51bfb-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51bfb-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51bfb-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="51bfb-151">In caso di problemi di integrazione, fare riferimento a questo [collegamento](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) per una guida alla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="51bfb-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="51bfb-152">Se non è stata trovata una soluzione, creare una richiesta di supporto dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bfb-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="51bfb-153">**Per configurare l'accesso Single Sign-On di Azure AD con Nexonia, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="51bfb-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="51bfb-154">Nella pagina di integrazione dell'applicazione **Nexonia** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="51bfb-156">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="51bfb-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="51bfb-158">Nella sezione **URL e dominio Nexonia** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="51bfb-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="51bfb-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="51bfb-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51bfb-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="51bfb-161">This value is not real.</span></span> <span data-ttu-id="51bfb-162">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="51bfb-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="51bfb-163">Per ottenere tale valore, contattare il team di supporto di [Nexonia](https://nexonia.zendesk.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="51bfb-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="51bfb-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="51bfb-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="51bfb-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="51bfb-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51bfb-168">Nella sezione **Configurazione di Nexonia** fare clic su **Configura Nexonia** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="51bfb-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="51bfb-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="51bfb-171">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il [team di supporto di Nexonia](https://nexonia.zendesk.com/hc/requests/new) e fornire i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="51bfb-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="51bfb-172">• **Certificato**</span><span class="sxs-lookup"><span data-stu-id="51bfb-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="51bfb-173">• **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="51bfb-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="51bfb-174">• **URL servizio Single Sign-On SAML**</span><span class="sxs-lookup"><span data-stu-id="51bfb-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="51bfb-175">• **URL di disconnessione**</span><span class="sxs-lookup"><span data-stu-id="51bfb-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="51bfb-176">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="51bfb-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51bfb-177">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="51bfb-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51bfb-178">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51bfb-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51bfb-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="51bfb-180">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bfb-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="51bfb-182">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="51bfb-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51bfb-183">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="51bfb-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51bfb-185">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="51bfb-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51bfb-187">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51bfb-189">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="51bfb-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51bfb-191">a.</span><span class="sxs-lookup"><span data-stu-id="51bfb-191">a.</span></span> <span data-ttu-id="51bfb-192">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51bfb-193">b.</span><span class="sxs-lookup"><span data-stu-id="51bfb-193">b.</span></span> <span data-ttu-id="51bfb-194">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="51bfb-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51bfb-195">c.</span><span class="sxs-lookup"><span data-stu-id="51bfb-195">c.</span></span> <span data-ttu-id="51bfb-196">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="51bfb-197">d.</span><span class="sxs-lookup"><span data-stu-id="51bfb-197">d.</span></span> <span data-ttu-id="51bfb-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="51bfb-199">Creazione di un utente test di Nexonia</span><span class="sxs-lookup"><span data-stu-id="51bfb-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="51bfb-200">In questa sezione viene creato un utente di nome Britta Simon in Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="51bfb-201">Collaborare con il [team di supporto di Nexonia](https://nexonia.zendesk.com/hc/requests/new) per aggiungere gli utenti alla piattaforma Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="51bfb-202">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="51bfb-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="51bfb-203">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="51bfb-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="51bfb-204">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure con la concessione dell'accesso a Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Assegna utente][200] 

<span data-ttu-id="51bfb-206">**Per assegnare Britta Simon a Nexonia, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="51bfb-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="51bfb-207">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="51bfb-209">Selezionare **Nexonia** dall'elenco di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="51bfb-209">In the applications list, select **Nexonia**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="51bfb-211">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="51bfb-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="51bfb-213">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-213">Click **Add** button.</span></span> <span data-ttu-id="51bfb-214">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="51bfb-216">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="51bfb-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51bfb-217">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51bfb-218">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="51bfb-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51bfb-219">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="51bfb-219">Testing single sign-on</span></span>

<span data-ttu-id="51bfb-220">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="51bfb-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="51bfb-221">Quando si fa clic sul riquadro Nexonia nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Nexonia.</span><span class="sxs-lookup"><span data-stu-id="51bfb-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="51bfb-222">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="51bfb-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51bfb-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="51bfb-223">Additional resources</span></span>

* [<span data-ttu-id="51bfb-224">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51bfb-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51bfb-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51bfb-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

