---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="1f378-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="1f378-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="1f378-104">Questa esercitazione descrive come integrare Salesforce Sandbox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f378-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f378-105">L'integrazione di Salesforce Sandbox con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f378-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f378-106">È possibile controllare in Azure AD chi può accedere a Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="1f378-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="1f378-107">È possibile abilitare gli utenti per l'accesso automatico a Salesforce Sandbox (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f378-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f378-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f378-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f378-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f378-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1f378-110">Prerequisites</span></span>

<span data-ttu-id="1f378-111">Per configurare l'integrazione di Azure AD con Salesforce Sandbox, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f378-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="1f378-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f378-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f378-113">Sottoscrizione di Salesforce Sandbox abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1f378-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f378-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1f378-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f378-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f378-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f378-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1f378-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f378-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f378-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f378-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1f378-118">Scenario description</span></span>
<span data-ttu-id="1f378-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1f378-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f378-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f378-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f378-121">Aggiunta di Salesforce Sandbox dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1f378-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="1f378-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="1f378-123">Aggiunta di Salesforce Sandbox dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1f378-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="1f378-124">Per configurare l'integrazione di Salesforce Sandbox in Azure AD, è necessario aggiungere Salesforce Sandbox dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1f378-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f378-125">**Per aggiungere Salesforce Sandbox dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f378-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f378-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1f378-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f378-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1f378-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f378-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1f378-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1f378-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1f378-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1f378-133">Nella casella di ricerca digitare **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="1f378-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="1f378-135">Nel pannello dei risultati selezionare **Salesforce Sandbox** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f378-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f378-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f378-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Salesforce Sandbox in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1f378-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f378-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Salesforce Sandbox che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f378-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="1f378-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="1f378-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Nome utente** in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="1f378-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Salesforce Sandbox, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f378-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f378-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1f378-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f378-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f378-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f378-145">**[Creazione di un utente test di Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**: per avere una controparte di Britta Simon in Salesforce Sandbox collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1f378-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f378-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f378-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f378-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1f378-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f378-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f378-149">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="1f378-150">**Per configurare Single Sign-On di Azure AD con Salesforce Sandbox, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f378-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="1f378-151">Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1f378-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1f378-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1f378-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="1f378-155">Nella sezione **URL e dominio Salesforce Sandbox** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f378-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="1f378-157">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="1f378-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f378-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="1f378-158">This value is not the real.</span></span> <span data-ttu-id="1f378-159">Aggiornare questo valore con l'URL di accesso effettivo. Contattare il [team di supporto clienti di Sandbox Salesforce](https://help.salesforce.com/support) per ottenere questo valore.</span><span class="sxs-lookup"><span data-stu-id="1f378-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="1f378-160">Se l'accesso Single Sign-On è già stato configurato per un'altra istanza di Salesforce Sandbox nella directory, sarà necessario configurare anche l'**identificatore** in modo che abbia lo stesso valore di **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="1f378-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="1f378-161">Per trovare il campo **Identificatore**, selezionare la casella di controllo **Impostazioni avanzate** nella pagina **Configura URL app** della finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="1f378-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="1f378-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="1f378-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="1f378-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1f378-164">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1f378-166">Nella sezione **Configurazione di Salesforce Sandbox** fare clic su **Configura Salesforce Sandbox** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="1f378-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f378-167">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1f378-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="1f378-168">![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="1f378-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="1f378-169">Aprire una nuova scheda del browser e accedere all'account di amministratore di Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="1f378-170">Nel menu in alto fare clic su **Impostazione**.</span><span class="sxs-lookup"><span data-stu-id="1f378-170">In the menu on the top, click **Setup**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="1f378-172">Nel riquadro di spostamento a sinistra, fare clic su **Security Controls** (Controlli di sicurezza) e quindi fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="1f378-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="1f378-174">Nella sezione Impostazioni Single Sign-On eseguire la procedura seguente: ![Configurazione dell'accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="1f378-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="1f378-175">a.</span><span class="sxs-lookup"><span data-stu-id="1f378-175">a.</span></span>  <span data-ttu-id="1f378-176">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="1f378-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="1f378-177">b.</span><span class="sxs-lookup"><span data-stu-id="1f378-177">b.</span></span>  <span data-ttu-id="1f378-178">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="1f378-178">Click **New**.</span></span>

12. <span data-ttu-id="1f378-179">Nella sezione Impostazioni SAML Single Sign-On, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1f378-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="1f378-181">a.Nella casella di testo Nome digitare il nome della configurazione, ad esempio *SPSSOWAAD\_Test*.</span><span class="sxs-lookup"><span data-stu-id="1f378-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="1f378-182">b.</span><span class="sxs-lookup"><span data-stu-id="1f378-182">b.</span></span> <span data-ttu-id="1f378-183">Incollare il valore **SMAL Entity ID** (ID entità SMAL) nella casella di testo **Issuer** (Autorità di certificazione).</span><span class="sxs-lookup"><span data-stu-id="1f378-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="1f378-184">c.</span><span class="sxs-lookup"><span data-stu-id="1f378-184">c.</span></span> <span data-ttu-id="1f378-185">Nella casella di testo **ID entità** digitare **https://test.salesforce.com** se è la prima istanza di Salesforce Sandbox aggiunta alla directory.</span><span class="sxs-lookup"><span data-stu-id="1f378-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="1f378-186">Se esiste già un'istanza di Salesforce Sandbox, in **ID entità** digitare l'**URL di accesso**, che deve avere questo formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="1f378-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="1f378-187">d.</span><span class="sxs-lookup"><span data-stu-id="1f378-187">d.</span></span> <span data-ttu-id="1f378-188">Per caricare il certificato scaricato, fare clic su **Sfoglia** .</span><span class="sxs-lookup"><span data-stu-id="1f378-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="1f378-189">e.</span><span class="sxs-lookup"><span data-stu-id="1f378-189">e.</span></span> <span data-ttu-id="1f378-190">In **SAML Identity Type** (Tipo di identità SAML) selezionare **Assertion contains the Federation ID from the User object** (L'asserzione contiene l'ID federazione dell'oggetto utente).</span><span class="sxs-lookup"><span data-stu-id="1f378-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="1f378-191">f.</span><span class="sxs-lookup"><span data-stu-id="1f378-191">f.</span></span> <span data-ttu-id="1f378-192">In **SAML Identity Location**(Percorso identità SAML) selezionare **Identity is in the NameIdentifier element of the Subject statement** (L'identità è nell'elemento NameIdentifier dell'istruzione Subject).</span><span class="sxs-lookup"><span data-stu-id="1f378-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="1f378-193">g.</span><span class="sxs-lookup"><span data-stu-id="1f378-193">g.</span></span> <span data-ttu-id="1f378-194">Incollare **URL servizio Single Sign-On** nella casella di testo **URL di accesso provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="1f378-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="1f378-195">h.</span><span class="sxs-lookup"><span data-stu-id="1f378-195">h.</span></span> <span data-ttu-id="1f378-196">SFDC non supporta la disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="1f378-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="1f378-197">Come soluzione alternativa, incollare "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" nella casella di testo **Identity Provider Logout URL** (URL di disconnessione provider di identità).</span><span class="sxs-lookup"><span data-stu-id="1f378-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="1f378-198">i.</span><span class="sxs-lookup"><span data-stu-id="1f378-198">i.</span></span> <span data-ttu-id="1f378-199">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="1f378-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="1f378-200">j.</span><span class="sxs-lookup"><span data-stu-id="1f378-200">j.</span></span> <span data-ttu-id="1f378-201">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1f378-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="1f378-202">Abilitare il dominio</span><span class="sxs-lookup"><span data-stu-id="1f378-202">Enable your domain</span></span>
<span data-ttu-id="1f378-203">In questa sezione si presuppone che sia già stato creato un dominio.</span><span class="sxs-lookup"><span data-stu-id="1f378-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="1f378-204">Per altre informazioni, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="1f378-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="1f378-205">**Per abilitare il dominio, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1f378-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="1f378-206">Nel riquadro di spostamento a sinistra fare clic su **Domain Management** (Gestione dominio) e quindi su **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="1f378-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="1f378-208">Assicurarsi che il dominio sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1f378-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="1f378-209">Nella sezione **Login Page Settings** (Impostazioni pagina di accesso) fare clic su **Edit** (Modifica), quindi per **Authentication Service** (Servizio di autenticazione) selezionare il nome dell'impostazione Single Sign-On SAML definita nella sezione precedente e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="1f378-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="1f378-211">Non appena si dispone di un dominio configurato, gli utenti devono utilizzare l'URL del dominio per l'accesso a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="1f378-212">Per ottenere il valore dell'URL, fare clic sul profilo SSO creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="1f378-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="1f378-213">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1f378-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f378-214">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="1f378-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f378-215">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f378-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f378-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f378-217">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f378-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1f378-219">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1f378-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f378-220">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1f378-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f378-222">passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="1f378-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f378-224">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1f378-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f378-226">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f378-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f378-228">a.</span><span class="sxs-lookup"><span data-stu-id="1f378-228">a.</span></span> <span data-ttu-id="1f378-229">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f378-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f378-230">b.</span><span class="sxs-lookup"><span data-stu-id="1f378-230">b.</span></span> <span data-ttu-id="1f378-231">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f378-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f378-232">c.</span><span class="sxs-lookup"><span data-stu-id="1f378-232">c.</span></span> <span data-ttu-id="1f378-233">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="1f378-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f378-234">d.</span><span class="sxs-lookup"><span data-stu-id="1f378-234">d.</span></span> <span data-ttu-id="1f378-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1f378-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="1f378-236">Creazione di un utente test di Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="1f378-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="1f378-237">In questa sezione si crea un utente di nome Britta Simon in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="1f378-238">Salesforce Sandbox supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1f378-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="1f378-239">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1f378-239">There is no action item for you in this section.</span></span> <span data-ttu-id="1f378-240">Se un utente non esiste in Salesforce Sandbox, ne viene creato uno nuovo quando si tenta di accedere a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f378-241">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f378-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f378-242">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="1f378-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1f378-244">**Per assegnare Britta Simon a Salesforce Sandbox, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f378-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="1f378-245">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1f378-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1f378-247">Nell'elenco di applicazioni selezionare **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="1f378-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="1f378-249">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1f378-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1f378-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1f378-251">Click **Add** button.</span></span> <span data-ttu-id="1f378-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1f378-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1f378-254">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="1f378-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f378-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1f378-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f378-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1f378-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f378-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1f378-257">Testing single sign-on</span></span>

<span data-ttu-id="1f378-258">Per testare le impostazioni di SSO, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1f378-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="1f378-259">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f378-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f378-260">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1f378-260">Additional resources</span></span>

* [<span data-ttu-id="1f378-261">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f378-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f378-262">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f378-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1f378-263">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="1f378-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

