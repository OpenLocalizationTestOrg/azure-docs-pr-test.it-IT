---
title: 'Esercitazione: Integrazione di Azure Active Directory con Alcumus Info Exchange | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Alcumus Info Exchange.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 1f67682111de0bea1b18fd97d739492661ebbfd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="37bb6-103">Esercitazione: Integrazione di Azure Active Directory con Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="37bb6-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="37bb6-104">Questa esercitazione descrive come integrare Alcumus Info Exchange con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37bb6-104">In this tutorial, you learn how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37bb6-105">L'integrazione di Alcumus Info Exchange con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="37bb6-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37bb6-106">È possibile controllare in Azure AD chi può accedere ad Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-106">You can control in Azure AD who has access to Alcumus Info Exchange</span></span>
- <span data-ttu-id="37bb6-107">È possibile abilitare gli utenti per l'accesso automatico ad Alcumus Info Exchange (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37bb6-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37bb6-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37bb6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37bb6-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37bb6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37bb6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="37bb6-110">Prerequisites</span></span>

<span data-ttu-id="37bb6-111">Per configurare l'integrazione di Azure AD con Alcumus Info Exchange, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="37bb6-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span></span>

- <span data-ttu-id="37bb6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37bb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37bb6-113">Sottoscrizione di Alcumus Info Exchange abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="37bb6-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37bb6-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="37bb6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37bb6-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="37bb6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37bb6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="37bb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37bb6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37bb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37bb6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="37bb6-118">Scenario description</span></span>
<span data-ttu-id="37bb6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="37bb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37bb6-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="37bb6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37bb6-121">Aggiunta di Alcumus Info Exchange dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="37bb6-121">Adding Alcumus Info Exchange from the gallery</span></span>
2. <span data-ttu-id="37bb6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37bb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-the-gallery"></a><span data-ttu-id="37bb6-123">Aggiunta di Alcumus Info Exchange dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="37bb6-123">Adding Alcumus Info Exchange from the gallery</span></span>
<span data-ttu-id="37bb6-124">Per configurare l'integrazione di Alcumus Info Exchange in Azure AD, è necessario aggiungere Alcumus Info Exchange dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="37bb6-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37bb6-125">**Per aggiungere Alcumus Info Exchange dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="37bb6-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37bb6-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="37bb6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37bb6-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37bb6-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="37bb6-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="37bb6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="37bb6-133">Nella casella di ricerca, digitare **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-133">In the search box, type **Alcumus Info Exchange**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="37bb6-135">Nel pannello dei risultati selezionare **Alcumus Info Exchange** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="37bb6-135">In the results panel, select **Alcumus Info Exchange**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37bb6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37bb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37bb6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Alcumus Info Exchange usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="37bb6-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37bb6-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Alcumus Info Exchange che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37bb6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange is to a user in Azure AD.</span></span> <span data-ttu-id="37bb6-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente Azure AD e l’utente correlato in Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-140">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span></span>

<span data-ttu-id="37bb6-141">Per stabilire la relazione di collegamento, in Alcumus Info Exchange assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-141">In Alcumus Info Exchange, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37bb6-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Alcumus Info Exchange, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="37bb6-142">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37bb6-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="37bb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37bb6-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37bb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37bb6-145">**[Creazione di un utente test di Alcumus Info Exchange](#creating-an-alcumus-info-exchange-test-user)** : per avere una controparte di Britta Simon in Alcumus Info Exchange collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37bb6-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37bb6-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37bb6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37bb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="37bb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37bb6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37bb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37bb6-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="37bb6-150">**Per configurare Single Sign-On di Azure AD con Alcumus Info Exchange, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="37bb6-150">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="37bb6-151">Nella pagina di integrazione dell'applicazione **Alcumus Info Exchange** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-151">In the Azure portal, on the **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="37bb6-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="37bb6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="37bb6-155">Nella sezione **dominio e URL di Alcumus Info Exchange** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="37bb6-155">On the **Alcumus Info Exchange Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="37bb6-157">a.</span><span class="sxs-lookup"><span data-stu-id="37bb6-157">a.</span></span> <span data-ttu-id="37bb6-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="37bb6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="37bb6-159">b.</span><span class="sxs-lookup"><span data-stu-id="37bb6-159">b.</span></span> <span data-ttu-id="37bb6-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="37bb6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37bb6-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="37bb6-161">These values are not real.</span></span> <span data-ttu-id="37bb6-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="37bb6-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="37bb6-163">Contattare il [team di supporto di Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com) per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="37bb6-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) to get these values.</span></span>
 
4. <span data-ttu-id="37bb6-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="37bb6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="37bb6-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="37bb6-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37bb6-168">Per configurare l'accesso Single Sign-On sul lato **Alcumus Info Exchange**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="37bb6-168">To configure single sign-on on **Alcumus Info Exchange** side, you need to send the downloaded **Metadata XML** to [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="37bb6-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="37bb6-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37bb6-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="37bb6-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37bb6-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37bb6-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37bb6-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37bb6-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="37bb6-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37bb6-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="37bb6-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="37bb6-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37bb6-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="37bb6-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37bb6-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="37bb6-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37bb6-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37bb6-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="37bb6-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37bb6-184">a.</span><span class="sxs-lookup"><span data-stu-id="37bb6-184">a.</span></span> <span data-ttu-id="37bb6-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37bb6-186">b.</span><span class="sxs-lookup"><span data-stu-id="37bb6-186">b.</span></span> <span data-ttu-id="37bb6-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37bb6-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37bb6-188">c.</span><span class="sxs-lookup"><span data-stu-id="37bb6-188">c.</span></span> <span data-ttu-id="37bb6-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37bb6-190">d.</span><span class="sxs-lookup"><span data-stu-id="37bb6-190">d.</span></span> <span data-ttu-id="37bb6-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="37bb6-192">Creazione di un utente test di Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="37bb6-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="37bb6-193">Questa sezione descrive come creare un utente chiamato Britta Simon in Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-193">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="37bb6-194">Per creare un utente denominato Britta Simon in Alcumus Info Exchange, contattare il [team di supporto di Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="37bb6-194">To create a user called Britta Simon in Alcumus Info Exchange, Contact the [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37bb6-195">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37bb6-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37bb6-196">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Alcumus Info Exchange.</span></span>

![Assegna utente][200] 

<span data-ttu-id="37bb6-198">**Per assegnare Britta Simon ad Alcumus Info Exchange, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="37bb6-198">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="37bb6-199">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="37bb6-201">Nell’elenco delle applicazioni selezionare **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-201">In the applications list, select **Alcumus Info Exchange**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="37bb6-203">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="37bb6-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="37bb6-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-205">Click **Add** button.</span></span> <span data-ttu-id="37bb6-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="37bb6-208">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="37bb6-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37bb6-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37bb6-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="37bb6-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37bb6-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="37bb6-211">Testing single sign-on</span></span>

<span data-ttu-id="37bb6-212">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="37bb6-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="37bb6-213">Quando si fa clic sul riquadro Alcumus Info Exchange nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="37bb6-213">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37bb6-214">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="37bb6-214">Additional resources</span></span>

* [<span data-ttu-id="37bb6-215">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37bb6-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37bb6-216">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37bb6-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

