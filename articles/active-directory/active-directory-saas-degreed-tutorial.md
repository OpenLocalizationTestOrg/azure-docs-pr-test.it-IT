---
title: 'Esercitazione: Integrazione di Azure Active Directory con Degreed | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Degreed.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eda2d1c-b5e2-4c53-ad46-bbeb91cd119a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: ea96edb25e2d7199981ff126bf4b2a3d93c6840a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a><span data-ttu-id="7e034-103">Esercitazione: Integrazione di Azure Active Directory con Degreed</span><span class="sxs-lookup"><span data-stu-id="7e034-103">Tutorial: Azure Active Directory integration with Degreed</span></span>

<span data-ttu-id="7e034-104">Questa esercitazione descrive come integrare Degreed con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e034-104">In this tutorial, you learn how to integrate Degreed with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e034-105">L'integrazione di Degreed con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e034-105">Integrating Degreed with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7e034-106">È possibile controllare in Azure AD chi può accedere a Degreed</span><span class="sxs-lookup"><span data-stu-id="7e034-106">You can control in Azure AD who has access to Degreed</span></span>
- <span data-ttu-id="7e034-107">È possibile abilitare gli utenti per l'accesso automatico a Degreed (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-107">You can enable your users to automatically get signed-on to Degreed (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e034-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e034-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7e034-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e034-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e034-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e034-110">Prerequisites</span></span>

<span data-ttu-id="7e034-111">Per configurare l'integrazione di Azure AD con Degreed, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e034-111">To configure Azure AD integration with Degreed, you need the following items:</span></span>

- <span data-ttu-id="7e034-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e034-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e034-113">Sottoscrizione di Degreed abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7e034-113">A Degreed single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e034-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7e034-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e034-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e034-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e034-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7e034-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e034-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e034-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e034-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7e034-118">Scenario description</span></span>
<span data-ttu-id="7e034-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7e034-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e034-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e034-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e034-121">Aggiunta di Degreed dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7e034-121">Adding Degreed from the gallery</span></span>
2. <span data-ttu-id="7e034-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-degreed-from-the-gallery"></a><span data-ttu-id="7e034-123">Aggiunta di Degreed dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7e034-123">Adding Degreed from the gallery</span></span>
<span data-ttu-id="7e034-124">Per configurare l'integrazione di Degreed in Azure AD, è necessario aggiungere Degreed dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7e034-124">To configure the integration of Degreed into Azure AD, you need to add Degreed from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e034-125">**Per aggiungere Degreed dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e034-125">**To add Degreed from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e034-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e034-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e034-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7e034-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7e034-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e034-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7e034-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e034-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7e034-133">Nella casella di ricerca digitare **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="7e034-133">In the search box, type **Degreed**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_search.png)

5. <span data-ttu-id="7e034-135">Nel pannello dei risultati selezionare **Degreed** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e034-135">In the results panel, select **Degreed**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e034-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e034-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Degreed mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e034-138">In this section, you configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e034-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Degreed corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e034-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Degreed is to a user in Azure AD.</span></span> <span data-ttu-id="7e034-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Degreed.</span><span class="sxs-lookup"><span data-stu-id="7e034-140">In other words, a link relationship between an Azure AD user and the related user in Degreed needs to be established.</span></span>

