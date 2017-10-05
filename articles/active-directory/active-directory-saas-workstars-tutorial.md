---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workstars | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workstars.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: e17c85689fa3aebf00ebf559185032b90103b4a5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="6a466-103">Esercitazione: integrazione di Azure Active Directory con Workstars</span><span class="sxs-lookup"><span data-stu-id="6a466-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="6a466-104">Questa esercitazione descrive come integrare Workstars con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a466-104">In this tutorial, you learn how to integrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a466-105">L'integrazione di Workstars con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a466-105">Integrating Workstars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a466-106">È possibile controllare in Azure AD chi può accedere a Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-106">You can control in Azure AD who has access to Workstars.</span></span>
- <span data-ttu-id="6a466-107">È possibile abilitare gli utenti per l'accesso automatico a Workstars (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a466-107">You can enable your users to automatically get signed-on to Workstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6a466-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a466-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6a466-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a466-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a466-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a466-110">Prerequisites</span></span>

<span data-ttu-id="6a466-111">Per configurare l'integrazione di Azure AD con Workstars, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a466-111">To configure Azure AD integration with Workstars, you need the following items:</span></span>

- <span data-ttu-id="6a466-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a466-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a466-113">Sottoscrizione di Workstars abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6a466-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a466-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6a466-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a466-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a466-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a466-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6a466-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a466-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a466-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a466-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6a466-118">Scenario description</span></span>
<span data-ttu-id="6a466-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6a466-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a466-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a466-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a466-121">Aggiunta di Workstars dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6a466-121">Adding Workstars from the gallery</span></span>
2. <span data-ttu-id="6a466-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a466-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-the-gallery"></a><span data-ttu-id="6a466-123">Aggiunta di Workstars dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6a466-123">Adding Workstars from the gallery</span></span>
<span data-ttu-id="6a466-124">Per configurare l'integrazione di Workstars in Azure AD, è necessario aggiungere Workstars dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6a466-124">To configure the integration of Workstars into Azure AD, you need to add Workstars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a466-125">**Per aggiungere Workstars dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6a466-125">**To add Workstars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a466-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6a466-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="6a466-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6a466-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a466-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a466-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="6a466-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a466-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="6a466-133">Nella casella di ricerca digitare **Workstars**, selezionare **Workstars** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a466-133">In the search box, type **Workstars**, select **Workstars** from result panel then click **Add** button to add the application.</span></span>

    ![Workstars nell'elenco dei risultati](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6a466-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a466-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6a466-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workstars usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6a466-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a466-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Workstars che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a466-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workstars is to a user in Azure AD.</span></span> <span data-ttu-id="6a466-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-138">In other words, a link relationship between an Azure AD user and the related user in Workstars needs to be established.</span></span>

<span data-ttu-id="6a466-139">Per stabilire la relazione di collegamento, in Workstars assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6a466-139">In Workstars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a466-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Workstars, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a466-140">To configure and test Azure AD single sign-on with Workstars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a466-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6a466-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a466-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a466-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a466-143">**[Creare un utente di test di Workstars](#create-a-workstars-test-user)**: per avere una controparte di Britta Simon in Workstars collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a466-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - to have a counterpart of Britta Simon in Workstars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a466-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a466-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a466-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6a466-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6a466-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a466-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6a466-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="6a466-148">**Per configurare Single Sign-On di Azure AD con Workstars, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6a466-148">**To configure Azure AD single sign-on with Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="6a466-149">Nella pagina di integrazione dell'applicazione **Workstars** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6a466-149">In the Azure portal, on the **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="6a466-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6a466-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="6a466-153">Nella sezione **URL e dominio Workstars** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6a466-153">On the **Workstars Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="6a466-155">a.</span><span class="sxs-lookup"><span data-stu-id="6a466-155">a.</span></span> <span data-ttu-id="6a466-156">Nella casella di testo **Identificatore** digitare l'URL: `https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="6a466-156">In the **Identifier** textbox, type the URL: `https://workstars.com`</span></span>

    <span data-ttu-id="6a466-157">b.</span><span class="sxs-lookup"><span data-stu-id="6a466-157">b.</span></span> <span data-ttu-id="6a466-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="6a466-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a466-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="6a466-159">The value is not real.</span></span> <span data-ttu-id="6a466-160">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="6a466-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="6a466-161">Per ottenere il valore, contattare il [team di supporto di Workstars](https://support.workstars.com).</span><span class="sxs-lookup"><span data-stu-id="6a466-161">Contact [Workstars support team](https://support.workstars.com) to get the value.</span></span>
 
4. <span data-ttu-id="6a466-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6a466-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="6a466-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6a466-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a466-166">Nella sezione **Configurazione di Workstars** fare clic su **Configura Workstars** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="6a466-166">On the **Workstars Configuration** section, click **Configure Workstars** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a466-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6a466-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="6a466-169">In un'altra finestra del browser accedere al sito aziendale di Workstars come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6a466-169">In another browser window, sign on to your Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="6a466-170">Nella barra degli strumenti principale scegliere **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a466-170">In the main toolbar, click **Settings**.</span></span>

    ![Impostazioni di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="6a466-172">Passare ad **Accesso** > **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a466-172">Go to **Sign On** > **Settings**.</span></span>

    ![Accesso a Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Impostazioni di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="6a466-175">Nella pagina **Single Sign On (SAML) - Settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6a466-175">On the **Single Sign On (SAML) - Settings** page, perform the following steps:</span></span>
    
    ![SAML di Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="6a466-177">a.</span><span class="sxs-lookup"><span data-stu-id="6a466-177">a.</span></span> <span data-ttu-id="6a466-178">Nella casella di testo **Nome provider identità** digitare **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="6a466-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="6a466-179">b.</span><span class="sxs-lookup"><span data-stu-id="6a466-179">b.</span></span> <span data-ttu-id="6a466-180">Nella casella di testo **Identity Provider Entity ID** (ID entità provider di identità) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a466-180">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a466-181">c.</span><span class="sxs-lookup"><span data-stu-id="6a466-181">c.</span></span> <span data-ttu-id="6a466-182">Copiare il contenuto del file del certificato scaricato nel Blocco note e incollarlo nella casella di testo **Certificato x509** .</span><span class="sxs-lookup"><span data-stu-id="6a466-182">Copy the content of the downloaded certificate file in notepad, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="6a466-183">d.</span><span class="sxs-lookup"><span data-stu-id="6a466-183">d.</span></span> <span data-ttu-id="6a466-184">Nella casella di testo **SAML SSO URL** (URL SSO SAML) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a466-184">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6a466-185">e.</span><span class="sxs-lookup"><span data-stu-id="6a466-185">e.</span></span> <span data-ttu-id="6a466-186">Nella casella di testo **Remote Log Out URL** (URL di disconnessione remota) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a466-186">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6a466-187">f.</span><span class="sxs-lookup"><span data-stu-id="6a466-187">f.</span></span> <span data-ttu-id="6a466-188">impostare **ID nome** su **Email (Default)** (Posta elettronica (impostazione predefinita)).</span><span class="sxs-lookup"><span data-stu-id="6a466-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="6a466-189">g.</span><span class="sxs-lookup"><span data-stu-id="6a466-189">g.</span></span> <span data-ttu-id="6a466-190">Fare clic su **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="6a466-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="6a466-191">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6a466-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a466-192">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6a466-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a466-193">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a466-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a466-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a466-194">Create an Azure AD test user</span></span>

<span data-ttu-id="6a466-195">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a466-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="6a466-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a466-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a466-198">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="6a466-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6a466-200">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6a466-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6a466-202">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6a466-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6a466-204">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6a466-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6a466-206">a.</span><span class="sxs-lookup"><span data-stu-id="6a466-206">a.</span></span> <span data-ttu-id="6a466-207">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a466-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a466-208">b.</span><span class="sxs-lookup"><span data-stu-id="6a466-208">b.</span></span> <span data-ttu-id="6a466-209">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a466-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6a466-210">c.</span><span class="sxs-lookup"><span data-stu-id="6a466-210">c.</span></span> <span data-ttu-id="6a466-211">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="6a466-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6a466-212">d.</span><span class="sxs-lookup"><span data-stu-id="6a466-212">d.</span></span> <span data-ttu-id="6a466-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6a466-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="6a466-214">Creare un utente di test di Workstars</span><span class="sxs-lookup"><span data-stu-id="6a466-214">Create a Workstars test user</span></span>

<span data-ttu-id="6a466-215">In questa sezione viene creato un utente di nome Britta Simon in Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="6a466-216">Collaborare con il [team di supporto di Workstars](https://support.workstars.com) per aggiungere gli utenti alla piattaforma Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-216">Work with [Workstars support team](https://support.workstars.com) to add the users in the Workstars platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6a466-217">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a466-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="6a466-218">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workstars.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="6a466-220">**Per assegnare Britta Simon a Workstars, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6a466-220">**To assign Britta Simon to Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="6a466-221">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a466-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6a466-223">Nell'elenco delle applicazioni selezionare **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="6a466-223">In the applications list, select **Workstars**.</span></span>

    ![Collegamento Workstars nell'elenco delle applicazioni](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="6a466-225">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6a466-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="6a466-227">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6a466-227">Click **Add** button.</span></span> <span data-ttu-id="6a466-228">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6a466-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="6a466-230">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6a466-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a466-231">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6a466-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a466-232">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6a466-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6a466-233">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6a466-233">Test single sign-on</span></span>

<span data-ttu-id="6a466-234">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6a466-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a466-235">Quando si fa clic sul riquadro Workstars nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Workstars.</span><span class="sxs-lookup"><span data-stu-id="6a466-235">When you click the Workstars tile in the Access Panel, you should get automatically signed-on to your Workstars application.</span></span>
<span data-ttu-id="6a466-236">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a466-236">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a466-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6a466-237">Additional resources</span></span>

* [<span data-ttu-id="6a466-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a466-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a466-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a466-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

