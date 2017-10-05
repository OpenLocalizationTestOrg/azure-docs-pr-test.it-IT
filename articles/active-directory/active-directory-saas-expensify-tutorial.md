---
title: 'Esercitazione: Integrazione di Azure Active Directory con Expensify | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory ed Expensify.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="4edb1-103">Esercitazione: Integrazione di Azure Active Directory con Expensify</span><span class="sxs-lookup"><span data-stu-id="4edb1-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="4edb1-104">Questa esercitazione descrive come integrare Expensify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4edb1-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4edb1-105">L'integrazione di Expensify con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4edb1-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4edb1-106">È possibile controllare in Azure AD chi può accedere a Expensify</span><span class="sxs-lookup"><span data-stu-id="4edb1-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="4edb1-107">È possibile abilitare gli utenti per l'accesso automatico a Expensify (Single Sign-On) con l'account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4edb1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4edb1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4edb1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4edb1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4edb1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4edb1-110">Prerequisites</span></span>

<span data-ttu-id="4edb1-111">Per configurare l'integrazione di Azure AD con Expensify, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4edb1-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="4edb1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4edb1-113">Sottoscrizione di Expensify abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4edb1-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4edb1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4edb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4edb1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4edb1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4edb1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4edb1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4edb1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4edb1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4edb1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4edb1-118">Scenario description</span></span>
<span data-ttu-id="4edb1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4edb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4edb1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4edb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4edb1-121">Aggiunta di Expensify dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4edb1-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="4edb1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="4edb1-123">Aggiunta di Expensify dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4edb1-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="4edb1-124">Per configurare l'integrazione di Expensify in Azure AD, è necessario aggiungere Expensify dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4edb1-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4edb1-125">**Per aggiungere Expensify dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4edb1-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4edb1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4edb1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4edb1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4edb1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4edb1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4edb1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4edb1-133">Nella casella di ricerca digitare **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-133">In the search box, type **Expensify**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="4edb1-135">Nel pannello dei risultati selezionare **Expensify** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4edb1-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4edb1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4edb1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Expensify con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4edb1-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4edb1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Expensify che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edb1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="4edb1-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="4edb1-141">Per stabilire la relazione di collegamento, in Expensify assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="4edb1-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4edb1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Expensify, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4edb1-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4edb1-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4edb1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4edb1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4edb1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4edb1-145">**[Creazione di un utente test di Expensify](#creating-an-expensify-test-user)**: per avere una controparte di Britta Simon in Expensify collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edb1-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4edb1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edb1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4edb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4edb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4edb1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4edb1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="4edb1-150">**Per configurare l'accesso Single Sign-On di Azure AD con Expensify, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4edb1-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="4edb1-151">Nella pagina di integrazione dell'applicazione **Expensify** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4edb1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4edb1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="4edb1-155">Nella sezione **URL e dominio Expensify** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4edb1-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="4edb1-157">a.</span><span class="sxs-lookup"><span data-stu-id="4edb1-157">a.</span></span> <span data-ttu-id="4edb1-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.expensify.com/authentication/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="4edb1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="4edb1-159">b.</span><span class="sxs-lookup"><span data-stu-id="4edb1-159">b.</span></span> <span data-ttu-id="4edb1-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="4edb1-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="4edb1-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4edb1-161">These values are not real.</span></span> <span data-ttu-id="4edb1-162">è necessario aggiornarli con l'URL di accesso e l'URL identificatore effettivi.</span><span class="sxs-lookup"><span data-stu-id="4edb1-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="4edb1-163">Per ottenere questi valori contattare il [team di supporto clienti di Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="4edb1-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="4edb1-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="4edb1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="4edb1-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4edb1-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4edb1-168">Per abilitare SSO in Expensify è necessario avere abilitato **Domain Control** (Controllo di dominio) nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4edb1-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="4edb1-169">Per abilitare il controllo di dominio nell'applicazione seguire [questa procedura](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="4edb1-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="4edb1-170">Per ulteriore supporto, contattare il [team di supporto clienti di Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="4edb1-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="4edb1-171">Dopo aver abilitato il controllo di dominio seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4edb1-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="4edb1-173">a.</span><span class="sxs-lookup"><span data-stu-id="4edb1-173">a.</span></span> <span data-ttu-id="4edb1-174">Accedere all'applicazione Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="4edb1-175">b.</span><span class="sxs-lookup"><span data-stu-id="4edb1-175">b.</span></span> <span data-ttu-id="4edb1-176">Nel barra degli strumenti in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="4edb1-177">c.</span><span class="sxs-lookup"><span data-stu-id="4edb1-177">c.</span></span> <span data-ttu-id="4edb1-178">Nel pannello sinistro fare clic su **Domain** (Dominio).</span><span class="sxs-lookup"><span data-stu-id="4edb1-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="4edb1-179">d.</span><span class="sxs-lookup"><span data-stu-id="4edb1-179">d.</span></span> <span data-ttu-id="4edb1-180">Fare clic sul nome di dominio verificato.</span><span class="sxs-lookup"><span data-stu-id="4edb1-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="4edb1-181">e.</span><span class="sxs-lookup"><span data-stu-id="4edb1-181">e.</span></span> <span data-ttu-id="4edb1-182">Nel pannello sinistro fare clic su **SAML**, quindi selezionare **Enabled** (Abilitato).</span><span class="sxs-lookup"><span data-stu-id="4edb1-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="4edb1-183">f.</span><span class="sxs-lookup"><span data-stu-id="4edb1-183">f.</span></span> <span data-ttu-id="4edb1-184">Aprire i metadati della federazione scaricati da Azure AD nel Blocco note, copiare il contenuto e incollarlo nella casella di testo **Identity Provider Metadata** (Metadati del provider di identità).</span><span class="sxs-lookup"><span data-stu-id="4edb1-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="4edb1-185">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4edb1-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4edb1-186">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="4edb1-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4edb1-187">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4edb1-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4edb1-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="4edb1-189">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4edb1-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4edb1-191">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4edb1-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4edb1-192">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4edb1-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4edb1-194">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4edb1-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4edb1-196">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4edb1-198">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4edb1-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4edb1-200">a.</span><span class="sxs-lookup"><span data-stu-id="4edb1-200">a.</span></span> <span data-ttu-id="4edb1-201">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4edb1-202">b.</span><span class="sxs-lookup"><span data-stu-id="4edb1-202">b.</span></span> <span data-ttu-id="4edb1-203">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4edb1-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4edb1-204">c.</span><span class="sxs-lookup"><span data-stu-id="4edb1-204">c.</span></span> <span data-ttu-id="4edb1-205">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4edb1-206">d.</span><span class="sxs-lookup"><span data-stu-id="4edb1-206">d.</span></span> <span data-ttu-id="4edb1-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="4edb1-208">Creazione di un utente test di Expensify</span><span class="sxs-lookup"><span data-stu-id="4edb1-208">Creating an Expensify test user</span></span>

<span data-ttu-id="4edb1-209">In questa sezione viene creato un utente chiamato Britta Simon in Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="4edb1-210">Collaborare con il [team di supporto clienti di Expensify](mailto:help@expensify.com) per aggiungere gli utenti nella piattaforma Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4edb1-211">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4edb1-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4edb1-212">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4edb1-214">**Per assegnare Britta Simon a Expensify, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4edb1-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="4edb1-215">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4edb1-217">Nell'elenco di applicazioni selezionare **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-217">In the applications list, select **Expensify**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="4edb1-219">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4edb1-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4edb1-221">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-221">Click **Add** button.</span></span> <span data-ttu-id="4edb1-222">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4edb1-224">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4edb1-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4edb1-225">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4edb1-226">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4edb1-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4edb1-227">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4edb1-227">Testing single sign-on</span></span>

<span data-ttu-id="4edb1-228">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4edb1-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="4edb1-229">Quando si fa clic sul riquadro Expensify nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione Expensify.</span><span class="sxs-lookup"><span data-stu-id="4edb1-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4edb1-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4edb1-230">Additional resources</span></span>

* [<span data-ttu-id="4edb1-231">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edb1-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4edb1-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edb1-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

