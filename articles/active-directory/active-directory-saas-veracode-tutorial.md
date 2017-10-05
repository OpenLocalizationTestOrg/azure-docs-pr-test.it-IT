---
title: 'Esercitazione: Integrazione di Azure Active Directory con Veracode | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="b818c-103">Esercitazione: Integrazione di Azure Active Directory con Veracode</span><span class="sxs-lookup"><span data-stu-id="b818c-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="b818c-104">Questa esercitazione descrive come integrare Veracode con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b818c-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b818c-105">L'integrazione di Veracode con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b818c-106">È possibile controllare in Azure AD chi può accedere a Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="b818c-107">È possibile abilitare gli utenti per l'accesso automatico a Veracode (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="b818c-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b818c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b818c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b818c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b818c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b818c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b818c-110">Prerequisites</span></span>

<span data-ttu-id="b818c-111">Per configurare l'integrazione di Azure AD con Veracode, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="b818c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b818c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b818c-113">Sottoscrizione di Veracode abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b818c-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b818c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b818c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b818c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b818c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b818c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b818c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b818c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b818c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b818c-118">Scenario description</span></span>
<span data-ttu-id="b818c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b818c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b818c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b818c-121">Aggiungere Veracode dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b818c-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="b818c-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b818c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="b818c-123">Aggiungere Veracode dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b818c-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="b818c-124">Per configurare l'integrazione di Veracode in Azure AD, è necessario aggiungere Veracode dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b818c-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b818c-125">**Per aggiungere Veracode dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b818c-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b818c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b818c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="b818c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b818c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b818c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b818c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="b818c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b818c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="b818c-133">Nella casella di ricerca digitare **Veracode**, selezionare **Veracode** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b818c-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode nell'elenco risultati](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b818c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b818c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b818c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Veracode usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b818c-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b818c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Veracode corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b818c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="b818c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="b818c-139">Per stabilire la relazione di collegamento, in Veracode assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b818c-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b818c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Veracode, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b818c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b818c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b818c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b818c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b818c-143">**[Creare un utente di test di Veracode](#create-a-veracode-test-user)**: per avere una controparte di Britta Simon in Veracode collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b818c-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b818c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b818c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b818c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b818c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b818c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b818c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b818c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="b818c-148">**Per configurare l'accesso Single Sign-On di Azure AD con Veracode, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b818c-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="b818c-149">Nella pagina di integrazione dell'applicazione **Veracode** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b818c-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b818c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b818c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="b818c-153">Nella sezione **URL e dominio Veracode** l'utente non deve eseguire alcuna operazione perché l'app è già preintegrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="b818c-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="b818c-155">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b818c-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="b818c-157">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a Veracode tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="b818c-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="b818c-158">L'applicazione Veracode prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli **attributi del token SAML**.</span><span class="sxs-lookup"><span data-stu-id="b818c-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="b818c-159">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="b818c-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="b818c-160">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="b818c-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="b818c-161">Per aggiungere i mapping di attributi obbligatori, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b818c-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="b818c-162">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="b818c-162">Attribute Name</span></span> | <span data-ttu-id="b818c-163">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="b818c-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="b818c-164">firstname</span><span class="sxs-lookup"><span data-stu-id="b818c-164">firstname</span></span> |<span data-ttu-id="b818c-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="b818c-165">User.givenname</span></span> |
    | <span data-ttu-id="b818c-166">lastname</span><span class="sxs-lookup"><span data-stu-id="b818c-166">lastname</span></span> |<span data-ttu-id="b818c-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="b818c-167">User.surname</span></span> |
    | <span data-ttu-id="b818c-168">email</span><span class="sxs-lookup"><span data-stu-id="b818c-168">email</span></span> |<span data-ttu-id="b818c-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="b818c-169">User.mail</span></span> |
    
    <span data-ttu-id="b818c-170">a.</span><span class="sxs-lookup"><span data-stu-id="b818c-170">a.</span></span> <span data-ttu-id="b818c-171">Per ogni riga di dati nella tabella precedente, fare clic su **aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="b818c-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="b818c-172">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="b818c-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="b818c-173">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="b818c-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="b818c-174">b.</span><span class="sxs-lookup"><span data-stu-id="b818c-174">b.</span></span> <span data-ttu-id="b818c-175">Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.</span><span class="sxs-lookup"><span data-stu-id="b818c-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b818c-176">c.</span><span class="sxs-lookup"><span data-stu-id="b818c-176">c.</span></span> <span data-ttu-id="b818c-177">Nella casella di testo **Valore attributo** , selezionare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="b818c-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b818c-178">d.</span><span class="sxs-lookup"><span data-stu-id="b818c-178">d.</span></span> <span data-ttu-id="b818c-179">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b818c-179">Click **Ok**.</span></span>

