---
title: 'Esercitazione: Integrazione di Azure Active Directory con Abintegro | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Abintegro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="434e1-103">Esercitazione: Integrazione di Azure Active Directory con Abintegro</span><span class="sxs-lookup"><span data-stu-id="434e1-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="434e1-104">Questa esercitazione descrive come integrare Abintegro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="434e1-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="434e1-105">L'integrazione di Abintegro con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="434e1-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="434e1-106">È possibile controllare in Azure AD chi può accedere ad Abintegro</span><span class="sxs-lookup"><span data-stu-id="434e1-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="434e1-107">È possibile abilitare gli utenti per l'accesso automatico ad Abintegro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="434e1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="434e1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="434e1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="434e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="434e1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="434e1-110">Prerequisites</span></span>

<span data-ttu-id="434e1-111">Per configurare l'integrazione di Azure AD con Abintegro, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="434e1-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="434e1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="434e1-113">Sottoscrizione di Abintegro abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="434e1-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="434e1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="434e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="434e1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="434e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="434e1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="434e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="434e1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="434e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="434e1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="434e1-118">Scenario description</span></span>
<span data-ttu-id="434e1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="434e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="434e1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="434e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="434e1-121">Aggiunta di Abintegro dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="434e1-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="434e1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="434e1-123">Aggiunta di Abintegro dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="434e1-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="434e1-124">Per configurare l'integrazione di Abintegro in Azure AD, è necessario aggiungere Abintegro dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="434e1-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="434e1-125">**Per aggiungere Abintegro dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="434e1-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="434e1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="434e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="434e1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="434e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="434e1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="434e1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="434e1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="434e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="434e1-133">Nella casella di ricerca digitare **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="434e1-133">In the search box, type **Abintegro**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="434e1-135">Nel pannello dei risultati selezionare **Abintegro** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="434e1-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="434e1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="434e1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Abintegro con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="434e1-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="434e1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Abintegro che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434e1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="434e1-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Abintegro.</span><span class="sxs-lookup"><span data-stu-id="434e1-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="434e1-141">Per stabilire la relazione di collegamento, in Abintegro assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="434e1-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="434e1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Abintegro, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="434e1-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="434e1-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="434e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="434e1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="434e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="434e1-145">**[Creazione di un utente di test di Abintegro](#creating-an-abintegro-test-user)**: per avere una controparte di Britta Simon in Abintegro collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434e1-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="434e1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434e1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="434e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="434e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="434e1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="434e1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Abintegro.</span><span class="sxs-lookup"><span data-stu-id="434e1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="434e1-150">**Per configurare l'accesso Single Sign-On di Azure AD con Abintegro, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="434e1-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="434e1-151">Nella pagina di integrazione dell'applicazione **Abintegro** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="434e1-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="434e1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="434e1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="434e1-155">Nella sezione **URL e dominio Abintegro** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="434e1-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="434e1-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="434e1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="434e1-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="434e1-158">This value is not real.</span></span> <span data-ttu-id="434e1-159">aggiornarlo con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="434e1-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="434e1-160">Per ottenere tale valore, contattare il [team di supporto clienti di Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="434e1-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="434e1-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="434e1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="434e1-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="434e1-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="434e1-165">Per configurare l'accesso Single Sign-On sul lato **Abintegro**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="434e1-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="434e1-166">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="434e1-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="434e1-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="434e1-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="434e1-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="434e1-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="434e1-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="434e1-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="434e1-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="434e1-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="434e1-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="434e1-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="434e1-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="434e1-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="434e1-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="434e1-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="434e1-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="434e1-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="434e1-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="434e1-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="434e1-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="434e1-182">a.</span><span class="sxs-lookup"><span data-stu-id="434e1-182">a.</span></span> <span data-ttu-id="434e1-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="434e1-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="434e1-184">b.</span><span class="sxs-lookup"><span data-stu-id="434e1-184">b.</span></span> <span data-ttu-id="434e1-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="434e1-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="434e1-186">c.</span><span class="sxs-lookup"><span data-stu-id="434e1-186">c.</span></span> <span data-ttu-id="434e1-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="434e1-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="434e1-188">d.</span><span class="sxs-lookup"><span data-stu-id="434e1-188">d.</span></span> <span data-ttu-id="434e1-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="434e1-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="434e1-190">Creazione di un utente di test di Abintegro</span><span class="sxs-lookup"><span data-stu-id="434e1-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="434e1-191">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in Abintegro.</span><span class="sxs-lookup"><span data-stu-id="434e1-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="434e1-192">Quando un utente assegnato tenta di accedere ad Abintegro usando il pannello di accesso, Abintegro verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="434e1-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="434e1-193">Se l'account utente non è presente, Abintegro lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="434e1-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="434e1-194">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="434e1-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="434e1-195">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Abintegro.</span><span class="sxs-lookup"><span data-stu-id="434e1-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Assegna utente][200] 

<span data-ttu-id="434e1-197">**Per assegnare Britta Simon ad Abintegro, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="434e1-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="434e1-198">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="434e1-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="434e1-200">Nell'elenco delle applicazioni selezionare **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="434e1-200">In the applications list, select **Abintegro**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="434e1-202">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="434e1-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="434e1-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="434e1-204">Click **Add** button.</span></span> <span data-ttu-id="434e1-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="434e1-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="434e1-207">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="434e1-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="434e1-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="434e1-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="434e1-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="434e1-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="434e1-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="434e1-210">Testing single sign-on</span></span>

<span data-ttu-id="434e1-211">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="434e1-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="434e1-212">Quando si fa clic sul riquadro Abintegro nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Abintegro.</span><span class="sxs-lookup"><span data-stu-id="434e1-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="434e1-213">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="434e1-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="434e1-214">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="434e1-214">Additional resources</span></span>

* [<span data-ttu-id="434e1-215">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="434e1-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="434e1-216">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="434e1-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

