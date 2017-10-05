---
title: 'Esercitazione: Integrazione di Azure Active Directory con Overdrive | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Overdrive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 515dd397c46df7c8c82afab9b50051e34db69d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="afa58-103">Esercitazione: Integrazione di Azure Active Directory con Overdrive</span><span class="sxs-lookup"><span data-stu-id="afa58-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="afa58-104">Questa esercitazione descrive come integrare Overdrive con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afa58-104">In this tutorial, you learn how to integrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afa58-105">L'integrazione di Overdrive con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa58-105">Integrating Overdrive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="afa58-106">È possibile controllare in Azure AD chi può accedere a Overdrive</span><span class="sxs-lookup"><span data-stu-id="afa58-106">You can control in Azure AD who has access to Overdrive</span></span> 
- <span data-ttu-id="afa58-107">È possibile abilitare gli utenti per l'accesso automatico a Overdrive (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="afa58-107">You can enable your users to automatically get signed-on to Overdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="afa58-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="afa58-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="afa58-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="afa58-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa58-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="afa58-110">Prerequisites</span></span>

<span data-ttu-id="afa58-111">Per configurare l'integrazione di Azure AD con Overdrive, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa58-111">To configure Azure AD integration with Overdrive, you need the following items:</span></span>

- <span data-ttu-id="afa58-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="afa58-113">Sottoscrizione di Overdrive abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa58-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="afa58-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="afa58-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="afa58-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa58-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="afa58-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="afa58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="afa58-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="afa58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="afa58-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="afa58-118">Scenario description</span></span>
<span data-ttu-id="afa58-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="afa58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="afa58-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa58-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="afa58-121">Aggiunta di Overdrive dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="afa58-121">Adding Overdrive from the gallery</span></span>
2. <span data-ttu-id="afa58-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-the-gallery"></a><span data-ttu-id="afa58-123">Aggiunta di Overdrive dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="afa58-123">Adding Overdrive from the gallery</span></span>
<span data-ttu-id="afa58-124">Per configurare l'integrazione di Overdrive in Azure AD, è necessario aggiungere Overdrive dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="afa58-124">To configure the integration of Overdrive into Azure AD, you need to add Overdrive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="afa58-125">**Per aggiungere New Overdrive dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="afa58-125">**To add Overdrive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="afa58-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="afa58-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="afa58-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="afa58-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="afa58-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa58-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="afa58-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa58-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="afa58-133">Nella casella di ricerca digitare **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="afa58-133">In the search box, type **Overdrive**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="afa58-135">Nel pannello dei risultati selezionare **Overdrive** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa58-135">In the results panel, select **Overdrive**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="afa58-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="afa58-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Overdrive usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="afa58-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="afa58-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Overdrive corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa58-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Overdrive is to a user in Azure AD.</span></span> <span data-ttu-id="afa58-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Overdrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-140">In other words, a link relationship between an Azure AD user and the related user in Overdrive needs to be established.</span></span>

<span data-ttu-id="afa58-141">Per stabilire la relazione di collegamento, in Overdrive assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="afa58-141">In Overdrive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="afa58-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Overdrive, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa58-142">To configure and test Azure AD single sign-on with Overdrive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="afa58-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="afa58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="afa58-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afa58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afa58-145">**[Creazione di un utente di test di Overdrive](#creating-an-overdrive-test-user)**: per avere una controparte di Britta Simon in Overdrive collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa58-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - to have a counterpart of Britta Simon in Overdrive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="afa58-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa58-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afa58-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="afa58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="afa58-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="afa58-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Overdrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="afa58-150">**Per configurare l'accesso Single Sign-On di Azure AD con Overdrive, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="afa58-150">**To configure Azure AD single sign-on with Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="afa58-151">Nella pagina di integrazione dell'applicazione **Overdrive** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="afa58-151">In the Azure portal, on the **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="afa58-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="afa58-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="afa58-155">Nella sezione **URL e dominio Overdrive** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="afa58-155">On the **Overdrive Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="afa58-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="afa58-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afa58-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="afa58-158">The value is not real.</span></span> <span data-ttu-id="afa58-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="afa58-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="afa58-160">Per ottenere il valore contattare il [team di supporto di Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="afa58-160">Contact [Overdrive Client support team](https://help.overdrive.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="afa58-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="afa58-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="afa58-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="afa58-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="afa58-165">Per configurare l'accesso Single Sign-On sul lato **Overdrive**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="afa58-165">To configure single sign-on on **Overdrive** side, you need to send the downloaded **Metadata XML** to [Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="afa58-166">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="afa58-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="afa58-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="afa58-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="afa58-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="afa58-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="afa58-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afa58-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="afa58-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa58-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="afa58-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="afa58-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="afa58-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa58-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="afa58-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="afa58-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="afa58-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="afa58-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="afa58-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="afa58-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="afa58-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="afa58-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="afa58-182">a.</span><span class="sxs-lookup"><span data-stu-id="afa58-182">a.</span></span> <span data-ttu-id="afa58-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="afa58-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="afa58-184">b.</span><span class="sxs-lookup"><span data-stu-id="afa58-184">b.</span></span> <span data-ttu-id="afa58-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="afa58-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="afa58-186">c.</span><span class="sxs-lookup"><span data-stu-id="afa58-186">c.</span></span> <span data-ttu-id="afa58-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="afa58-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="afa58-188">d.</span><span class="sxs-lookup"><span data-stu-id="afa58-188">d.</span></span> <span data-ttu-id="afa58-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="afa58-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="afa58-190">Creazione di un utente di test di Overdrive</span><span class="sxs-lookup"><span data-stu-id="afa58-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="afa58-191">Non è richiesta alcuna operazione per configurare il provisioning degli utenti in OverDrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-191">There is no action item for you to configure user provisioning to OverDrive.</span></span>  

<span data-ttu-id="afa58-192">Quando un utente assegnato tenta di accedere a Overdrive, se necessario viene creato automaticamente un account di Overdrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-192">When an assigned user tries to log in to OverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="afa58-193">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di OverDrive o le API fornite da OverDrive per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="afa58-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span></span>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="afa58-194">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa58-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="afa58-195">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Overdrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Overdrive.</span></span>

![Assegna utente][200] 

<span data-ttu-id="afa58-197">**Per assegnare Britta Simon a Overdrive, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="afa58-197">**To assign Britta Simon to Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="afa58-198">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa58-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="afa58-200">Nell'elenco delle applicazioni selezionare **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="afa58-200">In the applications list, select **Overdrive**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="afa58-202">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="afa58-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="afa58-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="afa58-204">Click **Add** button.</span></span> <span data-ttu-id="afa58-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa58-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="afa58-207">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="afa58-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="afa58-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="afa58-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="afa58-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa58-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="afa58-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa58-210">Testing single sign-on</span></span>

<span data-ttu-id="afa58-211">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="afa58-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="afa58-212">Quando si fa clic sul riquadro Overdrive nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Overdrive.</span><span class="sxs-lookup"><span data-stu-id="afa58-212">When you click the Overdrive tile in the Access Panel, you should get automatically signed-on to your Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afa58-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="afa58-213">Additional resources</span></span>

* [<span data-ttu-id="afa58-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afa58-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afa58-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afa58-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