<span data-ttu-id="7e034-141">Per stabilire la relazione di collegamento, in Degreed assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="7e034-141">In Degreed, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7e034-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Degreed, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e034-142">To configure and test Azure AD single sign-on with Degreed, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e034-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7e034-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e034-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e034-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e034-145">**[Creazione di un utente test di Degreed](#creating-a-degreed-test-user)**: per avere una controparte di Britta Simon in Degreed collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e034-145">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - to have a counterpart of Britta Simon in Degreed that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e034-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e034-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e034-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7e034-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e034-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e034-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Degreed.</span><span class="sxs-lookup"><span data-stu-id="7e034-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Degreed application.</span></span>

<span data-ttu-id="7e034-150">**Per configurare l'accesso Single Sign-On di Azure AD con Degreed, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e034-150">**To configure Azure AD single sign-on with Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="7e034-151">Nella pagina di integrazione dell'applicazione **Degreed** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7e034-151">In the Azure portal, on the **Degreed** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7e034-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7e034-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_samlbase.png)

3. <span data-ttu-id="7e034-155">Nella sezione **URL e dominio Degreed** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7e034-155">On the **Degreed Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_url.png)

    <span data-ttu-id="7e034-157">a.</span><span class="sxs-lookup"><span data-stu-id="7e034-157">a.</span></span> <span data-ttu-id="7e034-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://degreed.com/?orgsso=<company code>`.</span><span class="sxs-lookup"><span data-stu-id="7e034-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://degreed.com/?orgsso=<company code>`</span></span>

    <span data-ttu-id="7e034-159">b.</span><span class="sxs-lookup"><span data-stu-id="7e034-159">b.</span></span> <span data-ttu-id="7e034-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://degreed.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="7e034-160">In the **Identifier** textbox, type a URL using the following pattern: `https://degreed.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7e034-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="7e034-161">These values are not real.</span></span> <span data-ttu-id="7e034-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="7e034-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7e034-163">Per ottenere questi valori contattare il [team di supporto clienti di Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="7e034-163">Contact [Degreed Client support team](mailTo:admin@degreed.com) to get these values.</span></span> 
 


4. <span data-ttu-id="7e034-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="7e034-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_certificate.png) 

5. <span data-ttu-id="7e034-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7e034-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-degreed-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e034-168">Per configurare l'accesso Single Sign-On sul lato **Degreed**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="7e034-168">To configure single sign-on on **Degreed** side, you need to send the downloaded **Metadata XML** to [Degreed support team](mailTo:admin@degreed.com).</span></span> <span data-ttu-id="7e034-169">L'applicazione viene configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="7e034-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7e034-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7e034-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7e034-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7e034-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7e034-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e034-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e034-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e034-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e034-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7e034-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e034-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e034-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e034-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e034-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7e034-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e034-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7e034-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e034-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7e034-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e034-185">a.</span><span class="sxs-lookup"><span data-stu-id="7e034-185">a.</span></span> <span data-ttu-id="7e034-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e034-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e034-187">b.</span><span class="sxs-lookup"><span data-stu-id="7e034-187">b.</span></span> <span data-ttu-id="7e034-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e034-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e034-189">c.</span><span class="sxs-lookup"><span data-stu-id="7e034-189">c.</span></span> <span data-ttu-id="7e034-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7e034-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7e034-191">d.</span><span class="sxs-lookup"><span data-stu-id="7e034-191">d.</span></span> <span data-ttu-id="7e034-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7e034-192">Click **Create**.</span></span>
 
### <a name="creating-a-degreed-test-user"></a><span data-ttu-id="7e034-193">Creazione di un utente test Degreed</span><span class="sxs-lookup"><span data-stu-id="7e034-193">Creating a Degreed test user</span></span>

<span data-ttu-id="7e034-194">Questa sezione descrive come creare un utente chiamato Britta Simon in Degreed.</span><span class="sxs-lookup"><span data-stu-id="7e034-194">The objective of this section is to create a user called Britta Simon in Degreed.</span></span> <span data-ttu-id="7e034-195">Degreed supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7e034-195">Degreed supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7e034-196">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="7e034-196">There is no action item for you in this section.</span></span> <span data-ttu-id="7e034-197">Durante un tentativo di accesso a Degreed viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="7e034-197">A new user is created during an attempt to access Degreed if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="7e034-198">Per creare un utente manualmente è necessario contattare il [team di supporto di Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="7e034-198">If you need to create a user manually, you need to contact the [Degreed support team](mailTo:admin@degreed.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7e034-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e034-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7e034-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Degreed.</span><span class="sxs-lookup"><span data-stu-id="7e034-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Degreed.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7e034-202">**Per assegnare Britta Simon a Degreed, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e034-202">**To assign Britta Simon to Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="7e034-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e034-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7e034-205">Nell'elenco delle applicazioni selezionare **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="7e034-205">In the applications list, select **Degreed**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_app.png) 

3. <span data-ttu-id="7e034-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7e034-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7e034-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7e034-209">Click **Add** button.</span></span> <span data-ttu-id="7e034-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e034-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7e034-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7e034-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7e034-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7e034-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e034-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e034-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e034-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7e034-215">Testing single sign-on</span></span>

<span data-ttu-id="7e034-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7e034-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7e034-217">Quando si fa clic sul riquadro Degreed nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Degreed.</span><span class="sxs-lookup"><span data-stu-id="7e034-217">When you click the Degreed tile in the Access Panel, you should get automatically signed-on to your Degreed application.</span></span>
<span data-ttu-id="7e034-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e034-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e034-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7e034-219">Additional resources</span></span>

* [<span data-ttu-id="7e034-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e034-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e034-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e034-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_203.png

