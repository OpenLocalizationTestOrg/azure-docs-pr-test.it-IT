---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workfront | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workfront.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="6f3fd-103">Esercitazione: Integrazione di Azure Active Directory con Workfront</span><span class="sxs-lookup"><span data-stu-id="6f3fd-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="6f3fd-104">Questa esercitazione descrive come integrare Workfront con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f3fd-105">L'integrazione di Workfront con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f3fd-106">È possibile controllare in Azure AD chi può accedere a Workfront</span><span class="sxs-lookup"><span data-stu-id="6f3fd-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="6f3fd-107">È possibile abilitare gli utenti per l'accesso automatico a Workfront (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f3fd-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f3fd-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f3fd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f3fd-110">Prerequisites</span></span>

<span data-ttu-id="6f3fd-111">Per configurare l'integrazione di Azure AD con Workfront, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="6f3fd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f3fd-113">Sottoscrizione di Workfront abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f3fd-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f3fd-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f3fd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f3fd-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f3fd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f3fd-118">Scenario description</span></span>
<span data-ttu-id="6f3fd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f3fd-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f3fd-121">Aggiunta di Workfront dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f3fd-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="6f3fd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="6f3fd-123">Aggiunta di Workfront dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f3fd-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="6f3fd-124">Per configurare l'integrazione di Workfront in Azure AD, è necessario aggiungere Workfront dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f3fd-125">**Per aggiungere Workfront dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3fd-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f3fd-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f3fd-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6f3fd-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6f3fd-133">Nella casella di ricerca digitare **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-133">In the search box, type **Workfront**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="6f3fd-135">Nel pannello dei risultati selezionare **Workfront** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f3fd-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f3fd-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workfront con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f3fd-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6f3fd-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Workfront che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="6f3fd-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workfront.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="6f3fd-141">Per stabilire la relazione di collegamento, in Workfront assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f3fd-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Workfront, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f3fd-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f3fd-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f3fd-145">**[Creazione di un utente di test di Workfront](#creating-a-workfront-test-user)**: per avere una controparte di Britta Simon in Workfront collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f3fd-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f3fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f3fd-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f3fd-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Workfront.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="6f3fd-150">**Per configurare l'accesso Single Sign-On di Azure AD con Workfront, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3fd-151">Nella pagina di integrazione dell'applicazione **Workfront** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6f3fd-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="6f3fd-155">Nella sezione **URL e dominio Workfront** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="6f3fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-157">a.</span></span> <span data-ttu-id="6f3fd-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.attask-ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="6f3fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-159">b.</span></span> <span data-ttu-id="6f3fd-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="6f3fd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f3fd-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6f3fd-161">These values are not real.</span></span> <span data-ttu-id="6f3fd-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6f3fd-163">Per ottenere tali valori, contattare il [team di supporto clienti di Workfront](https://www.workfront.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="6f3fd-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="6f3fd-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f3fd-168">Nella sezione **Configurazione di Workfront** fare clic su **Configura Workfront** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6f3fd-169">Copiare **l'URL di disconnessione e l'URL servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="6f3fd-171">Accedere al sito aziendale di Workfront come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="6f3fd-172">Andare a **Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="6f3fd-173">Nella finestra di dialogo **Single Sign-On** seguire questa procedura</span><span class="sxs-lookup"><span data-stu-id="6f3fd-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Configura accesso Single Sign-On][23]
   
    <span data-ttu-id="6f3fd-175">a.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-175">a.</span></span> <span data-ttu-id="6f3fd-176">Per **Type** selezionare**SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="6f3fd-177">b.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-177">b.</span></span> <span data-ttu-id="6f3fd-178">Selezionare **Service Provider ID**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="6f3fd-179">c.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-179">c.</span></span> <span data-ttu-id="6f3fd-180">Incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) nella casella di testo **Login Portal URL** (URL portale di accesso).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="6f3fd-181">d.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-181">d.</span></span> <span data-ttu-id="6f3fd-182">Incollare il valore di **URL servizio Single Sign-Out** nella casella di testo **Sign-Out URL** (URL di disconnessione).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="6f3fd-183">e.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-183">e.</span></span> <span data-ttu-id="6f3fd-184">Incollare il valore di **Modifica URL password** nella casella di testo **Change Password URL** (Modifica URL password).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="6f3fd-185">f.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-185">f.</span></span> <span data-ttu-id="6f3fd-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6f3fd-187">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f3fd-188">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f3fd-189">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f3fd-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f3fd-191">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6f3fd-193">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3fd-194">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f3fd-196">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f3fd-198">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f3fd-200">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f3fd-202">a.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-202">a.</span></span> <span data-ttu-id="6f3fd-203">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f3fd-204">b.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-204">b.</span></span> <span data-ttu-id="6f3fd-205">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f3fd-206">c.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-206">c.</span></span> <span data-ttu-id="6f3fd-207">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f3fd-208">d.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-208">d.</span></span> <span data-ttu-id="6f3fd-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="6f3fd-210">Creazione di un utente di test di Workfront</span><span class="sxs-lookup"><span data-stu-id="6f3fd-210">Creating a Workfront test user</span></span>

<span data-ttu-id="6f3fd-211">Questa sezione descrive come creare un utente chiamato Britta Simon in Workfront.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="6f3fd-212">**Per creare un utente denominato Britta Simon in Workfront, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3fd-213">Accedere al sito aziendale di Workfront come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="6f3fd-214">Nel menu in alto fare clic su **People**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="6f3fd-215">Fare clic su **New Person**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="6f3fd-216">Nella finestra di dialogo New Person seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f3fd-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Creare un utente di test di Workfront][21] 
   
    <span data-ttu-id="6f3fd-218">a.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-218">a.</span></span> <span data-ttu-id="6f3fd-219">Nella casella di testo **First Name** (Nome) digitare "Britta".</span><span class="sxs-lookup"><span data-stu-id="6f3fd-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="6f3fd-220">b.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-220">b.</span></span> <span data-ttu-id="6f3fd-221">Nella casella di testo **Last Name** (Cognome) digitare "Simon".</span><span class="sxs-lookup"><span data-stu-id="6f3fd-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="6f3fd-222">c.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-222">c.</span></span> <span data-ttu-id="6f3fd-223">Nella casella di testo **Email Address** digitare l'indirizzo di posta elettronica di Britta Simon in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="6f3fd-224">d.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-224">d.</span></span> <span data-ttu-id="6f3fd-225">Fare clic su **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f3fd-226">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3fd-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f3fd-227">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Workfront.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6f3fd-229">**Per assegnare Britta Simon a Workfront, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3fd-230">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f3fd-232">Nell'elenco delle applicazioni selezionare **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-232">In the applications list, select **Workfront**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="6f3fd-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6f3fd-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-236">Click **Add** button.</span></span> <span data-ttu-id="6f3fd-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6f3fd-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f3fd-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f3fd-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f3fd-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f3fd-242">Testing single sign-on</span></span>

<span data-ttu-id="6f3fd-243">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6f3fd-244">Quando si fa clic sul riquadro Workfront nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Workfront.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="6f3fd-245">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6f3fd-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f3fd-246">Additional resources</span></span>

* [<span data-ttu-id="6f3fd-247">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f3fd-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f3fd-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f3fd-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

