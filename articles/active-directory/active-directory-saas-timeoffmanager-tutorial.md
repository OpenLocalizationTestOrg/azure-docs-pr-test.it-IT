---
title: 'Esercitazione: Integrazione di Azure Active Directory con TimeOffManager | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="bd93e-103">Esercitazione: Integrazione di Azure Active Directory con TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bd93e-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="bd93e-104">Questa esercitazione descrive come integrare TimeOffManager con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd93e-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd93e-105">L'integrazione di TimeOffManager con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd93e-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bd93e-106">È possibile controllare in Azure AD chi può accedere a TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bd93e-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="bd93e-107">È possibile abilitare gli utenti per l'accesso automatico a TimeOffManager (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="bd93e-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd93e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bd93e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd93e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd93e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd93e-110">Prerequisites</span></span>

<span data-ttu-id="bd93e-111">Per configurare l'integrazione di Azure AD con TimeOffManager, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd93e-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="bd93e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd93e-113">Sottoscrizione di TimeOffManager abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd93e-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd93e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bd93e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd93e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd93e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd93e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bd93e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd93e-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd93e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd93e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bd93e-118">Scenario description</span></span>
<span data-ttu-id="bd93e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bd93e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd93e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd93e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd93e-121">Aggiungere TimeOffManager dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bd93e-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="bd93e-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="bd93e-123">Aggiungere TimeOffManager dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bd93e-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="bd93e-124">Per configurare l'integrazione di TimeOffManager in Azure AD, è necessario aggiungere TimeOffManager dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bd93e-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd93e-125">**Per aggiungere TimeOffManager dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bd93e-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bd93e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd93e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bd93e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="bd93e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd93e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="bd93e-133">Nella casella di ricerca digitare **TimeOffManager**, selezionare **TimeOffManager** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd93e-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bd93e-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93e-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="bd93e-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TimeOffManager usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bd93e-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd93e-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di TimeOffManager corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="bd93e-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bd93e-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="bd93e-139">Per stabilire la relazione di collegamento, in TimeOffManager assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="bd93e-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bd93e-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con TimeOffManager, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd93e-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd93e-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd93e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd93e-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd93e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd93e-143">**[Creare un utente di test di TimeOffManager](#create-a-timeoffmanager-test-user)**: per avere una controparte di Britta Simon in TimeOffManager collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93e-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd93e-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd93e-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="bd93e-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bd93e-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bd93e-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bd93e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="bd93e-148">**Per configurare l'accesso Single Sign-On di Azure AD con TimeOffManager, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bd93e-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93e-149">Nella pagina di integrazione dell'applicazione **TimeOffManager** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="bd93e-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bd93e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="bd93e-153">Nella sezione **URL e dominio TimeOffManager** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd93e-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![Sezione URL e dominio TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="bd93e-155">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="bd93e-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd93e-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="bd93e-156">This value is not real.</span></span> <span data-ttu-id="bd93e-157">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="bd93e-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="bd93e-158">È possibile ottenere questo valore dalla **pagina delle impostazioni per l'accesso Single Sign-On**, illustrata più avanti nell'esercitazione, oppure contattando il [team di supporto di TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd93e-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="bd93e-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="bd93e-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="bd93e-161">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a TimeOffManger con il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="bd93e-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="bd93e-162">L'applicazione TimeOffManger si aspetta che le asserzioni SAML abbiano un formato specifico, quindi è necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="bd93e-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="bd93e-163">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="bd93e-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="bd93e-164">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="bd93e-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="bd93e-165">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="bd93e-165">Attribute Name</span></span> | <span data-ttu-id="bd93e-166">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="bd93e-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bd93e-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="bd93e-167">Firstname</span></span> |<span data-ttu-id="bd93e-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="bd93e-168">User.givenname</span></span> |
    | <span data-ttu-id="bd93e-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="bd93e-169">Lastname</span></span> |<span data-ttu-id="bd93e-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="bd93e-170">User.surname</span></span> |
    | <span data-ttu-id="bd93e-171">Email</span><span class="sxs-lookup"><span data-stu-id="bd93e-171">Email</span></span> |<span data-ttu-id="bd93e-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="bd93e-172">User.mail</span></span> |
    
    <span data-ttu-id="bd93e-173">a.</span><span class="sxs-lookup"><span data-stu-id="bd93e-173">a.</span></span>  <span data-ttu-id="bd93e-174">Per ogni riga di dati nella tabella precedente, fare clic su **aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="bd93e-175">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="bd93e-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="bd93e-176">![attributi token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "attributi token SAML")</span><span class="sxs-lookup"><span data-stu-id="bd93e-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="bd93e-177">b.</span><span class="sxs-lookup"><span data-stu-id="bd93e-177">b.</span></span>  <span data-ttu-id="bd93e-178">Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.</span><span class="sxs-lookup"><span data-stu-id="bd93e-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bd93e-179">c.</span><span class="sxs-lookup"><span data-stu-id="bd93e-179">c.</span></span>  <span data-ttu-id="bd93e-180">Nella casella di testo **Valore attributo** selezionare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="bd93e-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="bd93e-181">d.</span><span class="sxs-lookup"><span data-stu-id="bd93e-181">d.</span></span>  <span data-ttu-id="bd93e-182">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="bd93e-183">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bd93e-183">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bd93e-185">Nella sezione **Configurazione di TimeOffManager** fare clic su **Configura TimeOffManager** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bd93e-186">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="bd93e-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sezione Configurazione di TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="bd93e-188">In un'altra finestra del Web browser accedere al sito aziendale di TimeOffManager come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bd93e-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="bd93e-189">Andare a **Account \> Account Options \> Single Sign-On Settings** (Account > Opzioni account > Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="bd93e-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="bd93e-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="bd93e-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="bd93e-191">Nella sezione **Single Sign-On Settings** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bd93e-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="bd93e-192">![Impostazioni di Single Sign-On](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bd93e-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="bd93e-193">a.</span><span class="sxs-lookup"><span data-stu-id="bd93e-193">a.</span></span> <span data-ttu-id="bd93e-194">Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e incollare l’intero certificato nella casella di testo **Certificate X.509** .</span><span class="sxs-lookup"><span data-stu-id="bd93e-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="bd93e-195">b.</span><span class="sxs-lookup"><span data-stu-id="bd93e-195">b.</span></span> <span data-ttu-id="bd93e-196">Nella casella di testo **IdP Issuer** (Autorità emittente IdP) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bd93e-197">c.</span><span class="sxs-lookup"><span data-stu-id="bd93e-197">c.</span></span> <span data-ttu-id="bd93e-198">Nella casella di testo **IdP Endpoint URL** (URL endpoint IdP) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bd93e-199">d.</span><span class="sxs-lookup"><span data-stu-id="bd93e-199">d.</span></span> <span data-ttu-id="bd93e-200">Per **Enforce SAML** (Applica SAML), selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="bd93e-201">e.</span><span class="sxs-lookup"><span data-stu-id="bd93e-201">e.</span></span> <span data-ttu-id="bd93e-202">Per **Auto-Create Users** (Crea utenti in automatico), selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="bd93e-203">f.</span><span class="sxs-lookup"><span data-stu-id="bd93e-203">f.</span></span> <span data-ttu-id="bd93e-204">Nella casella di testo **Logout URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bd93e-205">g.</span><span class="sxs-lookup"><span data-stu-id="bd93e-205">g.</span></span> <span data-ttu-id="bd93e-206">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="bd93e-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="bd93e-207">Nella pagina **Single Sign on settings** (Impostazioni Single Sign-On) copiare il valore dell'**URL del servizio consumer di asserzione** e incollarlo nella casella di testo **URL di risposta** nella sezione **URL e dominio TimeOffManager** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="bd93e-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="bd93e-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="bd93e-209">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="bd93e-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bd93e-210">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="bd93e-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bd93e-211">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd93e-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bd93e-212">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93e-212">Create an Azure AD test user</span></span>
<span data-ttu-id="bd93e-213">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93e-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="bd93e-215">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd93e-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93e-216">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bd93e-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd93e-218">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="bd93e-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi --> Tutti gli utenti](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd93e-220">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd93e-222">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd93e-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd93e-224">a.</span><span class="sxs-lookup"><span data-stu-id="bd93e-224">a.</span></span> <span data-ttu-id="bd93e-225">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd93e-226">b.</span><span class="sxs-lookup"><span data-stu-id="bd93e-226">b.</span></span> <span data-ttu-id="bd93e-227">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd93e-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd93e-228">c.</span><span class="sxs-lookup"><span data-stu-id="bd93e-228">c.</span></span> <span data-ttu-id="bd93e-229">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bd93e-230">d.</span><span class="sxs-lookup"><span data-stu-id="bd93e-230">d.</span></span> <span data-ttu-id="bd93e-231">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="bd93e-232">Creare un utente di test di TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bd93e-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="bd93e-233">Per consentire agli utenti di Azure AD di accedere a TimeOffManager, è necessario eseguirne il provisioning in TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bd93e-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="bd93e-234">TimeOffManager supporta solo il provisioning just in time dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bd93e-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="bd93e-235">Non è necessario eseguire alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="bd93e-235">There is no action item for you.</span></span>  

<span data-ttu-id="bd93e-236">Gli utenti vengono aggiunti automaticamente durante l'utilizzo di Single Sign-on primo accesso.</span><span class="sxs-lookup"><span data-stu-id="bd93e-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="bd93e-237">È possibile usare qualsiasi altro strumento o API di creazione di account utente di TimeOffManager per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93e-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bd93e-238">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93e-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="bd93e-239">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bd93e-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Assegna utente][200] 

<span data-ttu-id="bd93e-241">**Per assegnare Britta Simon a TimeOffManager, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bd93e-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93e-242">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bd93e-244">Nell'elenco delle applicazioni selezionare **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-244">In the applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager nell'elenco di app](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="bd93e-246">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="bd93e-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="bd93e-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-248">Click **Add** button.</span></span> <span data-ttu-id="bd93e-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="bd93e-251">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="bd93e-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bd93e-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd93e-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd93e-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bd93e-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd93e-254">Test single sign-on</span></span>

<span data-ttu-id="bd93e-255">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bd93e-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bd93e-256">Quando si fa clic sul riquadro TimeOffManager nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bd93e-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="bd93e-257">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd93e-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd93e-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bd93e-258">Additional resources</span></span>

* [<span data-ttu-id="bd93e-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd93e-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd93e-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd93e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

