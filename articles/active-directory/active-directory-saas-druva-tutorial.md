---
title: 'Esercitazione: Integrazione di Azure Active Directory con Druva| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="2db67-103">Esercitazione: Integrazione di Azure Active Directory con Druva</span><span class="sxs-lookup"><span data-stu-id="2db67-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="2db67-104">Questa esercitazione descrive come integrare Druva con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2db67-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2db67-105">L'integrazione di Druva con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db67-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2db67-106">È possibile controllare in Azure AD chi può accedere a Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="2db67-107">È possibile abilitare gli utenti per l'accesso automatico a Druva (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db67-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2db67-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2db67-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2db67-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2db67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2db67-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2db67-110">Prerequisites</span></span>

<span data-ttu-id="2db67-111">Per configurare l'integrazione di Azure AD con Druva, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db67-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="2db67-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2db67-113">Sottoscrizione di Druva abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2db67-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2db67-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2db67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2db67-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2db67-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2db67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2db67-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2db67-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2db67-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2db67-118">Scenario description</span></span>
<span data-ttu-id="2db67-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2db67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2db67-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2db67-121">Aggiunta di Druva dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2db67-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="2db67-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="2db67-123">Aggiunta di Druva dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2db67-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="2db67-124">Per configurare l'integrazione di Druva in Azure AD, è necessario aggiungere Druva dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2db67-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2db67-125">**Per aggiungere Druva dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2db67-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2db67-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2db67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="2db67-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2db67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2db67-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2db67-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="2db67-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="2db67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="2db67-133">Nella casella di ricerca digitare **Druva**, selezionare **Druva** dal pannello dei risultati quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2db67-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva nell'elenco risultati](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2db67-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db67-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2db67-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Druva in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2db67-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2db67-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Druva che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db67-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="2db67-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="2db67-139">Per stabilire la relazione di collegamento, in Druva assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="2db67-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2db67-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Druva, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db67-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2db67-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2db67-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2db67-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2db67-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2db67-143">**[Creare un utente di test di Druva](#create-a-druva-test-user)**: per avere una controparte di Britta Simon in Druva collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db67-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2db67-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db67-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2db67-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2db67-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2db67-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db67-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2db67-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="2db67-148">**Per configurare l'accesso Single Sign-On di Azure AD con Druva, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2db67-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="2db67-149">Nella pagina di integrazione dell'applicazione **Druva** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2db67-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="2db67-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2db67-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="2db67-153">Nella sezione **URL e dominio Druva** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2db67-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="2db67-155">Nella casella di testo **URL accesso** digitare l'URL: `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="2db67-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="2db67-156">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="2db67-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="2db67-158">L'applicazione Druva prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli **attributi del token SAML**.</span><span class="sxs-lookup"><span data-stu-id="2db67-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="2db67-160">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente ed eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="2db67-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="2db67-161">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="2db67-161">Attribute Name</span></span>      | <span data-ttu-id="2db67-162">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="2db67-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="2db67-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="2db67-163">insync\_auth\_token</span></span> |<span data-ttu-id="2db67-164">Immettere il valore generato del token</span><span class="sxs-lookup"><span data-stu-id="2db67-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="2db67-165">a.</span><span class="sxs-lookup"><span data-stu-id="2db67-165">a.</span></span> <span data-ttu-id="2db67-166">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="2db67-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2db67-169">b.</span><span class="sxs-lookup"><span data-stu-id="2db67-169">b.</span></span> <span data-ttu-id="2db67-170">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="2db67-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2db67-171">c.</span><span class="sxs-lookup"><span data-stu-id="2db67-171">c.</span></span> <span data-ttu-id="2db67-172">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="2db67-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="2db67-173">In una fase successiva dell'esercitazione verrà illustrato il valore generato del token.</span><span class="sxs-lookup"><span data-stu-id="2db67-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="2db67-174">d.</span><span class="sxs-lookup"><span data-stu-id="2db67-174">d.</span></span> <span data-ttu-id="2db67-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2db67-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="2db67-176">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2db67-176">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2db67-178">Nella sezione **Configurazione di Druva** fare clic su **Configura Druva** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="2db67-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2db67-179">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="2db67-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="2db67-181">In un'altra finestra del Web browser accedere al sito aziendale di Druva come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2db67-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="2db67-182">Passare a **Manage \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="2db67-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="2db67-183">![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795091.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="2db67-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="2db67-184">Nella finestra di dialogo Single Sign-On Settings seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2db67-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="2db67-185">![Impostazioni di Single Sign-On](./media/active-directory-saas-druva-tutorial/ic795092.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2db67-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="2db67-186">a.</span><span class="sxs-lookup"><span data-stu-id="2db67-186">a.</span></span> <span data-ttu-id="2db67-187">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **ID Provider Login URL** (URL accesso provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2db67-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="2db67-188">b.</span><span class="sxs-lookup"><span data-stu-id="2db67-188">b.</span></span> <span data-ttu-id="2db67-189">Incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **URL di disconnessione provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="2db67-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="2db67-190">c.</span><span class="sxs-lookup"><span data-stu-id="2db67-190">c.</span></span> <span data-ttu-id="2db67-191">Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **ID Provider Certificate**</span><span class="sxs-lookup"><span data-stu-id="2db67-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="2db67-192">d.</span><span class="sxs-lookup"><span data-stu-id="2db67-192">d.</span></span> <span data-ttu-id="2db67-193">Per aprire la pagina **Settings** fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="2db67-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="2db67-194">Nella pagina **Settings** fare clic su **Generate SSO Token**.</span><span class="sxs-lookup"><span data-stu-id="2db67-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="2db67-195">![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795093.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="2db67-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="2db67-196">Nella finestra di dialogo **Single Sign-on Authentication Token** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2db67-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="2db67-197">![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")</span><span class="sxs-lookup"><span data-stu-id="2db67-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="2db67-198">a.</span><span class="sxs-lookup"><span data-stu-id="2db67-198">a.</span></span> <span data-ttu-id="2db67-199">Fare clic su **Copia**, incollare il valore copiato nella casella di testo **Valore** nella sezione **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="2db67-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="2db67-200">b.</span><span class="sxs-lookup"><span data-stu-id="2db67-200">b.</span></span> <span data-ttu-id="2db67-201">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="2db67-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="2db67-202">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2db67-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2db67-203">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="2db67-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2db67-204">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2db67-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2db67-205">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db67-205">Create an Azure AD test user</span></span>

<span data-ttu-id="2db67-206">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2db67-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="2db67-208">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2db67-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2db67-209">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="2db67-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2db67-211">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2db67-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2db67-213">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2db67-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2db67-215">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2db67-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2db67-217">a.</span><span class="sxs-lookup"><span data-stu-id="2db67-217">a.</span></span> <span data-ttu-id="2db67-218">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2db67-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2db67-219">b.</span><span class="sxs-lookup"><span data-stu-id="2db67-219">b.</span></span> <span data-ttu-id="2db67-220">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2db67-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2db67-221">c.</span><span class="sxs-lookup"><span data-stu-id="2db67-221">c.</span></span> <span data-ttu-id="2db67-222">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="2db67-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2db67-223">d.</span><span class="sxs-lookup"><span data-stu-id="2db67-223">d.</span></span> <span data-ttu-id="2db67-224">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2db67-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="2db67-225">Creare un utente test Druva</span><span class="sxs-lookup"><span data-stu-id="2db67-225">Create a Druva test user</span></span>

<span data-ttu-id="2db67-226">Per consentire agli utenti di Azure AD di accedere a Druva, è necessario eseguirne il provisioning in Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="2db67-227">Nel caso di Druva, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="2db67-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="2db67-228">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2db67-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="2db67-229">Accedere al sito aziendale di **Druva** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2db67-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="2db67-230">Passare a **Manage (Gestisci) \> Users (Utenti)**.</span><span class="sxs-lookup"><span data-stu-id="2db67-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="2db67-231">![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="2db67-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="2db67-232">Fare clic su **Create New**.</span><span class="sxs-lookup"><span data-stu-id="2db67-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="2db67-233">![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="2db67-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="2db67-234">Nella finestra di dialogo Create New User seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2db67-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="2db67-235">![Crea nuovo utente](./media/active-directory-saas-druva-tutorial/ic795099.png "Crea nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="2db67-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="2db67-236">a.</span><span class="sxs-lookup"><span data-stu-id="2db67-236">a.</span></span> <span data-ttu-id="2db67-237">Nella casella di testo **Email address** (Indirizzo di posta elettronica) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2db67-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="2db67-238">b.</span><span class="sxs-lookup"><span data-stu-id="2db67-238">b.</span></span> <span data-ttu-id="2db67-239">Nella casella di testo **Name** (Nome) immettere il nome dell'utente, ad esempio **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2db67-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="2db67-240">c.</span><span class="sxs-lookup"><span data-stu-id="2db67-240">c.</span></span> <span data-ttu-id="2db67-241">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="2db67-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="2db67-242">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Druva per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2db67-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2db67-243">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db67-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="2db67-244">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="2db67-246">**Per assegnare Britta Simon a Druva, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2db67-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="2db67-247">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2db67-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2db67-249">Nell'elenco delle applicazioni selezionare **Druva**.</span><span class="sxs-lookup"><span data-stu-id="2db67-249">In the applications list, select **Druva**.</span></span>

    ![Collegamento Druva nell'elenco Applicazioni](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="2db67-251">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2db67-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="2db67-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2db67-253">Click **Add** button.</span></span> <span data-ttu-id="2db67-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2db67-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="2db67-256">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2db67-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2db67-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2db67-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2db67-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2db67-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2db67-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2db67-259">Test single sign-on</span></span>

<span data-ttu-id="2db67-260">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2db67-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2db67-261">Quando si fa clic sul riquadro Druva nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Druva.</span><span class="sxs-lookup"><span data-stu-id="2db67-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="2db67-262">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2db67-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2db67-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2db67-263">Additional resources</span></span>

* [<span data-ttu-id="2db67-264">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2db67-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2db67-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2db67-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

