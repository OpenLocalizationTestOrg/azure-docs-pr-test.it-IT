---
title: 'Esercitazione: Integrazione di Azure Active Directory con DocuSign | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="5d5ed-103">Esercitazione: Integrazione di Azure Active Directory con DocuSign</span><span class="sxs-lookup"><span data-stu-id="5d5ed-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="5d5ed-104">Questa esercitazione descrive come integrare DocuSign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d5ed-105">L'integrazione di DocuSign con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5d5ed-106">È possibile controllare in Azure AD chi può accedere a DocuSign</span><span class="sxs-lookup"><span data-stu-id="5d5ed-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="5d5ed-107">È possibile abilitare gli utenti per l'accesso automatico a DocuSign (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d5ed-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5d5ed-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d5ed-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d5ed-110">Prerequisites</span></span>

<span data-ttu-id="5d5ed-111">Per configurare l'integrazione di Azure AD con DocuSign, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="5d5ed-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d5ed-113">Una sottoscrizione di DocuSign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5d5ed-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d5ed-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d5ed-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d5ed-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d5ed-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d5ed-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5d5ed-118">Scenario description</span></span>
<span data-ttu-id="5d5ed-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d5ed-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d5ed-121">Aggiunta di DocuSign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5d5ed-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="5d5ed-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="5d5ed-123">Aggiunta di DocuSign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5d5ed-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="5d5ed-124">Per configurare l'integrazione di DocuSign in Azure AD, è necessario aggiungere DocuSign dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5d5ed-125">**Per aggiungere DocuSign dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5d5ed-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d5ed-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5d5ed-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5d5ed-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5d5ed-133">Nella casella di ricerca digitare **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-133">In the search box, type **DocuSign**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="5d5ed-135">Nel pannello dei risultati selezionare **DocuSign** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d5ed-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d5ed-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con DocuSign in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5d5ed-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5d5ed-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di DocuSign che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="5d5ed-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="5d5ed-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="5d5ed-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con DocuSign, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5d5ed-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5d5ed-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d5ed-145">**[Creazione di un utente test di DocuSign](#creating-a-docusign-test-user)**: per avere una controparte di Britta Simon in DocuSign collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d5ed-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d5ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d5ed-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d5ed-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="5d5ed-150">**Per configurare Single Sign-On di Azure AD con DocuSign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="5d5ed-151">Nella pagina di integrazione dell'applicazione **DocuSign** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5d5ed-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="5d5ed-155">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="5d5ed-157">Nella sezione **Configurazione DocuSign** del portale di Azure, fare clic su **Configura DocuSign** per aprire la finestra Configura accesso.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="5d5ed-158">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="5d5ed-160">In un'altra finestra del Web browser accedere al **portale di amministrazione di DocuSign** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="5d5ed-161">Nel menu di navigazione a sinistra fare clic su **Domains**(Domini).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][51]

7. <span data-ttu-id="5d5ed-163">Nel riquadro di destra fare clic su **Richiedi dominio**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][52]

8. <span data-ttu-id="5d5ed-165">Nella finestra di dialogo **Richiedi dominio** digitare il dominio aziendale nella casella di testo **Nome di dominio** e quindi fare clic su **Richiedi**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="5d5ed-166">Verificare il dominio e che lo stato sia attivo.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][53]

9. <span data-ttu-id="5d5ed-168">Nel riquadro di spostamento a sinistra fare clic su **Identity Providers**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configurazione dell'accesso Single Sign-On][54]
10. <span data-ttu-id="5d5ed-170">Nel riquadro destro fare clic sul pulsante **Add Identity Provider**(Aggiungi provider di identità).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configurazione dell'accesso Single Sign-On][55]

