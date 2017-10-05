---
title: 'Esercitazione: Integrazione di Azure Active Directory con 15Five | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e 15Five.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="f5f1b-103">Esercitazione: Integrazione di Azure Active Directory con 15Five</span><span class="sxs-lookup"><span data-stu-id="f5f1b-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="f5f1b-104">Questa esercitazione descrive come integrare 15Five con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5f1b-105">L'integrazione di 15Five con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5f1b-106">È possibile controllare in Azure AD chi può accedere a 15Five</span><span class="sxs-lookup"><span data-stu-id="f5f1b-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="f5f1b-107">È possibile abilitare gli utenti per l'accesso automatico a 15Five (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5f1b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5f1b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5f1b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5f1b-110">Prerequisites</span></span>

<span data-ttu-id="f5f1b-111">Per configurare l'integrazione di Azure AD con 15Five, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="f5f1b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5f1b-113">Sottoscrizione di 15Five abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5f1b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5f1b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5f1b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5f1b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5f1b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f5f1b-118">Scenario description</span></span>
<span data-ttu-id="f5f1b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5f1b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5f1b-121">Aggiunta di 15Five dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5f1b-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="f5f1b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="f5f1b-123">Aggiunta di 15Five dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5f1b-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="f5f1b-124">Per configurare l'integrazione di 15Five in Azure AD, è necessario aggiungere 15Five dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5f1b-125">**Per aggiungere 15Five dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5f1b-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5f1b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5f1b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5f1b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f5f1b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f5f1b-133">Nella casella di ricerca digitare **15Five**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-133">In the search box, type **15Five**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="f5f1b-135">Nel pannello dei risultati selezionare **15Five** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5f1b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5f1b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 15Five con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5f1b-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5f1b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di 15Five che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="f5f1b-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 15Five.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="f5f1b-141">Per stabilire la relazione di collegamento, in 15Five assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5f1b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con 15Five, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5f1b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5f1b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5f1b-145">**[Creazione di un utente di test di 15Five](#creating-a-15five-test-user)**: per avere una controparte di Britta Simon in 15Five collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5f1b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5f1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5f1b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5f1b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione 15Five.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="f5f1b-150">**Per configurare l'accesso Single Sign-On di Azure AD con 15Five, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5f1b-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="f5f1b-151">Nella pagina di integrazione dell'applicazione **15Five** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f5f1b-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="f5f1b-155">Nella sezione **URL e dominio 15Five** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="f5f1b-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-157">a.</span></span> <span data-ttu-id="f5f1b-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.15five.com`.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="f5f1b-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-159">b.</span></span> <span data-ttu-id="f5f1b-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="f5f1b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5f1b-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f5f1b-161">These values are not real.</span></span> <span data-ttu-id="f5f1b-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5f1b-163">Per ottenere tali valori, contattare il [team di supporto clienti di 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="f5f1b-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="f5f1b-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f5f1b-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5f1b-168">Per configurare l'accesso Single Sign-On sul lato **15Five**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="f5f1b-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5f1b-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5f1b-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5f1b-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5f1b-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f5f1b-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5f1b-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5f1b-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5f1b-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5f1b-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5f1b-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5f1b-184">a.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-184">a.</span></span> <span data-ttu-id="f5f1b-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5f1b-186">b.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-186">b.</span></span> <span data-ttu-id="f5f1b-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5f1b-188">c.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-188">c.</span></span> <span data-ttu-id="f5f1b-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5f1b-190">d.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-190">d.</span></span> <span data-ttu-id="f5f1b-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="f5f1b-192">Creazione di un utente di test di 15Five</span><span class="sxs-lookup"><span data-stu-id="f5f1b-192">Creating a 15Five test user</span></span>

<span data-ttu-id="f5f1b-193">Per consentire agli utenti di Azure AD di accedere a 15Five, è necessario effettuarne il provisioning in 15Five.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="f5f1b-194">Nel caso di 15Five, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="f5f1b-195">Per configurare il provisioning utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="f5f1b-196">Accedere al sito aziendale di **15Five** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="f5f1b-197">Passare a **Gestisci azienda**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="f5f1b-198">![Gestire una società](./media/active-directory-saas-15five-tutorial/IC784675.png "Gestire una società")</span><span class="sxs-lookup"><span data-stu-id="f5f1b-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="f5f1b-199">Passare a **Persone \> Aggiungi persone**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="f5f1b-200">![Persone](./media/active-directory-saas-15five-tutorial/IC784676.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="f5f1b-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="f5f1b-201">Nella sezione Add New Person seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5f1b-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="f5f1b-202">![Aggiungere una nuova persona](./media/active-directory-saas-15five-tutorial/IC784677.png "Aggiungere una nuova persona")</span><span class="sxs-lookup"><span data-stu-id="f5f1b-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="f5f1b-203">a.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-203">a.</span></span> <span data-ttu-id="f5f1b-204">Digitare il **Nome**, il **Cognome**, il **Titolo**, l'**Indirizzo email** di un account utente Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="f5f1b-205">b.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-205">b.</span></span> <span data-ttu-id="f5f1b-206">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="f5f1b-207">Il titolare dell'account Azure AD riceve un messaggio di posta elettronica contenente un collegamento per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5f1b-208">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5f1b-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5f1b-209">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a 15Five.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f5f1b-211">**Per assegnare Britta Simon a 15Five, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5f1b-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="f5f1b-212">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f5f1b-214">Nell'elenco delle applicazioni selezionare **15Five**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-214">In the applications list, select **15Five**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="f5f1b-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f5f1b-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-218">Click **Add** button.</span></span> <span data-ttu-id="f5f1b-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f5f1b-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5f1b-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5f1b-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5f1b-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5f1b-224">Testing single sign-on</span></span>

<span data-ttu-id="f5f1b-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5f1b-226">Quando si fa clic sul riquadro 15Five nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione 15Five.</span><span class="sxs-lookup"><span data-stu-id="f5f1b-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="f5f1b-227">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5f1b-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f5f1b-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f5f1b-228">Additional resources</span></span>

* [<span data-ttu-id="f5f1b-229">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5f1b-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5f1b-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5f1b-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

