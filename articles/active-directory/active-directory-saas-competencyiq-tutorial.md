---
title: 'Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e CompetencyIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ad3cec3de9034ddab2161952620d31540ae51978
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="67784-103">Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="67784-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="67784-104">Questa esercitazione descrive come integrare CompetencyIQ con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67784-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67784-105">L'integrazione di CompetencyIQ con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67784-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67784-106">È possibile controllare in Azure AD chi può accedere a CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="67784-106">You can control in Azure AD who has access to CompetencyIQ</span></span>
- <span data-ttu-id="67784-107">È possibile abilitare gli utenti per l'accesso automatico a CompetencyIQ (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="67784-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67784-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67784-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67784-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67784-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67784-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67784-110">Prerequisites</span></span>

<span data-ttu-id="67784-111">Per configurare l'integrazione di Azure AD con CompetencyIQ, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67784-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span></span>

- <span data-ttu-id="67784-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67784-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67784-113">Sottoscrizione di CompetencyIQ abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67784-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67784-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="67784-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67784-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="67784-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67784-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="67784-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67784-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67784-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67784-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="67784-118">Scenario description</span></span>
<span data-ttu-id="67784-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="67784-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67784-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="67784-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67784-121">Aggiunta di CompetencyIQ dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="67784-121">Adding CompetencyIQ from the gallery</span></span>
2. <span data-ttu-id="67784-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67784-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-the-gallery"></a><span data-ttu-id="67784-123">Aggiunta di CompetencyIQ dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="67784-123">Adding CompetencyIQ from the gallery</span></span>
<span data-ttu-id="67784-124">Per configurare l'integrazione di CompetencyIQ in Azure AD, è necessario aggiungere CompetencyIQ dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="67784-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67784-125">**Per aggiungere CompetencyIQ dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67784-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67784-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="67784-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67784-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="67784-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67784-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67784-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="67784-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="67784-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="67784-133">Nella casella di ricerca digitare **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="67784-133">In the search box, type **CompetencyIQ**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="67784-135">Nel pannello dei risultati selezionare **CompetencyIQ** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67784-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67784-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67784-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67784-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CompetencyIQ usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="67784-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67784-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di CompetencyIQ corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67784-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span></span> <span data-ttu-id="67784-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="67784-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span></span>

<span data-ttu-id="67784-141">Per stabilire la relazione di collegamento, in CompetencyIQ assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="67784-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="67784-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con CompetencyIQ, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="67784-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67784-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67784-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67784-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67784-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67784-145">**[Creazione di un utente di test di CompetencyIQ](#creating-a-competencyiq-test-user)**: per avere una controparte di Britta Simon in CompetencyIQ collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67784-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67784-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67784-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67784-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="67784-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67784-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67784-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67784-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel nuovo portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="67784-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="67784-150">**Per configurare l'accesso Single Sign-On di Azure AD con CompetencyIQ, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67784-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="67784-151">Nella pagina di integrazione dell'applicazione **CompetencyIQ** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="67784-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="67784-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="67784-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="67784-155">Nella sezione **URL e dominio CompetencyIQ** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67784-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="67784-157">a.</span><span class="sxs-lookup"><span data-stu-id="67784-157">a.</span></span> <span data-ttu-id="67784-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<customer>.competencyiq.com/`.</span><span class="sxs-lookup"><span data-stu-id="67784-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="67784-159">b.</span><span class="sxs-lookup"><span data-stu-id="67784-159">b.</span></span> <span data-ttu-id="67784-160">Nella casella di testo **Identificatore** digitare l'URL: `https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="67784-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67784-161">Poiché non è reale, è necessario aggiornare questo valore con l'URL di disconnessione effettivo.</span><span class="sxs-lookup"><span data-stu-id="67784-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="67784-162">Per ottenere il valore, contattare il [team di supporto clienti di CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="67784-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span></span> 
 
4. <span data-ttu-id="67784-163">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="67784-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="67784-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="67784-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67784-167">Nella sezione **Configurazione di CompetencyIQ** fare clic su **Configura CompetencyIQ** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="67784-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="67784-168">Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="67784-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="67784-170">Per configurare l'accesso Single Sign-On sul lato **CompetencyIQ**, è necessario inviare il file **XML metadati** scaricato, l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** al [team di supporto di CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="67784-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="67784-171">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="67784-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="67784-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="67784-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67784-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="67784-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67784-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67784-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67784-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67784-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="67784-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67784-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="67784-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67784-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67784-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="67784-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67784-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="67784-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67784-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="67784-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67784-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67784-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67784-187">a.</span><span class="sxs-lookup"><span data-stu-id="67784-187">a.</span></span> <span data-ttu-id="67784-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67784-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67784-189">b.</span><span class="sxs-lookup"><span data-stu-id="67784-189">b.</span></span> <span data-ttu-id="67784-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67784-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67784-191">c.</span><span class="sxs-lookup"><span data-stu-id="67784-191">c.</span></span> <span data-ttu-id="67784-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="67784-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67784-193">d.</span><span class="sxs-lookup"><span data-stu-id="67784-193">d.</span></span> <span data-ttu-id="67784-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="67784-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="67784-195">Creazione di un utente di test di CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="67784-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="67784-196">Per consentire agli utenti di Azure AD di accedere a CompetencyIQ, è necessario effettuarne il provisioning in CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="67784-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="67784-197">Contattare il [team di supporto di CompetencyIQ](https://www.competencyiq.com/) per creare gli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67784-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="67784-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67784-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="67784-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="67784-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span></span>

![Assegna utente][200] 

<span data-ttu-id="67784-201">**Per assegnare Britta Simon a CompetencyIQ, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="67784-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="67784-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67784-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="67784-204">Nell'elenco delle applicazioni selezionare **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="67784-204">In the applications list, select **CompetencyIQ**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="67784-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="67784-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="67784-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67784-208">Click **Add** button.</span></span> <span data-ttu-id="67784-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67784-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="67784-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="67784-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67784-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67784-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67784-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67784-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67784-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67784-214">Testing single sign-on</span></span>

<span data-ttu-id="67784-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="67784-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="67784-216">Quando si fa clic sul riquadro CompetencyIQ nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="67784-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span></span>
<span data-ttu-id="67784-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67784-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="67784-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="67784-218">Additional resources</span></span>

* [<span data-ttu-id="67784-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67784-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67784-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67784-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

