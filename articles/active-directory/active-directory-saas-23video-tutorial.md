---
title: 'Esercitazione: Integrazione di Azure Active Directory con 23 Video | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e 23 Video.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="02c56-103">Esercitazione: Integrazione di Azure Active Directory con 23 Video</span><span class="sxs-lookup"><span data-stu-id="02c56-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="02c56-104">Questa esercitazione descrive come integrare 23 Video con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02c56-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02c56-105">L'integrazione di 23 Video con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="02c56-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02c56-106">È possibile controllare in Azure AD chi può accedere a 23 Video</span><span class="sxs-lookup"><span data-stu-id="02c56-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="02c56-107">È possibile abilitare gli utenti per l'accesso automatico a 23 Video (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02c56-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02c56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="02c56-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02c56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02c56-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02c56-110">Prerequisites</span></span>

<span data-ttu-id="02c56-111">Per configurare l'integrazione di Azure AD con 23 Video, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="02c56-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="02c56-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02c56-113">Sottoscrizione di 23 Video abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="02c56-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02c56-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="02c56-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02c56-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="02c56-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02c56-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="02c56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02c56-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02c56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02c56-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="02c56-118">Scenario description</span></span>
<span data-ttu-id="02c56-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="02c56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02c56-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="02c56-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02c56-121">Aggiunta di 23 Video dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="02c56-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="02c56-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="02c56-123">Aggiunta di 23 Video dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="02c56-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="02c56-124">Per configurare l'integrazione di 23 Video in Azure AD, è necessario aggiungere 23 Video dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="02c56-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02c56-125">**Per aggiungere 23 Video dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="02c56-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02c56-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="02c56-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02c56-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="02c56-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02c56-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="02c56-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="02c56-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="02c56-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="02c56-133">Nella casella di ricerca digitare **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="02c56-133">In the search box, type **23 Video**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="02c56-135">Nel pannello dei risultati selezionare **23 Video** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="02c56-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02c56-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02c56-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 23 Video con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02c56-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="02c56-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di 23 Video che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="02c56-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="02c56-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="02c56-141">Per stabilire la relazione di collegamento, in 23 Video assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="02c56-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="02c56-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con 23 Video, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="02c56-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02c56-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="02c56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02c56-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02c56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02c56-145">**[Creazione di un utente di test di 23 Video](#creating-a-23-video-test-user)**: per avere una controparte di Britta Simon in 23 Video collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c56-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02c56-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c56-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02c56-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="02c56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02c56-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02c56-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione 23 Video.</span><span class="sxs-lookup"><span data-stu-id="02c56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="02c56-150">**Per configurare l'accesso Single Sign-On di Azure AD con 23 Video, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="02c56-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="02c56-151">Nella pagina di integrazione dell'applicazione **23 Video** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="02c56-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="02c56-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="02c56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="02c56-155">Nella sezione **URL e dominio 23 Video** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="02c56-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="02c56-157">a.</span><span class="sxs-lookup"><span data-stu-id="02c56-157">a.</span></span> <span data-ttu-id="02c56-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.23video.com`.</span><span class="sxs-lookup"><span data-stu-id="02c56-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="02c56-159">b.</span><span class="sxs-lookup"><span data-stu-id="02c56-159">b.</span></span> <span data-ttu-id="02c56-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="02c56-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02c56-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="02c56-161">These values are not real.</span></span> <span data-ttu-id="02c56-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="02c56-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="02c56-163">Per ottenere tali valori, contattare il [team di supporto clienti di 23 Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="02c56-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="02c56-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="02c56-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="02c56-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="02c56-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02c56-168">Nella sezione **Configurazione di 23 Video** fare clic su **Configura 23 Video** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="02c56-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02c56-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="02c56-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="02c56-171">Per configurare l'accesso Single Sign-On sul lato **23 Video**, è necessario inviare il file di **Certificato (Base64)** scaricato, **l'URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di 23 Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="02c56-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="02c56-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="02c56-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="02c56-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="02c56-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="02c56-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02c56-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02c56-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="02c56-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02c56-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="02c56-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="02c56-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02c56-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="02c56-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02c56-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="02c56-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02c56-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="02c56-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02c56-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="02c56-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02c56-187">a.</span><span class="sxs-lookup"><span data-stu-id="02c56-187">a.</span></span> <span data-ttu-id="02c56-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02c56-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02c56-189">b.</span><span class="sxs-lookup"><span data-stu-id="02c56-189">b.</span></span> <span data-ttu-id="02c56-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02c56-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02c56-191">c.</span><span class="sxs-lookup"><span data-stu-id="02c56-191">c.</span></span> <span data-ttu-id="02c56-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="02c56-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="02c56-193">d.</span><span class="sxs-lookup"><span data-stu-id="02c56-193">d.</span></span> <span data-ttu-id="02c56-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="02c56-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="02c56-195">Creazione di un utente di test di 23 Video</span><span class="sxs-lookup"><span data-stu-id="02c56-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="02c56-196">Questa sezione descrive come creare un utente chiamato Britta Simon in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="02c56-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="02c56-197">**Per creare un utente denominato Britta Simon in 23 Video, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="02c56-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="02c56-198">Accedere al sito aziendale di 23 Video come amministratore.</span><span class="sxs-lookup"><span data-stu-id="02c56-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="02c56-199">Passare a **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="02c56-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="02c56-200">Nella sezione **Users** (Utenti) fare clic su **Configure** (Configura).</span><span class="sxs-lookup"><span data-stu-id="02c56-200">In **Users** section, click **Configure**.</span></span>
   
    ![Assegna utente][400]

4. <span data-ttu-id="02c56-202">Fare clic su **Aggiungi nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="02c56-202">Click **Add a new user**.</span></span> 
   
    ![Assegna utente][401]

5. <span data-ttu-id="02c56-204">Nella sezione **Invita qualcuno a questo sito** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="02c56-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Assegna utente][402]

    <span data-ttu-id="02c56-206">a.</span><span class="sxs-lookup"><span data-stu-id="02c56-206">a.</span></span> <span data-ttu-id="02c56-207">Nella casella di testo **E-mail addresses** digitare l'indirizzo di posta elettronica di Britta Simon in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02c56-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="02c56-208">b.</span><span class="sxs-lookup"><span data-stu-id="02c56-208">b.</span></span> <span data-ttu-id="02c56-209">Fare clic su **Aggiungi questo utente**.</span><span class="sxs-lookup"><span data-stu-id="02c56-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02c56-210">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c56-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="02c56-211">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a 23 Video.</span><span class="sxs-lookup"><span data-stu-id="02c56-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Assegna utente][200] 

<span data-ttu-id="02c56-213">**Per assegnare Britta Simon a 23 Video, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="02c56-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="02c56-214">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="02c56-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="02c56-216">Nell'elenco delle applicazioni selezionare **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="02c56-216">In the applications list, select **23 Video**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="02c56-218">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="02c56-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="02c56-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="02c56-220">Click **Add** button.</span></span> <span data-ttu-id="02c56-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="02c56-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="02c56-223">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="02c56-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02c56-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="02c56-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02c56-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="02c56-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02c56-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="02c56-226">Testing single sign-on</span></span>

<span data-ttu-id="02c56-227">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="02c56-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="02c56-228">Quando si fa clic sul riquadro 23 Video nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione 23 Video.</span><span class="sxs-lookup"><span data-stu-id="02c56-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="02c56-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="02c56-229">Additional resources</span></span>

* [<span data-ttu-id="02c56-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02c56-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02c56-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02c56-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
