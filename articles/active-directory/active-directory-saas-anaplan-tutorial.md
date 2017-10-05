---
title: 'Esercitazione: Integrazione di Azure Active Directory con Anaplan | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Anaplan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: c2ecfd5f066ed3bd10f74f935de2f2b80057329f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="a2f13-103">Esercitazione: Integrazione di Azure Active Directory con Anaplan</span><span class="sxs-lookup"><span data-stu-id="a2f13-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="a2f13-104">Questa esercitazione descrive come integrare Anaplan con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2f13-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2f13-105">L'integrazione di Anaplan con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2f13-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2f13-106">È possibile controllare in Azure AD chi può accedere ad Anaplan</span><span class="sxs-lookup"><span data-stu-id="a2f13-106">You can control in Azure AD who has access to Anaplan</span></span>
- <span data-ttu-id="a2f13-107">È possibile abilitare gli utenti per l'accesso automatico ad Anaplan (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2f13-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f13-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a2f13-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2f13-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2f13-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a2f13-110">Prerequisites</span></span>

<span data-ttu-id="a2f13-111">Per configurare l'integrazione di Azure AD con Anaplan, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2f13-111">To configure Azure AD integration with Anaplan, you need the following items:</span></span>

- <span data-ttu-id="a2f13-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2f13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2f13-113">Sottoscrizione di Anaplan abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a2f13-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2f13-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a2f13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2f13-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2f13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2f13-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a2f13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2f13-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2f13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2f13-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a2f13-118">Scenario description</span></span>
<span data-ttu-id="a2f13-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a2f13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2f13-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2f13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2f13-121">Aggiunta di Anaplan dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a2f13-121">Adding Anaplan from the gallery</span></span>
2. <span data-ttu-id="a2f13-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-the-gallery"></a><span data-ttu-id="a2f13-123">Aggiunta di Anaplan dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a2f13-123">Adding Anaplan from the gallery</span></span>
<span data-ttu-id="a2f13-124">Per configurare l'integrazione di Anaplan in Azure AD, è necessario aggiungere Anaplan dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a2f13-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2f13-125">**Per aggiungere Anaplan dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a2f13-125">**To add Anaplan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2f13-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a2f13-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2f13-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2f13-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a2f13-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2f13-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a2f13-133">Nella casella di ricerca digitare **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-133">In the search box, type **Anaplan**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="a2f13-135">Nel pannello dei risultati selezionare **Anaplan** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2f13-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2f13-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2f13-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Anaplan in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a2f13-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2f13-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Anaplan che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2f13-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span></span> <span data-ttu-id="a2f13-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span></span>

<span data-ttu-id="a2f13-141">Per stabilire la relazione di collegamento, in Anaplan assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a2f13-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2f13-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Anaplan, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2f13-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2f13-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a2f13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a2f13-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2f13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2f13-145">**[Creazione di un utente test di Anaplan](#creating-an-anaplan-test-user)** : per avere una controparte di Britta Simon in Anaplan collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2f13-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2f13-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2f13-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a2f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2f13-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2f13-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="a2f13-150">**Per configurare l'accesso Single Sign-On di Azure AD con Anaplan, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a2f13-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="a2f13-151">Nella pagina di integrazione dell'applicazione **Anaplan** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a2f13-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a2f13-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="a2f13-155">Nella sezione **URL e dominio Anaplan** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="a2f13-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="a2f13-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2f13-157">a.</span></span> <span data-ttu-id="a2f13-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`.</span><span class="sxs-lookup"><span data-stu-id="a2f13-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="a2f13-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2f13-159">b.</span></span> <span data-ttu-id="a2f13-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="a2f13-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2f13-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a2f13-161">These values are not real.</span></span> <span data-ttu-id="a2f13-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="a2f13-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a2f13-163">Per ottenere questi valori, contattare il [team di supporto clienti di Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="a2f13-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a2f13-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="a2f13-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="a2f13-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a2f13-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2f13-168">Nella sezione **Configurazione di Anaplan** fare clic su **Configura Anaplan** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a2f13-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a2f13-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="a2f13-171">Per configurare l'accesso Single Sign-On sul lato **Anaplan**, è necessario inviare il file di **XML metadati** scaricato, **l'ID entità SAML**, **l'URL del servizio Single Sign-On SAML** e l'**URL di disconnessione**, al [team di supporto di Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="a2f13-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="a2f13-172">L’impostazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="a2f13-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a2f13-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a2f13-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2f13-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a2f13-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2f13-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2f13-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2f13-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2f13-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f13-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a2f13-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2f13-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2f13-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a2f13-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2f13-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a2f13-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2f13-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2f13-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a2f13-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2f13-188">a.</span><span class="sxs-lookup"><span data-stu-id="a2f13-188">a.</span></span> <span data-ttu-id="a2f13-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2f13-190">b.</span><span class="sxs-lookup"><span data-stu-id="a2f13-190">b.</span></span> <span data-ttu-id="a2f13-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2f13-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2f13-192">c.</span><span class="sxs-lookup"><span data-stu-id="a2f13-192">c.</span></span> <span data-ttu-id="a2f13-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a2f13-194">d.</span><span class="sxs-lookup"><span data-stu-id="a2f13-194">d.</span></span> <span data-ttu-id="a2f13-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="a2f13-196">Creazione di un utente test di Anaplan</span><span class="sxs-lookup"><span data-stu-id="a2f13-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="a2f13-197">In questa sezione viene creato un utente di nome Britta Simon in Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="a2f13-198">Rivolgersi al [team di supporto di Anaplan](mailto:support@anaplan.com) per aggiungere utenti alla piattaforma Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a2f13-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f13-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a2f13-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a2f13-202">**Per assegnare Britta Simon ad Anaplan, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a2f13-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="a2f13-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a2f13-205">Nell'elenco delle applicazioni selezionare **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-205">In the applications list, select **Anaplan**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="a2f13-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a2f13-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a2f13-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-209">Click **Add** button.</span></span> <span data-ttu-id="a2f13-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a2f13-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a2f13-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a2f13-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2f13-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2f13-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2f13-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a2f13-215">Testing single sign-on</span></span>

<span data-ttu-id="a2f13-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a2f13-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a2f13-217">Quando si fa clic sul riquadro Anaplan nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a2f13-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span></span>

<span data-ttu-id="a2f13-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2f13-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2f13-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a2f13-219">Additional resources</span></span>

* [<span data-ttu-id="a2f13-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2f13-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2f13-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2f13-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