7. <span data-ttu-id="b818c-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b818c-180">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b818c-182">Nella sezione **Configurazione di Veracode** fare clic su **Configura Veracode** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b818c-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b818c-183">Copiare l'**ID di entità SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="b818c-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurazione di Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="b818c-185">In un'altra finestra del Web browser accedere al sito aziendale di Veracode come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b818c-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="b818c-186">Nel menu in alto fare clic su **Settings** (Impostazioni) e quindi su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b818c-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="b818c-187">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802911.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="b818c-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="b818c-188">Fare clic sulla scheda **SAML** .</span><span class="sxs-lookup"><span data-stu-id="b818c-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="b818c-189">Nella sezione **Impostazioni SAML dell’organizzazione** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b818c-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b818c-190">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802912.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="b818c-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="b818c-191">a.</span><span class="sxs-lookup"><span data-stu-id="b818c-191">a.</span></span>  <span data-ttu-id="b818c-192">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b818c-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b818c-193">b.</span><span class="sxs-lookup"><span data-stu-id="b818c-193">b.</span></span> <span data-ttu-id="b818c-194">Per caricare il certificato scaricato dal portale di Azure, fare clic su **Choose File** (Scegli file).</span><span class="sxs-lookup"><span data-stu-id="b818c-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="b818c-195">c.</span><span class="sxs-lookup"><span data-stu-id="b818c-195">c.</span></span> <span data-ttu-id="b818c-196">Selezionare **Abilita la registrazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="b818c-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="b818c-197">Nella sezione **Self Registration Settings** (Impostazioni di registrazione automatica) seguire questa procedura e quindi fare clic su **Save** (Salva):</span><span class="sxs-lookup"><span data-stu-id="b818c-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="b818c-198">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802913.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="b818c-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="b818c-199">a.</span><span class="sxs-lookup"><span data-stu-id="b818c-199">a.</span></span> <span data-ttu-id="b818c-200">In **New User Activation** (Attivazione nuovo utente) selezionare **No Activation Required** (Nessuna attivazione richiesta).</span><span class="sxs-lookup"><span data-stu-id="b818c-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="b818c-201">b.</span><span class="sxs-lookup"><span data-stu-id="b818c-201">b.</span></span> <span data-ttu-id="b818c-202">In **User Data Updates** (Aggiornamenti dati utenti) selezionare **Preference Veracode User Data** (Dati utenti Veracode di preferenza).</span><span class="sxs-lookup"><span data-stu-id="b818c-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="b818c-203">c.</span><span class="sxs-lookup"><span data-stu-id="b818c-203">c.</span></span> <span data-ttu-id="b818c-204">In **Dettagli sull’attributo SAML**selezionare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b818c-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="b818c-205">**User Roles**</span><span class="sxs-lookup"><span data-stu-id="b818c-205">**User Roles**</span></span>
      * <span data-ttu-id="b818c-206">**Policy Administrator**</span><span class="sxs-lookup"><span data-stu-id="b818c-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="b818c-207">**Reviewer**</span><span class="sxs-lookup"><span data-stu-id="b818c-207">**Reviewer**</span></span>
      * <span data-ttu-id="b818c-208">**Security Lead**</span><span class="sxs-lookup"><span data-stu-id="b818c-208">**Security Lead**</span></span>
      * <span data-ttu-id="b818c-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="b818c-209">**Executive**</span></span>
      * <span data-ttu-id="b818c-210">**Submitter**</span><span class="sxs-lookup"><span data-stu-id="b818c-210">**Submitter**</span></span>
      * <span data-ttu-id="b818c-211">**Creator**</span><span class="sxs-lookup"><span data-stu-id="b818c-211">**Creator**</span></span>
      * <span data-ttu-id="b818c-212">**All Scan Types**</span><span class="sxs-lookup"><span data-stu-id="b818c-212">**All Scan Types**</span></span>
      * <span data-ttu-id="b818c-213">**Team Memberships**</span><span class="sxs-lookup"><span data-stu-id="b818c-213">**Team Memberships**</span></span>
      * <span data-ttu-id="b818c-214">**Default Team**</span><span class="sxs-lookup"><span data-stu-id="b818c-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="b818c-215">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b818c-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b818c-216">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b818c-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b818c-217">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b818c-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b818c-218">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b818c-218">Create an Azure AD test user</span></span>

