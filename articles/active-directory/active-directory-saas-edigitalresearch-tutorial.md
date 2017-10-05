---
title: 'Esercitazione: Integrazione di Azure Active Directory con eDigitalResearch | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory ed eDigitalResearch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="0b34e-103">Esercitazione: Integrazione di Azure Active Directory con eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="0b34e-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="0b34e-104">Questa esercitazione descrive come integrare eDigitalResearch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b34e-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b34e-105">L'integrazione di eDigitalResearch con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b34e-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b34e-106">È possibile controllare in Azure AD chi ha accesso a eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="0b34e-107">È possibile abilitare gli utenti per l'accesso automatico a eDigitalResearch (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b34e-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0b34e-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b34e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0b34e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b34e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b34e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0b34e-110">Prerequisites</span></span>

<span data-ttu-id="0b34e-111">Per configurare l'integrazione di Azure AD con eDigitalResearch, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b34e-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="0b34e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b34e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b34e-113">Sottoscrizione di eDigitalResearch abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0b34e-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b34e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0b34e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b34e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b34e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b34e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0b34e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b34e-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b34e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b34e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0b34e-118">Scenario description</span></span>
<span data-ttu-id="0b34e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0b34e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b34e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b34e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b34e-121">Aggiunta di eDigitalResearch dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0b34e-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="0b34e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b34e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="0b34e-123">Aggiunta di eDigitalResearch dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0b34e-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="0b34e-124">Per configurare l'integrazione di eDigitalResearch in Azure AD, è necessario aggiungere eDigitalResearch dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0b34e-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b34e-125">**Per aggiungere eDigitalResearch dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0b34e-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b34e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0b34e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="0b34e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b34e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="0b34e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0b34e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="0b34e-133">Nella casella di ricerca digitare **eDigitalResearch**, selezionare **eDigitalResearch** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0b34e-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch nell'elenco risultati](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0b34e-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b34e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0b34e-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con eDigitalResearch usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0b34e-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b34e-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di eDigitalResearch che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b34e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="0b34e-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="0b34e-139">Per stabilire la relazione di collegamento, in eDigitalResearch assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="0b34e-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b34e-140">Per configurare e testare l'accesso Single Sign-On di Microsoft Azure AD con eDigitalResearch, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b34e-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b34e-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0b34e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b34e-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b34e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b34e-143">**[Creare un utente test di eDigitalResearch](#create-a-edigitalresearch-test-user)**: per avere una controparte di Britta Simon in eDigitalResearch collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b34e-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b34e-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b34e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b34e-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0b34e-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0b34e-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b34e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0b34e-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="0b34e-148">**Per configurare Single Sign-On di Microsoft Azure AD con eDigitalResearch, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0b34e-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="0b34e-149">Nella pagina di integrazione dell'applicazione **eDigitalResearch** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="0b34e-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0b34e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="0b34e-153">Nella sezione **URL e dominio eDigitalResearch** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0b34e-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sul Single Sign-On di URL e dominio di eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="0b34e-155">a.</span><span class="sxs-lookup"><span data-stu-id="0b34e-155">a.</span></span> <span data-ttu-id="0b34e-156">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="0b34e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="0b34e-157">b.</span><span class="sxs-lookup"><span data-stu-id="0b34e-157">b.</span></span> <span data-ttu-id="0b34e-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="0b34e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b34e-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0b34e-159">These values are not real.</span></span> <span data-ttu-id="0b34e-160">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="0b34e-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0b34e-161">Per ottenere questi valori, contattare il [team di supporto di eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="0b34e-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="0b34e-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato Base(64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="0b34e-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="0b34e-163">!</span><span class="sxs-lookup"><span data-stu-id="0b34e-163">!</span></span>![Collegamento di download del certificato](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="0b34e-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0b34e-165">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b34e-167">Nella sezione **Configurazione di eDigitalResearch** fare clic su **Configura eDigitalResearch** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b34e-168">Copiare l'**URL di disconnessione e l'ID di entità SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurazione di eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="0b34e-170">Per configurare l'accesso Single Sign-On sul lato **eDigitalResearch**, è necessario inviare il **file di Certificato (Base64)** scaricato, l'**ID entità SAML** e l'**URL di disconnessione** al [team di supporto di eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="0b34e-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="0b34e-171">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="0b34e-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0b34e-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0b34e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b34e-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0b34e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b34e-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b34e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0b34e-175">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b34e-175">Create an Azure AD test user</span></span>

<span data-ttu-id="0b34e-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b34e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="0b34e-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0b34e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b34e-179">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="0b34e-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0b34e-181">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0b34e-183">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0b34e-185">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0b34e-185">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0b34e-187">a.</span><span class="sxs-lookup"><span data-stu-id="0b34e-187">a.</span></span> <span data-ttu-id="0b34e-188">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b34e-189">b.</span><span class="sxs-lookup"><span data-stu-id="0b34e-189">b.</span></span> <span data-ttu-id="0b34e-190">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b34e-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0b34e-191">c.</span><span class="sxs-lookup"><span data-stu-id="0b34e-191">c.</span></span> <span data-ttu-id="0b34e-192">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0b34e-193">d.</span><span class="sxs-lookup"><span data-stu-id="0b34e-193">d.</span></span> <span data-ttu-id="0b34e-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="0b34e-195">Creare un utente test di eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="0b34e-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="0b34e-196">Questa sezione descrive come creare un utente chiamato Britta Simon in eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="0b34e-197">Per creare gli utenti, collaborare con il [team di supporto eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="0b34e-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="0b34e-198">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="0b34e-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0b34e-199">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b34e-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="0b34e-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="0b34e-202">**Per assegnare Britta Simon a eDigitalResearch, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0b34e-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="0b34e-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0b34e-205">Nell'elenco delle applicazioni, selezionare **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![Collegamento eDigitalResearch nell'elenco Applicazioni](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="0b34e-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0b34e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="0b34e-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-209">Click **Add** button.</span></span> <span data-ttu-id="0b34e-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="0b34e-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0b34e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b34e-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b34e-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0b34e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0b34e-215">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0b34e-215">Test single sign-on</span></span>

<span data-ttu-id="0b34e-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0b34e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b34e-217">Quando si fa clic sul riquadro eDigitalResearch nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0b34e-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="0b34e-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0b34e-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0b34e-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0b34e-219">Additional resources</span></span>

* [<span data-ttu-id="0b34e-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b34e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b34e-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b34e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

