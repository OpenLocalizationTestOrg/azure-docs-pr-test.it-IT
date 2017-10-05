---
title: 'Esercitazione: Integrazione di Azure Active Directory con People | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e People.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="0ecd8-103">Esercitazione: Integrazione di Azure Active Directory con People</span><span class="sxs-lookup"><span data-stu-id="0ecd8-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="0ecd8-104">Questa esercitazione descrive come integrare People con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ecd8-105">L'integrazione di People con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ecd8-106">È possibile controllare in Azure AD chi può accedere a People</span><span class="sxs-lookup"><span data-stu-id="0ecd8-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="0ecd8-107">È possibile abilitare gli utenti per l'accesso automatico a People (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ecd8-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0ecd8-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ecd8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0ecd8-110">Prerequisites</span></span>

<span data-ttu-id="0ecd8-111">Per configurare l'integrazione di Azure AD con People, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="0ecd8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ecd8-113">Sottoscrizione di People abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0ecd8-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ecd8-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ecd8-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ecd8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ecd8-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ecd8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0ecd8-118">Scenario description</span></span>
<span data-ttu-id="0ecd8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ecd8-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ecd8-121">Aggiunta di People dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0ecd8-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="0ecd8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="0ecd8-123">Aggiunta di People dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0ecd8-123">Adding People from the gallery</span></span>
<span data-ttu-id="0ecd8-124">Per configurare l'integrazione di People in Azure AD, è necessario aggiungere People dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ecd8-125">**Per aggiungere People dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0ecd8-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecd8-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ecd8-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0ecd8-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0ecd8-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0ecd8-133">Nella casella di ricerca digitare **People**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-133">In the search box, type **People**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="0ecd8-135">Nel pannello dei risultati selezionare **People** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ecd8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ecd8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con People in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0ecd8-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ecd8-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di People che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="0ecd8-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="0ecd8-141">Per stabilire la relazione di collegamento, in People assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0ecd8-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con People, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ecd8-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ecd8-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ecd8-145">**[Creazione di un utente test di People](#creating-a-people-test-user)**: per avere una controparte di Britta Simon in People collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ecd8-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ecd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ecd8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ecd8-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On all'applicazione People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="0ecd8-150">**Per configurare l'accesso Single Sign-On di Azure AD con People, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0ecd8-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecd8-151">Nella pagina di integrazione dell'applicazione **People** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0ecd8-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="0ecd8-155">Nella sezione **URL e dominio People** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="0ecd8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-157">a.</span></span> <span data-ttu-id="0ecd8-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.peoplehr.com/`.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="0ecd8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-159">b.</span></span> <span data-ttu-id="0ecd8-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="0ecd8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="0ecd8-161">c.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-161">c.</span></span> <span data-ttu-id="0ecd8-162">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="0ecd8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ecd8-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0ecd8-163">These values are not real.</span></span> <span data-ttu-id="0ecd8-164">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0ecd8-165">Per ottenere tali valori, contattare il [team di supporto clienti di People](mailto:customerservices@peoplehr.com).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="0ecd8-166">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="0ecd8-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0ecd8-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0ecd8-170">Per configurare l'accesso SSO sull'applicazione, è necessario accedere al tenant di People come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="0ecd8-171">Nella barra di spostamento sul lato sinistro fare clic su **Settings (Impostazioni)**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-171">In the menu on the left side, click **Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="0ecd8-173">Fare clic su **Azienda**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-173">Click **Company**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="0ecd8-175">In **Upload 'Single Sign On' SAML meta-data file** (Carica il file dei metadati SAML "Single Sign-On") fare clic su **Browse** (Sfoglia) per caricare il file di metadati scaricato.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="0ecd8-177">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0ecd8-178">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0ecd8-179">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ecd8-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ecd8-180">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ecd8-181">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0ecd8-183">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0ecd8-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecd8-184">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ecd8-186">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ecd8-188">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ecd8-190">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0ecd8-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ecd8-192">a.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-192">a.</span></span> <span data-ttu-id="0ecd8-193">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ecd8-194">b.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-194">b.</span></span> <span data-ttu-id="0ecd8-195">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ecd8-196">c.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-196">c.</span></span> <span data-ttu-id="0ecd8-197">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0ecd8-198">d.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-198">d.</span></span> <span data-ttu-id="0ecd8-199">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="0ecd8-200">Creazione di un utente test di People</span><span class="sxs-lookup"><span data-stu-id="0ecd8-200">Creating a People test user</span></span>

<span data-ttu-id="0ecd8-201">In questa sezione viene creato un utente chiamato Britta Simon in People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="0ecd8-202">Collaborare con il [team di supporto client di People](mailto:customerservices@peoplehr.com) per aggiungere gli utenti alla piattaforma People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="0ecd8-203">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0ecd8-204">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ecd8-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0ecd8-205">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0ecd8-207">**Per assegnare Britta Simon a People, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0ecd8-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecd8-208">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0ecd8-210">Nell'elenco delle applicazioni, selezionare **People**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-210">In the applications list, select **People**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="0ecd8-212">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0ecd8-214">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-214">Click **Add** button.</span></span> <span data-ttu-id="0ecd8-215">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0ecd8-217">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0ecd8-218">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ecd8-219">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ecd8-220">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0ecd8-220">Testing single sign-on</span></span>

<span data-ttu-id="0ecd8-221">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="0ecd8-222">Quando si fa clic sul riquadro People nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione People.</span><span class="sxs-lookup"><span data-stu-id="0ecd8-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ecd8-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0ecd8-223">Additional resources</span></span>

* [<span data-ttu-id="0ecd8-224">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ecd8-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ecd8-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ecd8-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