<span data-ttu-id="b818c-219">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b818c-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="b818c-221">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b818c-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b818c-222">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="b818c-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b818c-224">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b818c-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b818c-226">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b818c-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b818c-228">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b818c-228">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b818c-230">a.</span><span class="sxs-lookup"><span data-stu-id="b818c-230">a.</span></span> <span data-ttu-id="b818c-231">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b818c-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b818c-232">b.</span><span class="sxs-lookup"><span data-stu-id="b818c-232">b.</span></span> <span data-ttu-id="b818c-233">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b818c-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b818c-234">c.</span><span class="sxs-lookup"><span data-stu-id="b818c-234">c.</span></span> <span data-ttu-id="b818c-235">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="b818c-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b818c-236">d.</span><span class="sxs-lookup"><span data-stu-id="b818c-236">d.</span></span> <span data-ttu-id="b818c-237">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b818c-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="b818c-238">Creare un utente di test di Veracode</span><span class="sxs-lookup"><span data-stu-id="b818c-238">Create a Veracode test user</span></span>
<span data-ttu-id="b818c-239">Per consentire agli utenti di Azure AD di accedere a Veracode, è necessario eseguirne il provisioning in Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="b818c-240">Nel caso di Veracode, il provisioning è un'attività automatica.</span><span class="sxs-lookup"><span data-stu-id="b818c-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="b818c-241">Non è necessario eseguire alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="b818c-241">There is no action item for you.</span></span> <span data-ttu-id="b818c-242">Se necessario, gli utenti vengono creati automaticamente durante il primo tentativo di accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b818c-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="b818c-243">È possibile usare qualsiasi altro strumento o API di creazione di account utente di Veracode per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b818c-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b818c-244">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b818c-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="b818c-245">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="b818c-247">**Per assegnare Britta Simon a Veracode, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b818c-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="b818c-248">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b818c-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b818c-250">Nell'elenco delle applicazioni selezionare **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="b818c-250">In the applications list, select **Veracode**.</span></span>

    ![Collegamento di Veracode nell'elenco delle applicazioni](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="b818c-252">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b818c-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="b818c-254">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b818c-254">Click **Add** button.</span></span> <span data-ttu-id="b818c-255">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b818c-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="b818c-257">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b818c-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b818c-258">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b818c-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b818c-259">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b818c-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b818c-260">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b818c-260">Test single sign-on</span></span>

<span data-ttu-id="b818c-261">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b818c-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b818c-262">Quando si fa clic sul riquadro Veracode nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Veracode.</span><span class="sxs-lookup"><span data-stu-id="b818c-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="b818c-263">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b818c-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b818c-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b818c-264">Additional resources</span></span>

* [<span data-ttu-id="b818c-265">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b818c-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b818c-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b818c-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

