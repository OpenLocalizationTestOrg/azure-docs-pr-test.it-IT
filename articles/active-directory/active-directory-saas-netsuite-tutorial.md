---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="cc247-103">Esercitazione: Integrazione di Azure Active Directory con NetSuite</span><span class="sxs-lookup"><span data-stu-id="cc247-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="cc247-104">Questa esercitazione descrive come integrare Netsuite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc247-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc247-105">L'integrazione di Netsuite con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc247-106">È possibile controllare in Azure AD chi può accedere a Netsuite</span><span class="sxs-lookup"><span data-stu-id="cc247-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="cc247-107">È possibile abilitare gli utenti per l'accesso automatico a Netsuite (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc247-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc247-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc247-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc247-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc247-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc247-110">Prerequisites</span></span>

<span data-ttu-id="cc247-111">Per configurare l'integrazione di Azure AD con Netsuite, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="cc247-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc247-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc247-113">Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc247-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc247-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cc247-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc247-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc247-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cc247-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc247-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc247-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc247-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cc247-118">Scenario description</span></span>
<span data-ttu-id="cc247-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cc247-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc247-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc247-121">Aggiunta di Netsuite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cc247-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="cc247-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="cc247-123">Aggiunta di Netsuite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cc247-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="cc247-124">Per configurare l'integrazione di Netsuite in Azure AD, è necessario aggiungere Netsuite dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cc247-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc247-125">**Per aggiungere Netsuite dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc247-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc247-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cc247-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc247-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cc247-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc247-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc247-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cc247-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cc247-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cc247-133">Nella casella di ricerca digitare **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="cc247-133">In the search box, type **Netsuite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="cc247-135">Nel pannello dei risultati selezionare **Netsuite** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc247-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc247-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc247-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Netsuite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc247-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc247-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Netsuite corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc247-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="cc247-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="cc247-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="cc247-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Netsuite, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc247-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cc247-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cc247-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc247-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc247-145">**[Creazione di un utente test di Netsuite](#creating-a-netsuite-test-user)**: per avere una controparte di Britta Simon in Netsuite collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cc247-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc247-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc247-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc247-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="cc247-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc247-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc247-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="cc247-150">**Per configurare l'accesso Single Sign-On di Azure AD con Netsuite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc247-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="cc247-151">Nella pagina di integrazione dell'applicazione **Netsuite** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cc247-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cc247-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cc247-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="cc247-155">Nella sezione **URL e dominio Netsuite** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cc247-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="cc247-157">Nella casella di testo **URL di risposta** digitare un URL usando il modello seguente: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="cc247-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc247-158">Poiché il valore non è reale,</span><span class="sxs-lookup"><span data-stu-id="cc247-158">This value is not real value.</span></span> <span data-ttu-id="cc247-159">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="cc247-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="cc247-160">Per ottenere il valore, contattare il [team di supporto di Netsuite](http://www.netsuite.com/portal/services/support.shtml).</span><span class="sxs-lookup"><span data-stu-id="cc247-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="cc247-161">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="cc247-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="cc247-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cc247-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc247-165">Nella sezione **Configurazione di Netsuite** fare clic su **Configura Netsuite** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="cc247-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cc247-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="cc247-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="cc247-168">Aprire una nuova scheda nel browser e accedere al sito della società Netsuite come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cc247-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="cc247-169">Sulla barra degli strumenti nella parte superiore della pagina fare clic su **Setup** (Configurazione) e quindi su **Setup Manager** (Configura gestore).</span><span class="sxs-lookup"><span data-stu-id="cc247-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="cc247-171">Dall'elenco **Setup Tasks** (Configura attività) selezionare **Integration** (Integrazione).</span><span class="sxs-lookup"><span data-stu-id="cc247-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="cc247-173">Nella sezione **Manage Authentication** (Gestione autenticazione) fare clic su **SAML Single Sign-on** (Single Sign-on di SAML).</span><span class="sxs-lookup"><span data-stu-id="cc247-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="cc247-175">Nella pagina **SAML Setup** eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc247-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="cc247-176">a.</span><span class="sxs-lookup"><span data-stu-id="cc247-176">a.</span></span> <span data-ttu-id="cc247-177">Copiare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) dalla sezione di **Quick Reference** (Riferimento rapido) di **Configure sign-on** (Configura accesso) e incollarlo nel campo **Identity Provider Login Page** (Pagina di accesso provider di identità) in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="cc247-179">b.</span><span class="sxs-lookup"><span data-stu-id="cc247-179">b.</span></span> <span data-ttu-id="cc247-180">In NetSuite selezionare **Primary Authentication Method** (Metodo di autenticazione primario).</span><span class="sxs-lookup"><span data-stu-id="cc247-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="cc247-181">c.</span><span class="sxs-lookup"><span data-stu-id="cc247-181">c.</span></span> <span data-ttu-id="cc247-182">Per il campo con etichetta **SAMLV2 Identity Provider Metadata** (Metadati provider identità SAMLV2) selezionare **Upload IDP Metadata File** (Carica file di metadati IDP).</span><span class="sxs-lookup"><span data-stu-id="cc247-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="cc247-183">Fare quindi clic su **Browse** (Sfoglia) per caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc247-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="cc247-185">d.</span><span class="sxs-lookup"><span data-stu-id="cc247-185">d.</span></span> <span data-ttu-id="cc247-186">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="cc247-186">Click **Submit**.</span></span>

12. <span data-ttu-id="cc247-187">In Azure AD fare clic sulla casella di controllo **Visualizza e modifica tutti gli altri attributi utente** e aggiungere l'attributo.</span><span class="sxs-lookup"><span data-stu-id="cc247-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="cc247-189">Nel campo **Nome attributo** immettere `account`.</span><span class="sxs-lookup"><span data-stu-id="cc247-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="cc247-190">Per il campo **Valore attributo** digitare l'ID account Netsuite. Questo valore è costante e cambia in base all'account.</span><span class="sxs-lookup"><span data-stu-id="cc247-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="cc247-191">Per istruzioni su come individuare l'ID dell'account, vedere di seguito:</span><span class="sxs-lookup"><span data-stu-id="cc247-191">Instructions on how to find your account ID are included below:</span></span>

      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="cc247-193">a.</span><span class="sxs-lookup"><span data-stu-id="cc247-193">a.</span></span> <span data-ttu-id="cc247-194">In Netsuite fare clic su **Setup** (Configurazione) nel menu di spostamento superiore.</span><span class="sxs-lookup"><span data-stu-id="cc247-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="cc247-195">b.</span><span class="sxs-lookup"><span data-stu-id="cc247-195">b.</span></span> <span data-ttu-id="cc247-196">Fare quindi clic sulla sezione **Setup Tasks** (Configura attività) del menu di spostamento sinistro, selezionare la sezione **Integration** (Integrazione), quindi fare clic su **Web Services Preferences** (Preferenze servizi Web).</span><span class="sxs-lookup"><span data-stu-id="cc247-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="cc247-197">c.</span><span class="sxs-lookup"><span data-stu-id="cc247-197">c.</span></span> <span data-ttu-id="cc247-198">Copiare l'ID dell'account NetSuite e incollarlo nel campo **Valore attributo** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc247-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="cc247-200">Per consentire l'accesso Single Sign-On a NetSuite, è prima di tutto necessario che agli utenti vengano assegnate le autorizzazioni appropriate in NetSuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="cc247-201">Per assegnare le autorizzazioni, seguire le istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc247-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="cc247-202">a.</span><span class="sxs-lookup"><span data-stu-id="cc247-202">a.</span></span> <span data-ttu-id="cc247-203">Scegliere **Setup** (Configurazione) dal menu di navigazione principale, quindi fare clic su **Setup Manager** (Configura gestore).</span><span class="sxs-lookup"><span data-stu-id="cc247-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="cc247-205">b.</span><span class="sxs-lookup"><span data-stu-id="cc247-205">b.</span></span> <span data-ttu-id="cc247-206">Scegliere **Users/Roles** (Utenti/Ruoli) dal menu di navigazione a sinistra, quindi fare clic su **Manage Roles** (Gestisci ruoli).</span><span class="sxs-lookup"><span data-stu-id="cc247-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="cc247-208">c.</span><span class="sxs-lookup"><span data-stu-id="cc247-208">c.</span></span> <span data-ttu-id="cc247-209">Fare clic su **New Role**.</span><span class="sxs-lookup"><span data-stu-id="cc247-209">Click **New Role**.</span></span>

    <span data-ttu-id="cc247-210">d.</span><span class="sxs-lookup"><span data-stu-id="cc247-210">d.</span></span> <span data-ttu-id="cc247-211">Digitare un nome per il nuovo ruolo in **Name** e selezionare la casella di controllo **Single Sign-On Only** (Solo Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="cc247-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="cc247-213">e.</span><span class="sxs-lookup"><span data-stu-id="cc247-213">e.</span></span> <span data-ttu-id="cc247-214">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cc247-214">Click **Save**.</span></span>

    <span data-ttu-id="cc247-215">f.</span><span class="sxs-lookup"><span data-stu-id="cc247-215">f.</span></span> <span data-ttu-id="cc247-216">Scegliere **Permissions**dal menu disponibile nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="cc247-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="cc247-217">Fare quindi clic su **Setup**.</span><span class="sxs-lookup"><span data-stu-id="cc247-217">Then click **Setup**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="cc247-219">g.</span><span class="sxs-lookup"><span data-stu-id="cc247-219">g.</span></span> <span data-ttu-id="cc247-220">Selezionare **Set Up SAM Single Sign-on** (Configura Single Sign-on SAM), quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cc247-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="cc247-221">h.</span><span class="sxs-lookup"><span data-stu-id="cc247-221">h.</span></span> <span data-ttu-id="cc247-222">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cc247-222">Click **Save**.</span></span>

    <span data-ttu-id="cc247-223">i.</span><span class="sxs-lookup"><span data-stu-id="cc247-223">i.</span></span> <span data-ttu-id="cc247-224">Scegliere **Setup** (Configurazione) dal menu di navigazione principale, quindi fare clic su **Setup Manager** (Configura gestore).</span><span class="sxs-lookup"><span data-stu-id="cc247-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="cc247-226">j.</span><span class="sxs-lookup"><span data-stu-id="cc247-226">j.</span></span> <span data-ttu-id="cc247-227">Scegliere **Users/Roles** (Utenti/Ruoli) dal menu di navigazione a sinistra, quindi fare clic su **Manage Users** (Gestisci utenti).</span><span class="sxs-lookup"><span data-stu-id="cc247-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="cc247-229">k.</span><span class="sxs-lookup"><span data-stu-id="cc247-229">k.</span></span> <span data-ttu-id="cc247-230">Selezionare un utente di test.</span><span class="sxs-lookup"><span data-stu-id="cc247-230">Select a test user.</span></span> <span data-ttu-id="cc247-231">Fare quindi clic su **Edit**.</span><span class="sxs-lookup"><span data-stu-id="cc247-231">Then click **Edit**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="cc247-233">l.</span><span class="sxs-lookup"><span data-stu-id="cc247-233">l.</span></span> <span data-ttu-id="cc247-234">Nella finestra di dialogo Roles selezionare il ruolo creato e quindi fare clic su **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc247-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="cc247-236">m.</span><span class="sxs-lookup"><span data-stu-id="cc247-236">m.</span></span> <span data-ttu-id="cc247-237">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cc247-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="cc247-238">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="cc247-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc247-239">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="cc247-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc247-240">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc247-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc247-241">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc247-242">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc247-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cc247-244">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc247-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc247-245">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cc247-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="cc247-247">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="cc247-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc247-249">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="cc247-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc247-251">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cc247-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc247-253">a.</span><span class="sxs-lookup"><span data-stu-id="cc247-253">a.</span></span> <span data-ttu-id="cc247-254">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc247-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc247-255">b.</span><span class="sxs-lookup"><span data-stu-id="cc247-255">b.</span></span> <span data-ttu-id="cc247-256">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc247-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc247-257">c.</span><span class="sxs-lookup"><span data-stu-id="cc247-257">c.</span></span> <span data-ttu-id="cc247-258">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc247-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc247-259">d.</span><span class="sxs-lookup"><span data-stu-id="cc247-259">d.</span></span> <span data-ttu-id="cc247-260">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cc247-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="cc247-261">Creazione di un utente test di Netsuite</span><span class="sxs-lookup"><span data-stu-id="cc247-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="cc247-262">In questa sezione si crea un utente di nome Britta Simon in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="cc247-263">Netsuite supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cc247-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="cc247-264">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="cc247-264">There is no action item for you in this section.</span></span> <span data-ttu-id="cc247-265">Se un utente non esiste in Netsuite, ne viene creato uno nuovo quando si tenta di accedere a Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc247-266">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc247-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc247-267">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Netsuite.</span><span class="sxs-lookup"><span data-stu-id="cc247-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cc247-269">**Per assegnare Britta Simon a Netsuite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc247-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="cc247-270">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc247-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cc247-272">Nell'elenco di applicazioni selezionare **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="cc247-272">In the applications list, select **Netsuite**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="cc247-274">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="cc247-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cc247-276">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cc247-276">Click **Add** button.</span></span> <span data-ttu-id="cc247-277">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc247-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cc247-279">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="cc247-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cc247-280">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc247-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc247-281">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc247-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc247-282">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc247-282">Testing single sign-on</span></span>

<span data-ttu-id="cc247-283">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cc247-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc247-284">Per testare le impostazioni dell'accesso Single Sign-On, aprire il pannello di accesso all'indirizzo [https://myapps.microsoft.com](https://myapps.microsoft.com/), quindi accedere all'account di test e fare clic su **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="cc247-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc247-285">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cc247-285">Additional resources</span></span>

* [<span data-ttu-id="cc247-286">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc247-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc247-287">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc247-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cc247-288">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="cc247-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

