---
title: 'Esercitazione: Integrazione di Azure Active Directory con ScreenSteps | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="839ec-103">Esercitazione: Integrazione di Azure Active Directory con ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="839ec-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="839ec-104">Questa esercitazione descrive come integrare ScreenSteps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="839ec-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="839ec-105">L'integrazione di ScreenSteps con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="839ec-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="839ec-106">È possibile controllare in Azure AD chi può accedere a ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="839ec-107">È possibile abilitare gli utenti per l'accesso automatico a ScreenSteps (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839ec-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="839ec-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="839ec-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="839ec-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="839ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="839ec-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="839ec-110">Prerequisites</span></span>

<span data-ttu-id="839ec-111">Per configurare l'integrazione di Azure AD con ScreenSteps, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="839ec-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="839ec-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="839ec-113">Sottoscrizione di ScreenSteps abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="839ec-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="839ec-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="839ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="839ec-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="839ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="839ec-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="839ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="839ec-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="839ec-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="839ec-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="839ec-118">Scenario description</span></span>
<span data-ttu-id="839ec-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="839ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="839ec-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="839ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="839ec-121">Aggiunta di ScreenSteps dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="839ec-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="839ec-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="839ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="839ec-123">Aggiunta di ScreenSteps dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="839ec-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="839ec-124">Per configurare l'integrazione di ScreenSteps in Azure AD, è necessario aggiungere ScreenSteps dalla raccolta al proprio elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="839ec-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="839ec-125">**Per aggiungere ScreenSteps dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="839ec-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="839ec-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="839ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="839ec-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="839ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="839ec-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="839ec-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="839ec-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="839ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="839ec-133">Nella casella di ricerca digitare **ScreenSteps**, selezionare **ScreenSteps** dal pannello dei risultati quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="839ec-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps nell'elenco risultati](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="839ec-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="839ec-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="839ec-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ScreenSteps usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="839ec-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="839ec-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di ScreenSteps che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839ec-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="839ec-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="839ec-139">Per stabilire la relazione di collegamento, in ScreenSteps assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="839ec-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="839ec-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con ScreenSteps, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="839ec-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="839ec-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="839ec-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="839ec-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="839ec-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="839ec-143">**[Creare un utente test di ScreenSteps](#create-a-screensteps-test-user)**: per avere una controparte di Britta Simon in ScreenSteps collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839ec-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="839ec-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839ec-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="839ec-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="839ec-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="839ec-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="839ec-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="839ec-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="839ec-148">**Per configurare Single Sign-On di Azure AD con ScreenSteps, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="839ec-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="839ec-149">Nella pagina di integrazione dell'applicazione **ScreenSteps** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="839ec-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="839ec-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="839ec-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="839ec-153">Nella sezione **URL e dominio ScreenSteps** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="839ec-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="839ec-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenantname>.ScreenSteps.com`.</span><span class="sxs-lookup"><span data-stu-id="839ec-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="839ec-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="839ec-156">This value is not real.</span></span> <span data-ttu-id="839ec-157">Aggiornare questo valore con l'URL di accesso effettivo, come illustrato più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="839ec-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="839ec-158">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="839ec-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="839ec-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="839ec-160">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="839ec-162">Nella sezione **Configurazione di ScreenSteps** fare clic su **Configura ScreenSteps** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="839ec-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="839ec-163">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="839ec-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="839ec-165">In un'altra finestra del Web browser accedere al sito aziendale di ScreenSteps come amministratore.</span><span class="sxs-lookup"><span data-stu-id="839ec-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="839ec-166">Click **Account Settings** (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="839ec-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="839ec-167">![Gestione degli account](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Gestione degli account")</span><span class="sxs-lookup"><span data-stu-id="839ec-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="839ec-168">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="839ec-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="839ec-169">![Autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="839ec-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="839ec-170">Fare clic su **Create Single Sign-on Endpoint** (Crea endpoint Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="839ec-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="839ec-171">![Autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="839ec-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="839ec-172">Nella sezione **Create Single Sign-on Endpoint** (Crea endpoint Single Sign-On) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="839ec-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="839ec-173">![Creare un endpoint di autenticazione](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Creare un endpoint di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="839ec-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="839ec-174">a.</span><span class="sxs-lookup"><span data-stu-id="839ec-174">a.</span></span> <span data-ttu-id="839ec-175">Nella casella di testo **Title** digitare un titolo.</span><span class="sxs-lookup"><span data-stu-id="839ec-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="839ec-176">b.</span><span class="sxs-lookup"><span data-stu-id="839ec-176">b.</span></span> <span data-ttu-id="839ec-177">Nell'elenco **Mode** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="839ec-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="839ec-178">c.</span><span class="sxs-lookup"><span data-stu-id="839ec-178">c.</span></span> <span data-ttu-id="839ec-179">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="839ec-179">Click **Create**.</span></span>

12. <span data-ttu-id="839ec-180">**Modificare** il nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="839ec-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="839ec-181">![Modifica endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Modifica endpoint")</span><span class="sxs-lookup"><span data-stu-id="839ec-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="839ec-182">Nella sezione **Edit Single Sign-on Endpoint** (Modifica endpoint Single Sign-On) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="839ec-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="839ec-183">![Endpoint di autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Endpoint di autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="839ec-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="839ec-184">a.</span><span class="sxs-lookup"><span data-stu-id="839ec-184">a.</span></span> <span data-ttu-id="839ec-185">Fare clic su **Upload new SAML Certificate file** (Carica il nuovo file di certificato SAML) e quindi caricare il certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="839ec-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="839ec-186">b.</span><span class="sxs-lookup"><span data-stu-id="839ec-186">b.</span></span> <span data-ttu-id="839ec-187">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Remote Login URL** (URL accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="839ec-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="839ec-188">c.</span><span class="sxs-lookup"><span data-stu-id="839ec-188">c.</span></span> <span data-ttu-id="839ec-189">Incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **Log out URL** (URL di disconnessione).</span><span class="sxs-lookup"><span data-stu-id="839ec-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="839ec-190">d.</span><span class="sxs-lookup"><span data-stu-id="839ec-190">d.</span></span> <span data-ttu-id="839ec-191">Selezionare un **gruppo** a cui assegnare gli utenti quando viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="839ec-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="839ec-192">e.</span><span class="sxs-lookup"><span data-stu-id="839ec-192">e.</span></span> <span data-ttu-id="839ec-193">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="839ec-193">Click **Update**.</span></span>

    <span data-ttu-id="839ec-194">f.</span><span class="sxs-lookup"><span data-stu-id="839ec-194">f.</span></span> <span data-ttu-id="839ec-195">Copiare il valore di **SAML Consumer URL** (URL consumer SAML) negli Appunti e incollarlo nella casella di testo **URL di accesso** in **URL e dominio ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="839ec-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="839ec-196">g.</span><span class="sxs-lookup"><span data-stu-id="839ec-196">g.</span></span> <span data-ttu-id="839ec-197">Tornare a **Edit Single Sign-on Endpoint** (Modifica endpoint Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="839ec-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="839ec-198">h.</span><span class="sxs-lookup"><span data-stu-id="839ec-198">h.</span></span> <span data-ttu-id="839ec-199">Fare clic sul pulsante **Make default for account** (Rendi predefinito per account) per usare questo endpoint per tutti gli utenti che accedono a ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="839ec-200">In alternativa, è possibile scegliere il pulsante **Add to Site** (Aggiungi a sito) per usare questo endpoint per siti specifici in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="839ec-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="839ec-201">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="839ec-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="839ec-202">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="839ec-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="839ec-203">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="839ec-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="839ec-204">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="839ec-204">Create an Azure AD test user</span></span>

<span data-ttu-id="839ec-205">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="839ec-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="839ec-207">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="839ec-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="839ec-208">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="839ec-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="839ec-210">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="839ec-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="839ec-212">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="839ec-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="839ec-214">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="839ec-214">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="839ec-216">a.</span><span class="sxs-lookup"><span data-stu-id="839ec-216">a.</span></span> <span data-ttu-id="839ec-217">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="839ec-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="839ec-218">b.</span><span class="sxs-lookup"><span data-stu-id="839ec-218">b.</span></span> <span data-ttu-id="839ec-219">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="839ec-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="839ec-220">c.</span><span class="sxs-lookup"><span data-stu-id="839ec-220">c.</span></span> <span data-ttu-id="839ec-221">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="839ec-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="839ec-222">d.</span><span class="sxs-lookup"><span data-stu-id="839ec-222">d.</span></span> <span data-ttu-id="839ec-223">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="839ec-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="839ec-224">Creare un utente test di ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="839ec-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="839ec-225">In questa sezione viene creato un utente di nome Britta Simon in ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="839ec-226">Collaborare con il [team di supporto clienti di ScreenSteps](https://www.screensteps.com/contact) per aggiungere gli utenti nella piattaforma ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="839ec-227">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="839ec-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="839ec-228">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="839ec-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="839ec-229">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="839ec-231">**Per assegnare Britta Simon a ScreenSteps, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="839ec-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="839ec-232">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="839ec-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="839ec-234">Nell'elenco delle applicazioni, selezionare **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="839ec-234">In the applications list, select **ScreenSteps**.</span></span>

    ![Collegamento di ScreenSteps nell'elenco delle applicazioni](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="839ec-236">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="839ec-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="839ec-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="839ec-238">Click **Add** button.</span></span> <span data-ttu-id="839ec-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="839ec-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="839ec-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="839ec-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="839ec-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="839ec-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="839ec-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="839ec-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="839ec-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="839ec-244">Test single sign-on</span></span>

<span data-ttu-id="839ec-245">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="839ec-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="839ec-246">Quando si fa clic sul riquadro ScreenSteps nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="839ec-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="839ec-247">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="839ec-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="839ec-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="839ec-248">Additional resources</span></span>

* [<span data-ttu-id="839ec-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="839ec-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="839ec-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="839ec-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

