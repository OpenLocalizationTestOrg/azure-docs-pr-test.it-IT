---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mindflash | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Mindflash.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="0fa33-103">Esercitazione: Integrazione di Azure Active Directory con Mindflash</span><span class="sxs-lookup"><span data-stu-id="0fa33-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="0fa33-104">Questa esercitazione descrive come integrare Mindflash con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fa33-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fa33-105">L'integrazione di Mindflash con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa33-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0fa33-106">È possibile controllare in Azure AD chi può accedere a Mindflash</span><span class="sxs-lookup"><span data-stu-id="0fa33-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="0fa33-107">È possibile abilitare gli utenti per l'accesso automatico a Mindflash (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="0fa33-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fa33-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa33-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0fa33-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fa33-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa33-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0fa33-110">Prerequisites</span></span>

<span data-ttu-id="0fa33-111">Per configurare l'integrazione di Azure AD con Mindflash, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa33-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="0fa33-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fa33-113">Sottoscrizione di Mindflash abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0fa33-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fa33-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0fa33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fa33-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa33-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fa33-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0fa33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fa33-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fa33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fa33-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0fa33-118">Scenario description</span></span>
<span data-ttu-id="0fa33-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0fa33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fa33-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa33-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fa33-121">Aggiunta di Mindflash dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0fa33-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="0fa33-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="0fa33-123">Aggiunta di Mindflash dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0fa33-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="0fa33-124">Per configurare l'integrazione di Mindflash in Azure AD, è necessario aggiungere Mindflash dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0fa33-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0fa33-125">**Per aggiungere Mindflash dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa33-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa33-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0fa33-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fa33-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0fa33-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0fa33-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0fa33-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0fa33-133">Nella casella di ricerca digitare **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-133">In the search box, type **Mindflash**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="0fa33-135">Nel pannello dei risultati selezionare **Mindflash** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0fa33-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fa33-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa33-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fa33-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mindflash usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0fa33-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0fa33-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Mindflash corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa33-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="0fa33-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Mindflash.</span><span class="sxs-lookup"><span data-stu-id="0fa33-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="0fa33-141">Per stabilire la relazione di collegamento, in Mindflash assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="0fa33-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0fa33-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Mindflash, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa33-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0fa33-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0fa33-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0fa33-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fa33-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fa33-145">**[Creazione di un utente di test di Mindflash](#creating-a-mindflash-test-user)**: per avere una controparte di Britta Simon in Mindflash collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa33-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fa33-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa33-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fa33-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0fa33-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fa33-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa33-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fa33-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Mindflash.</span><span class="sxs-lookup"><span data-stu-id="0fa33-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="0fa33-150">**Per configurare l'accesso Single Sign-On di Azure AD con Mindflash, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa33-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa33-151">Nella pagina di integrazione dell'applicazione **Mindflash** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0fa33-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0fa33-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="0fa33-155">Nella sezione **URL e dominio Mindflash** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa33-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="0fa33-157">a.</span><span class="sxs-lookup"><span data-stu-id="0fa33-157">a.</span></span> <span data-ttu-id="0fa33-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.mindflash.com`.</span><span class="sxs-lookup"><span data-stu-id="0fa33-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="0fa33-159">b.</span><span class="sxs-lookup"><span data-stu-id="0fa33-159">b.</span></span> <span data-ttu-id="0fa33-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="0fa33-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0fa33-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0fa33-161">These values are not real.</span></span> <span data-ttu-id="0fa33-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0fa33-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0fa33-163">Per ottenere questi valori, contattare il [team di supporto di Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0fa33-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="0fa33-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="0fa33-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="0fa33-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0fa33-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0fa33-168">Per configurare l'accesso Single Sign-On sul lato **Mindflash**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0fa33-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="0fa33-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0fa33-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0fa33-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0fa33-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0fa33-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fa33-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fa33-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa33-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fa33-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa33-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0fa33-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0fa33-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa33-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0fa33-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fa33-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0fa33-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fa33-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fa33-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa33-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fa33-184">a.</span><span class="sxs-lookup"><span data-stu-id="0fa33-184">a.</span></span> <span data-ttu-id="0fa33-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fa33-186">b.</span><span class="sxs-lookup"><span data-stu-id="0fa33-186">b.</span></span> <span data-ttu-id="0fa33-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0fa33-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fa33-188">c.</span><span class="sxs-lookup"><span data-stu-id="0fa33-188">c.</span></span> <span data-ttu-id="0fa33-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0fa33-190">d.</span><span class="sxs-lookup"><span data-stu-id="0fa33-190">d.</span></span> <span data-ttu-id="0fa33-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="0fa33-192">Creazione di un utente di test di Mindflash</span><span class="sxs-lookup"><span data-stu-id="0fa33-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="0fa33-193">Per consentire agli utenti di Azure AD di accedere a Mindflash, è necessario eseguirne il provisioning in Mindflash.</span><span class="sxs-lookup"><span data-stu-id="0fa33-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="0fa33-194">Nel caso di Mindflash, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="0fa33-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="0fa33-195">Per eseguire il provisioning di un account utente, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0fa33-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="0fa33-196">Accedere al sito aziendale di **Mindflash** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0fa33-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="0fa33-197">Passare a **Gestisci utenti**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="0fa33-198">![Gestione utenti](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="0fa33-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="0fa33-199">Fare clic su **Aggiungi utenti**, quindi fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="0fa33-200">Nella sezione **Add New Users** (Aggiungi nuovi utenti) eseguire i passaggi seguenti per un account Azure AD valido di cui si vuole eseguire il provisioning:</span><span class="sxs-lookup"><span data-stu-id="0fa33-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="0fa33-201">![Aggiungi nuovi utenti](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Aggiungi nuovi utenti")</span><span class="sxs-lookup"><span data-stu-id="0fa33-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="0fa33-202">a.</span><span class="sxs-lookup"><span data-stu-id="0fa33-202">a.</span></span> <span data-ttu-id="0fa33-203">Nella casella di testo **First Name** (Nome) digitare**** **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="0fa33-204">b.</span><span class="sxs-lookup"><span data-stu-id="0fa33-204">b.</span></span> <span data-ttu-id="0fa33-205">Nella casella di testo **Last name** (Cognome) digitare**** **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="0fa33-206">c.</span><span class="sxs-lookup"><span data-stu-id="0fa33-206">c.</span></span> <span data-ttu-id="0fa33-207">Nella casella di testo **Email** (Indirizzo e-mail) digitare**** **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="0fa33-208">b.</span><span class="sxs-lookup"><span data-stu-id="0fa33-208">b.</span></span> <span data-ttu-id="0fa33-209">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="0fa33-210">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di Mindflash o le API fornite da Mindflash per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="0fa33-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0fa33-211">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa33-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0fa33-212">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Mindflash.</span><span class="sxs-lookup"><span data-stu-id="0fa33-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0fa33-214">**Per assegnare Britta Simon a Mindflash, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa33-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa33-215">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0fa33-217">Nell'elenco delle applicazioni selezionare **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-217">In the applications list, select **Mindflash**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="0fa33-219">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0fa33-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0fa33-221">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-221">Click **Add** button.</span></span> <span data-ttu-id="0fa33-222">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0fa33-224">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0fa33-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0fa33-225">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fa33-226">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0fa33-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fa33-227">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0fa33-227">Testing single sign-on</span></span>

<span data-ttu-id="0fa33-228">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0fa33-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0fa33-229">Quando si fa clic sul riquadro Mindflash nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Mindflash.</span><span class="sxs-lookup"><span data-stu-id="0fa33-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="0fa33-230">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0fa33-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fa33-231">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0fa33-231">Additional resources</span></span>

* [<span data-ttu-id="0fa33-232">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fa33-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fa33-233">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fa33-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

