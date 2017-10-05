---
title: 'Esercitazione: Integrazione di Azure Active Directory con HPE SaaS | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e HPE SaaS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 5e6f0da531df85359aa47477248dd020a039e7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="2a1fd-103">Esercitazione: Integrazione di Azure Active Directory con HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="2a1fd-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="2a1fd-104">Questa esercitazione descrive come integrare HPE SaaS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a1fd-105">L'integrazione di HPE SaaS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a1fd-106">È possibile controllare in Azure AD chi può accedere a HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="2a1fd-106">You can control in Azure AD who has access to HPE SaaS</span></span>
- <span data-ttu-id="2a1fd-107">È possibile abilitare gli utenti per l'accesso automatico a HPE SaaS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a1fd-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2a1fd-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a1fd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a1fd-110">Prerequisites</span></span>

<span data-ttu-id="2a1fd-111">Per configurare l'integrazione di Azure AD con HPE SaaS, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

- <span data-ttu-id="2a1fd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a1fd-113">Sottoscrizione di HPE SaaS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2a1fd-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a1fd-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a1fd-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a1fd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a1fd-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a1fd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2a1fd-118">Scenario description</span></span>
<span data-ttu-id="2a1fd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a1fd-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a1fd-121">Aggiunta di HPE SaaS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2a1fd-121">Adding HPE SaaS from the gallery</span></span>
2. <span data-ttu-id="2a1fd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="2a1fd-123">Aggiunta di HPE SaaS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2a1fd-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="2a1fd-124">Per configurare l'integrazione di HPE SaaS in Azure AD, è necessario aggiungere HPE SaaS dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a1fd-125">**Per aggiungere HPE SaaS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2a1fd-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a1fd-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a1fd-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a1fd-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2a1fd-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2a1fd-133">Nella casella di ricerca digitare **HPE SaaS**</span><span class="sxs-lookup"><span data-stu-id="2a1fd-133">In the search box, type **HPE SaaS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="2a1fd-135">Nel pannello dei risultati selezionare **HPE SaaS** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a1fd-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a1fd-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HPE SaaS usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a1fd-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a1fd-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di HPE SaaS corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span></span> <span data-ttu-id="2a1fd-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>

<span data-ttu-id="2a1fd-141">Per stabilire la relazione di collegamento, in HPE SaaS assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2a1fd-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con HPE SaaS, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a1fd-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a1fd-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a1fd-145">**[Creazione di un utente di test di HPE SaaS](#creating-an-hpe-saas-test-user)**: per avere una controparte di Britta Simon in HPE SaaS collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a1fd-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a1fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a1fd-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a1fd-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="2a1fd-150">**Per configurare Single Sign-On di Azure AD con HPE SaaS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2a1fd-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="2a1fd-151">Nella pagina di integrazione dell'applicazione **HPE SaaS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2a1fd-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="2a1fd-155">Nella sezione **URL e dominio HPE SaaS** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="2a1fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-157">a.</span></span> <span data-ttu-id="2a1fd-158">Nella casella di testo **URL di accesso** digitare l'URL come: `https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="2a1fd-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="2a1fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-159">b.</span></span> <span data-ttu-id="2a1fd-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="2a1fd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a1fd-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2a1fd-161">These values are not real.</span></span> <span data-ttu-id="2a1fd-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2a1fd-163">Per ottenere questi valori, contattare il [team di supporto clienti di HPE SaaS](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="2a1fd-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="2a1fd-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2a1fd-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2a1fd-168">Per configurare l'accesso Single Sign-On sul lato **HPE SaaS**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di HPE SaaS](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="2a1fd-169">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2a1fd-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2a1fd-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2a1fd-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a1fd-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a1fd-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2a1fd-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2a1fd-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a1fd-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a1fd-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a1fd-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a1fd-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a1fd-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a1fd-185">a.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-185">a.</span></span> <span data-ttu-id="2a1fd-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a1fd-187">b.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-187">b.</span></span> <span data-ttu-id="2a1fd-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a1fd-189">c.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-189">c.</span></span> <span data-ttu-id="2a1fd-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2a1fd-191">d.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-191">d.</span></span> <span data-ttu-id="2a1fd-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="2a1fd-193">Creazione di un utente di test di HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="2a1fd-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="2a1fd-194">Questa sezione descrive come creare un utente chiamato Britta Simon in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="2a1fd-195">Collaborare con il [team di supporto di HPE SaaS](https://saas.hpe.com/en-us/contact) per aggiungere gli utenti nell'account HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a1fd-196">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a1fd-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2a1fd-197">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2a1fd-199">**Per assegnare Britta Simon a HPE SaaS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2a1fd-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="2a1fd-200">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2a1fd-202">Nell'elenco delle applicazioni selezionare **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-202">In the applications list, select **HPE SaaS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="2a1fd-204">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2a1fd-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-206">Click **Add** button.</span></span> <span data-ttu-id="2a1fd-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2a1fd-209">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a1fd-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a1fd-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a1fd-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2a1fd-212">Testing single sign-on</span></span>

<span data-ttu-id="2a1fd-213">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a1fd-214">Quando si fa clic sul riquadro HPE SaaS nel pannello di accesso, si accederà automaticamente all'applicazione HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a1fd-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>
<span data-ttu-id="2a1fd-215">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2a1fd-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a1fd-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2a1fd-216">Additional resources</span></span>

* [<span data-ttu-id="2a1fd-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a1fd-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a1fd-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a1fd-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

