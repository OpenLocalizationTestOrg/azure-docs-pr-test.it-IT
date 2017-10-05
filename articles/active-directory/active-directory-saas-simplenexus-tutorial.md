---
title: 'Esercitazione: Integrazione di Azure Active Directory con SimpleNexus| Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SimpleNexus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bddd82b986039cf67827cb407f500edb2000964b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="f609c-103">Esercitazione: Integrazione di Azure Active Directory con SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="f609c-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="f609c-104">Questa esercitazione descrive come integrare SimpleNexus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f609c-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f609c-105">L'integrazione di SimpleNexus con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f609c-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f609c-106">È possibile controllare in Azure AD chi può accedere a SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="f609c-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="f609c-107">È possibile abilitare gli utenti per l'accesso automatico a SimpleNexus (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f609c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f609c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f609c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f609c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f609c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f609c-110">Prerequisites</span></span>

<span data-ttu-id="f609c-111">Per configurare l'integrazione di Azure AD con SimpleNexus sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f609c-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="f609c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f609c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f609c-113">Sottoscrizione di SimpleNexus abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f609c-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f609c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f609c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f609c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f609c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f609c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f609c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f609c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f609c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f609c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f609c-118">Scenario description</span></span>
<span data-ttu-id="f609c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f609c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f609c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f609c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f609c-121">Aggiunta di SimpleNexus dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f609c-121">Adding SimpleNexus from the gallery</span></span>
2. <span data-ttu-id="f609c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="f609c-123">Aggiunta di SimpleNexus dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f609c-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="f609c-124">Per configurare l'integrazione di SimpleNexus in Azure AD, è necessario aggiungere SimpleNexus dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f609c-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f609c-125">**Per aggiungere SimpleNexus dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f609c-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f609c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f609c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f609c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f609c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f609c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f609c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f609c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f609c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f609c-133">Nella casella di ricerca digitare **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="f609c-133">In the search box, type **SimpleNexus**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="f609c-135">Nel pannello dei risultati selezionare **SimpleNexus** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f609c-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f609c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f609c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SimpleNexus usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f609c-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f609c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di SimpleNexus che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f609c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="f609c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="f609c-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="f609c-141">Per stabilire la relazione di collegamento, in SimpleNexus assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f609c-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f609c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SimpleNexus, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f609c-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f609c-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f609c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f609c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f609c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f609c-145">**[Creazione di un utente test di SimpleNexus](#creating-a-simplenexus-test-user)**: per avere una controparte di Britta Simon in SimpleNexus collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f609c-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f609c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f609c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f609c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f609c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f609c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f609c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="f609c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="f609c-150">**Per configurare Single Sign-On di Azure AD con SimpleNexus, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f609c-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="f609c-151">Nella pagina di integrazione dell'applicazione **SimpleNexus** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f609c-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f609c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f609c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="f609c-155">Nella sezione **URL e dominio SimpleNexus** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f609c-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="f609c-157">a.</span><span class="sxs-lookup"><span data-stu-id="f609c-157">a.</span></span> <span data-ttu-id="f609c-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://simplenexus.com/<companyname>_login`.</span><span class="sxs-lookup"><span data-stu-id="f609c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="f609c-159">b.</span><span class="sxs-lookup"><span data-stu-id="f609c-159">b.</span></span> <span data-ttu-id="f609c-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f609c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f609c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f609c-161">These values are not real.</span></span> <span data-ttu-id="f609c-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f609c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f609c-163">Per ottenere questi valori, contattare il [team di supporto clienti di SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="f609c-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="f609c-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="f609c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="f609c-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f609c-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f609c-168">Per configurare l'accesso Single Sign-On sul lato **SimpleNexus**, è necessario inviare il file **XML dei metadati** scaricato al [team di supporto di SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="f609c-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="f609c-169">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="f609c-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f609c-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f609c-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f609c-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f609c-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f609c-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f609c-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f609c-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f609c-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f609c-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f609c-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f609c-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f609c-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f609c-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f609c-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f609c-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f609c-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f609c-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f609c-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f609c-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f609c-185">a.</span><span class="sxs-lookup"><span data-stu-id="f609c-185">a.</span></span> <span data-ttu-id="f609c-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f609c-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f609c-187">b.</span><span class="sxs-lookup"><span data-stu-id="f609c-187">b.</span></span> <span data-ttu-id="f609c-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f609c-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f609c-189">c.</span><span class="sxs-lookup"><span data-stu-id="f609c-189">c.</span></span> <span data-ttu-id="f609c-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f609c-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f609c-191">d.</span><span class="sxs-lookup"><span data-stu-id="f609c-191">d.</span></span> <span data-ttu-id="f609c-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f609c-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="f609c-193">Creazione di un utente di test di SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="f609c-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="f609c-194">Per consentire agli utenti di Azure AD di accedere a SimpleNexus, è necessario eseguirne il provisioning in SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="f609c-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="f609c-195">Nel caso di SimpleNexus, il provisioning è un'attività manuale eseguita dall'amministratore tenant.</span><span class="sxs-lookup"><span data-stu-id="f609c-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="f609c-196">È possibile usare qualsiasi altro strumento di creazione di account utente di SimpleNexus o API fornita da SimpleNexus per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="f609c-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f609c-197">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f609c-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f609c-198">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="f609c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f609c-200">**Per assegnare Britta Simon a SimpleNexus, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f609c-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="f609c-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f609c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f609c-203">Nell'elenco di applicazioni selezionare **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="f609c-203">In the applications list, select **SimpleNexus**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="f609c-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f609c-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f609c-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f609c-207">Click **Add** button.</span></span> <span data-ttu-id="f609c-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f609c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f609c-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f609c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f609c-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f609c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f609c-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f609c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f609c-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f609c-213">Testing single sign-on</span></span>

<span data-ttu-id="f609c-214">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f609c-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f609c-215">Quando si fa clic sul riquadro SimpleNexus nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="f609c-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f609c-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f609c-216">Additional resources</span></span>

* [<span data-ttu-id="f609c-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f609c-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f609c-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f609c-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