11. <span data-ttu-id="5d5ed-172">Nella pagina **Identity Provider Settings** (Impostazioni provider di identità) eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][56]

    <span data-ttu-id="5d5ed-174">a.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-174">a.</span></span> <span data-ttu-id="5d5ed-175">Nella casella di testo **Name** (Nome) digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="5d5ed-176">Non usare spazi.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-176">Do not use spaces.</span></span>

    <span data-ttu-id="5d5ed-177">b.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-177">b.</span></span> <span data-ttu-id="5d5ed-178">Incollare l'**ID entità SAML** nella casella dell'**autorità di certificazione del provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="5d5ed-179">c.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-179">c.</span></span> <span data-ttu-id="5d5ed-180">Incollare l'**URL del servizio Single Sign-On SAML** nella casella dell'**URL di accesso del provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="5d5ed-181">d.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-181">d.</span></span> <span data-ttu-id="5d5ed-182">Incollare l'**URL di accesso** nella casella dell'**URL di disconnessione del provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="5d5ed-183">e.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-183">e.</span></span> <span data-ttu-id="5d5ed-184">Selezionare **Sign AuthN Request**(Firma richiesta di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="5d5ed-185">f.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-185">f.</span></span> <span data-ttu-id="5d5ed-186">Per **Invia richiesta di autenticazione da** selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="5d5ed-187">g.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-187">g.</span></span> <span data-ttu-id="5d5ed-188">Per **Invia richiesta di disconnessione da** selezionare **GET**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="5d5ed-189">Nella sezione **Custom Attribute Mapping** (Mapping attributi personalizzati) scegliere il campo da associare all'attestazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="5d5ed-190">In questo esempio, viene eseguito il mapping dell'attestazione **emailaddress** con il valore di **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="5d5ed-191">Si tratta del nome di attestazione predefinito di Azure AD per l'attestazione basata su posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="5d5ed-192">Usare l' **Identificatore utente** appropriato per associare l'utente da Azure AD al mapping degli utenti di DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="5d5ed-193">Selezionare il campo corretto e immettere il valore appropriato in base alle impostazioni dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Configurazione dell'accesso Single Sign-On][57]

13. <span data-ttu-id="5d5ed-195">Nella sezione **Certificato provider di identità** fare clic su **Aggiungi certificato** e quindi caricare il certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configurazione dell'accesso Single Sign-On][58]

14. <span data-ttu-id="5d5ed-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-197">Click **Save**.</span></span>

15. <span data-ttu-id="5d5ed-198">Nella sezione **Provider di identità** fare clic su **Azioni** e quindi su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configurazione dell'accesso Single Sign-On][59]
 
16. <span data-ttu-id="5d5ed-200">Nella sezione **View SAML 2.0 Endpoints** (Visualizza endpoint SAML 2.0) del **portale di amministrazione di DocuSign** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][60]
   
    <span data-ttu-id="5d5ed-202">a.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-202">a.</span></span> <span data-ttu-id="5d5ed-203">Copiare l'**URL dell'autorità di certificazione del provider di servizi**e incollarlo nella casella di testo **Identificatore** della sezione **URL e dominio DocuSign** del portale di Azure usando questo modello: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="5d5ed-204">b.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-204">b.</span></span> <span data-ttu-id="5d5ed-205">Copiare l'**URL di accesso del provider di servizi**e incollarlo nella casella di testo **URL di accesso** della sezione **URL e dominio DocuSign** del portale di Azure usando questo modello: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="5d5ed-207">c.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-207">c.</span></span>  <span data-ttu-id="5d5ed-208">Fare clic su **Close**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-208">Click **Close**</span></span>
    
17. <span data-ttu-id="5d5ed-209">Nel portale di Azure fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-209">On the Azure portal, click **Save**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="5d5ed-211">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5d5ed-212">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5d5ed-213">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d5ed-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d5ed-215">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5d5ed-217">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5d5ed-218">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d5ed-220">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d5ed-222">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d5ed-224">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5d5ed-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d5ed-226">a.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-226">a.</span></span> <span data-ttu-id="5d5ed-227">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d5ed-228">b.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-228">b.</span></span> <span data-ttu-id="5d5ed-229">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d5ed-230">c.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-230">c.</span></span> <span data-ttu-id="5d5ed-231">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5d5ed-232">d.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-232">d.</span></span> <span data-ttu-id="5d5ed-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="5d5ed-234">Creazione di un utente test di DocuSign</span><span class="sxs-lookup"><span data-stu-id="5d5ed-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="5d5ed-235">L'applicazione supporta il **provisioning dell'utente just-in-time** e dopo l'autenticazione gli utenti vengono automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5d5ed-236">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d5ed-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5d5ed-237">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5d5ed-239">**Per assegnare Britta Simon a DocuSign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5d5ed-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="5d5ed-240">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5d5ed-242">Nell'elenco di applicazioni selezionare **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-242">In the applications list, select **DocuSign**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="5d5ed-244">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5d5ed-246">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-246">Click **Add** button.</span></span> <span data-ttu-id="5d5ed-247">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5d5ed-249">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5d5ed-250">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d5ed-251">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d5ed-252">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5d5ed-252">Testing single sign-on</span></span>

<span data-ttu-id="5d5ed-253">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5d5ed-254">Quando si fa clic sul riquadro DocuSign nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione DocuSign.</span><span class="sxs-lookup"><span data-stu-id="5d5ed-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="5d5ed-255">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d5ed-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5d5ed-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5d5ed-256">Additional resources</span></span>

* [<span data-ttu-id="5d5ed-257">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d5ed-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d5ed-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d5ed-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5d5ed-259">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="5d5ed-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

