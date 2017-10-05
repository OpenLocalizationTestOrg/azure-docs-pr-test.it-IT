---
title: 'Esercitazione: Integrazione di Azure Active Directory con Asset Bank | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Asset Bank.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="32a6b-103">Esercitazione: Integrazione di Azure Active Directory con Asset Bank</span><span class="sxs-lookup"><span data-stu-id="32a6b-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="32a6b-104">Questa esercitazione descrive come integrare Asset Bank con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32a6b-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a6b-105">L'integrazione di Asset Bank con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32a6b-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32a6b-106">È possibile controllare in Azure AD chi può accedere ad Asset Bank</span><span class="sxs-lookup"><span data-stu-id="32a6b-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="32a6b-107">È possibile abilitare gli utenti per l'accesso automatico ad Asset Bank (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a6b-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32a6b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32a6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32a6b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32a6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a6b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32a6b-110">Prerequisites</span></span>

<span data-ttu-id="32a6b-111">Per configurare l'integrazione di Azure AD con Asset Bank, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32a6b-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="32a6b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a6b-113">Sottoscrizione di Asset Bank abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32a6b-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32a6b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32a6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32a6b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="32a6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a6b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="32a6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a6b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32a6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32a6b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="32a6b-118">Scenario description</span></span>
<span data-ttu-id="32a6b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="32a6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a6b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="32a6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a6b-121">Aggiunta di Asset Bank dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32a6b-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="32a6b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="32a6b-123">Aggiunta di Asset Bank dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32a6b-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="32a6b-124">Per configurare l'integrazione di Asset Bank in Azure AD, è necessario aggiungere Asset Bank dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="32a6b-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32a6b-125">**Per aggiungere Asset Bank dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32a6b-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32a6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32a6b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32a6b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="32a6b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="32a6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="32a6b-133">Nella casella di ricerca digitare **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-133">In the search box, type **Asset Bank**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="32a6b-135">Nel pannello dei risultati selezionare **Asset Bank** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32a6b-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32a6b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32a6b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Asset Bank usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32a6b-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32a6b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Asset Bank che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="32a6b-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="32a6b-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="32a6b-141">Per stabilire la relazione di collegamento, in Asset Bank assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="32a6b-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32a6b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Asset Bank, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="32a6b-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32a6b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="32a6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32a6b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a6b-145">**[Creazione di un utente test di Asset Bank](#creating-an-asset-bank-test-user)** : per avere una controparte di Britta Simon in Asset Bank collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a6b-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a6b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="32a6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32a6b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32a6b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="32a6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="32a6b-150">**Per configurare Single Sign-On di Azure AD con Asset Bank, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32a6b-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6b-151">Nella pagina di integrazione dell'applicazione **Asset Bank** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="32a6b-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="32a6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="32a6b-155">Nella sezione **URL e dominio Asset Bank** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32a6b-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="32a6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="32a6b-157">a.</span></span> <span data-ttu-id="32a6b-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.assetbank-server.com`.</span><span class="sxs-lookup"><span data-stu-id="32a6b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="32a6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="32a6b-159">b.</span></span> <span data-ttu-id="32a6b-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="32a6b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a6b-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="32a6b-161">These values are not real.</span></span> <span data-ttu-id="32a6b-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="32a6b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32a6b-163">Per ottenere questi valori, contattare il [team di supporto clienti di Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="32a6b-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="32a6b-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="32a6b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="32a6b-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="32a6b-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32a6b-168">Per configurare l'accesso Single Sign-On sul lato **Asset Bank**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="32a6b-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="32a6b-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="32a6b-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32a6b-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="32a6b-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32a6b-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32a6b-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32a6b-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a6b-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="32a6b-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32a6b-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="32a6b-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32a6b-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6b-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32a6b-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32a6b-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="32a6b-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32a6b-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32a6b-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32a6b-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32a6b-184">a.</span><span class="sxs-lookup"><span data-stu-id="32a6b-184">a.</span></span> <span data-ttu-id="32a6b-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a6b-186">b.</span><span class="sxs-lookup"><span data-stu-id="32a6b-186">b.</span></span> <span data-ttu-id="32a6b-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32a6b-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32a6b-188">c.</span><span class="sxs-lookup"><span data-stu-id="32a6b-188">c.</span></span> <span data-ttu-id="32a6b-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32a6b-190">d.</span><span class="sxs-lookup"><span data-stu-id="32a6b-190">d.</span></span> <span data-ttu-id="32a6b-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="32a6b-192">Creazione di un utente test di Asset Bank</span><span class="sxs-lookup"><span data-stu-id="32a6b-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="32a6b-193">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="32a6b-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="32a6b-194">Asset Bank supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="32a6b-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="32a6b-195">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="32a6b-195">There is no action item for you in this section.</span></span> <span data-ttu-id="32a6b-196">Durante un tentativo di accesso ad Asset Bank viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="32a6b-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="32a6b-197">Per creare un utente manualmente, è necessario contattare il team di supporto di [Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="32a6b-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32a6b-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a6b-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32a6b-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="32a6b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Assegna utente][200] 

<span data-ttu-id="32a6b-201">**Per assegnare Britta Simon ad Asset Bank, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32a6b-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6b-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="32a6b-204">Nell'elenco di applicazioni selezionare **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-204">In the applications list, select **Asset Bank**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="32a6b-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="32a6b-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="32a6b-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-208">Click **Add** button.</span></span> <span data-ttu-id="32a6b-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="32a6b-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="32a6b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32a6b-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a6b-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32a6b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32a6b-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32a6b-214">Testing single sign-on</span></span>

<span data-ttu-id="32a6b-215">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="32a6b-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32a6b-216">Quando si fa clic sul riquadro Asset Bank nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="32a6b-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32a6b-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="32a6b-217">Additional resources</span></span>

* [<span data-ttu-id="32a6b-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32a6b-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a6b-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32a6b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

