---
title: 'Esercitazione: Integrazione di Azure Active Directory con Predictix Assortment Planning | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Predictix Assortment Planning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: cc7ad4aa5260276e26406b6b79c039372e5ee69f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="c3dc6-103">Esercitazione: Integrazione di Azure Active Directory con Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="c3dc6-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="c3dc6-104">Questa esercitazione descrive come integrare Predictix Assortment Planning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3dc6-105">L'integrazione di Predictix Assortment Planning con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3dc6-106">È possibile controllare in Azure AD chi può accedere a Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-106">You can control in Azure AD who has access to Predictix Assortment Planning.</span></span>
- <span data-ttu-id="c3dc6-107">È possibile abilitare gli utenti perché possano accedere automaticamente, ossia tramite accesso Single Sign-On, a Predictix Assortment Planning con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c3dc6-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c3dc6-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3dc6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c3dc6-110">Prerequisites</span></span>

<span data-ttu-id="c3dc6-111">Per configurare l'integrazione di Azure AD con Predictix Assortment Planning, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span></span>

- <span data-ttu-id="c3dc6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3dc6-113">Sottoscrizione di Predictix Assortment Planning abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3dc6-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3dc6-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3dc6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3dc6-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3dc6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c3dc6-118">Scenario description</span></span>
<span data-ttu-id="c3dc6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3dc6-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3dc6-121">Aggiunta di Predictix Assortment Planning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3dc6-121">Adding Predictix Assortment Planning from the gallery</span></span>
2. <span data-ttu-id="c3dc6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3dc6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-the-gallery"></a><span data-ttu-id="c3dc6-123">Aggiunta di Predictix Assortment Planning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3dc6-123">Adding Predictix Assortment Planning from the gallery</span></span>
<span data-ttu-id="c3dc6-124">Per configurare l'integrazione di Predictix Assortment Planning in Azure AD, è necessario aggiungere Predictix Assortment Planning dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3dc6-125">**Per aggiungere Predictix Assortment Planning dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3dc6-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3dc6-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="c3dc6-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3dc6-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="c3dc6-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="c3dc6-133">Nella casella di ricerca digitare **Predictix Assortment Planning**, selezionare **Predictix Assortment Planning** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-133">In the search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix Assortment Planning nell'elenco risultati](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c3dc6-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3dc6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c3dc6-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Predictix Assortment Planning usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3dc6-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3dc6-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Predictix Assortment Planning che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span></span> <span data-ttu-id="c3dc6-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span></span>

<span data-ttu-id="c3dc6-139">Per stabilire la relazione di collegamento, in Predictix Assortment Planning assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-139">In Predictix Assortment Planning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3dc6-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Predictix Assortment Planning, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-140">To configure and test Azure AD single sign-on with Predictix Assortment Planning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3dc6-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3dc6-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3dc6-143">**[Creare un utente test di Predictix Assortment Planning](#create-a-predictix-assortment-planning-test-user)**: per avere una controparte di Britta Simon in Predictix Assortment Planning che sia collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3dc6-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3dc6-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c3dc6-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3dc6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c3dc6-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="c3dc6-148">**Per configurare l'accesso Single Sign-On di Azure AD con Predictix Assortment Planning, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3dc6-148">**To configure Azure AD single sign-on with Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="c3dc6-149">Nella pagina di integrazione dell'applicazione **Predictix Assortment Planning** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-149">In the Azure portal, on the **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="c3dc6-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="c3dc6-153">Nella sezione **URL e dominio Predictix Assortment Planning** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-153">On the **Predictix Assortment Planning Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="c3dc6-155">a.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-155">a.</span></span> <span data-ttu-id="c3dc6-156">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="c3dc6-157">b.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-157">b.</span></span> <span data-ttu-id="c3dc6-158">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="c3dc6-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c3dc6-159">These values are not real.</span></span> <span data-ttu-id="c3dc6-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c3dc6-161">Per ottenere questi valori, contattare il [team di supporto clienti di Predictix Assortment Planning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) to get these values.</span></span> 
 


4. <span data-ttu-id="c3dc6-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="c3dc6-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c3dc6-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3dc6-166">Nella sezione **Configurazione di Predictix Assortment Planning** fare clic su **Configura Predictix Assortment Planning** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-166">On the **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c3dc6-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c3dc6-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="c3dc6-169">Per configurare l'accesso Single Sign-On sul lato **Predictix Assortment Planning** , è necessario inviare il **Certificato (Base64)** scaricato e i valori di **SAML Entity ID** (ID entità SAML), **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) e **Sign-Out URL** al [team di supporto di Predictix Assortment Planning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-169">To configure single sign-on on **Predictix Assortment Planning** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  to [Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="c3dc6-170">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c3dc6-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3dc6-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3dc6-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c3dc6-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3dc6-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c3dc6-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="c3dc6-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3dc6-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3dc6-178">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c3dc6-180">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c3dc6-182">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c3dc6-184">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3dc6-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c3dc6-186">a.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-186">a.</span></span> <span data-ttu-id="c3dc6-187">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3dc6-188">b.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-188">b.</span></span> <span data-ttu-id="c3dc6-189">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c3dc6-190">c.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-190">c.</span></span> <span data-ttu-id="c3dc6-191">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c3dc6-192">d.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-192">d.</span></span> <span data-ttu-id="c3dc6-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="c3dc6-194">Creare un utente test di Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="c3dc6-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="c3dc6-195">In questa sezione viene creato un utente di nome Britta Simon in Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="c3dc6-196">Per aggiungere gli utenti nella piattaforma di [Predictix Assortment Planning](http://www.infor.com/contact/), contattare il team di supporto tecnico di Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) to add the users in the Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="c3dc6-197">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-197">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c3dc6-198">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3dc6-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="c3dc6-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Assortment Planning.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="c3dc6-201">**Per assegnare Britta Simon a Predictix Assortment Planning, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3dc6-201">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="c3dc6-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c3dc6-204">Nell'elenco delle applicazioni selezionare **Predictix Assortment Planning**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-204">In the applications list, select **Predictix Assortment Planning**.</span></span>

    ![Collegamento di Predictix Assortment Planning nell'elenco delle applicazioni](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="c3dc6-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="c3dc6-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-208">Click **Add** button.</span></span> <span data-ttu-id="c3dc6-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="c3dc6-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3dc6-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3dc6-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c3dc6-214">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3dc6-214">Test single sign-on</span></span>

<span data-ttu-id="c3dc6-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3dc6-216">Quando si fa clic sul riquadro Predictix Assortment Planning nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="c3dc6-216">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span></span>
<span data-ttu-id="c3dc6-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3dc6-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3dc6-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c3dc6-218">Additional resources</span></span>

* [<span data-ttu-id="c3dc6-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3dc6-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3dc6-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3dc6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

