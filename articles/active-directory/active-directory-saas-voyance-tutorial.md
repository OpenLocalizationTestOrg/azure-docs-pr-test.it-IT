---
title: 'Esercitazione: Integrazione di Azure Active Directory con Voyance | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="d6601-103">Esercitazione: integrazione di Azure Active Directory con Voyance</span><span class="sxs-lookup"><span data-stu-id="d6601-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="d6601-104">Questa esercitazione descrive come integrare Voyance con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6601-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6601-105">L'integrazione di Voyance con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6601-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6601-106">È possibile controllare in Azure AD chi può accedere a Voyance</span><span class="sxs-lookup"><span data-stu-id="d6601-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="d6601-107">È possibile abilitare gli utenti per l'accesso automatico a Voyance (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6601-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6601-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6601-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6601-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6601-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6601-110">Prerequisites</span></span>

<span data-ttu-id="d6601-111">Per configurare l'integrazione di Azure AD con Voyance, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6601-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="d6601-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6601-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6601-113">Sottoscrizione di Voyance abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6601-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6601-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d6601-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6601-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6601-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6601-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d6601-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6601-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6601-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6601-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d6601-118">Scenario description</span></span>
<span data-ttu-id="d6601-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d6601-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6601-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6601-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6601-121">Aggiunta di Voyance dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d6601-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="d6601-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="d6601-123">Aggiunta di Voyance dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d6601-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="d6601-124">Per configurare l'integrazione di Voyance in Azure AD, è necessario aggiungere Voyance dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d6601-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6601-125">**Per aggiungere Voyance dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6601-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6601-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d6601-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="d6601-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d6601-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6601-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6601-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="d6601-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6601-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="d6601-133">Nella casella di ricerca digitare **Voyance**, selezionare **Voyance** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6601-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance nell'elenco risultati](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d6601-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d6601-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Voyance in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6601-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6601-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Voyance che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6601-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="d6601-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Voyance.</span><span class="sxs-lookup"><span data-stu-id="d6601-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="d6601-139">Per stabilire la relazione di collegamento, in Voyance assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d6601-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6601-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Voyance, è necessario completare le operazioni fondamentali seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6601-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6601-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d6601-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6601-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6601-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6601-143">**[Creare un utente di test di Voyance](#create-a-voyance-test-user)**: per avere una controparte di Britta Simon in Voyance collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6601-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6601-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6601-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6601-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d6601-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d6601-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d6601-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Voyance.</span><span class="sxs-lookup"><span data-stu-id="d6601-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="d6601-148">**Per configurare l'accesso Single Sign-On di Azure AD con Voyance, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6601-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="d6601-149">Nella pagina di integrazione dell'applicazione **Voyance** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d6601-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d6601-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d6601-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="d6601-153">Nella sezione **URL e dominio Voyance** seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="d6601-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Voyance per IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="d6601-155">a.</span><span class="sxs-lookup"><span data-stu-id="d6601-155">a.</span></span> <span data-ttu-id="d6601-156">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="d6601-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="d6601-157">b.</span><span class="sxs-lookup"><span data-stu-id="d6601-157">b.</span></span> <span data-ttu-id="d6601-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="d6601-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="d6601-159">Selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="d6601-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Voyance per SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="d6601-161">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.nyansa.com/`.</span><span class="sxs-lookup"><span data-stu-id="d6601-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d6601-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d6601-162">These values are not real.</span></span> <span data-ttu-id="d6601-163">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d6601-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d6601-164">Per ottenere questi valori, contattare il [team di supporto clienti di Voyance](mailto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="d6601-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="d6601-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d6601-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="d6601-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d6601-167">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d6601-169">Nella sezione **Configurazione di Voyance** fare clic su **Configura Voyance** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d6601-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d6601-170">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d6601-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="d6601-172">In un'altra finestra del browser Web accedere al tenant Voyance come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d6601-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="d6601-173">Passare all'angolo superiore destro della barra di spostamento e fare clic nell'elenco a discesa "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="d6601-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Configurare l'accesso Single Sign-On sul lato app - Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="d6601-175">Fare clic su "**Admin Settings**" (Impostazioni amministrazione).</span><span class="sxs-lookup"><span data-stu-id="d6601-175">Click "**Admin Settings**".</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Impostazioni di amministrazione](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="d6601-177">Fare clic sulla scheda "**User Access**" (Accesso utente).</span><span class="sxs-lookup"><span data-stu-id="d6601-177">Click "**User Access**" tab.</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Accesso utente](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="d6601-179">Fare clic sul pulsante "**SSO is disabled**" (SSO disabilitato) per configurare Azure AD come IdP tramite SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="d6601-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Pulsante che indica che l'accesso SSO è disabilitato](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="d6601-181">Passare alla sezione **SAML v2** e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d6601-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="d6601-183">a.</span><span class="sxs-lookup"><span data-stu-id="d6601-183">a.</span></span> <span data-ttu-id="d6601-184">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="d6601-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="d6601-185">b.</span><span class="sxs-lookup"><span data-stu-id="d6601-185">b.</span></span> <span data-ttu-id="d6601-186">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo**IdP Login URL** (URL di accesso IdP).</span><span class="sxs-lookup"><span data-stu-id="d6601-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="d6601-187">c.</span><span class="sxs-lookup"><span data-stu-id="d6601-187">c.</span></span> <span data-ttu-id="d6601-188">Aprire il certificato con codifica Base64 scaricato nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **IdP Cert** (Certificato IdP).</span><span class="sxs-lookup"><span data-stu-id="d6601-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="d6601-189">d.</span><span class="sxs-lookup"><span data-stu-id="d6601-189">d.</span></span> <span data-ttu-id="d6601-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d6601-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d6601-191">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d6601-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6601-192">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d6601-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6601-193">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6601-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d6601-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-194">Create an Azure AD test user</span></span>

<span data-ttu-id="d6601-195">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6601-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="d6601-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6601-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6601-198">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d6601-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6601-200">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d6601-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6601-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d6601-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6601-204">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d6601-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6601-206">a.</span><span class="sxs-lookup"><span data-stu-id="d6601-206">a.</span></span> <span data-ttu-id="d6601-207">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6601-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6601-208">b.</span><span class="sxs-lookup"><span data-stu-id="d6601-208">b.</span></span> <span data-ttu-id="d6601-209">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6601-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6601-210">c.</span><span class="sxs-lookup"><span data-stu-id="d6601-210">c.</span></span> <span data-ttu-id="d6601-211">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d6601-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6601-212">d.</span><span class="sxs-lookup"><span data-stu-id="d6601-212">d.</span></span> <span data-ttu-id="d6601-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d6601-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="d6601-214">Creare un utente test di Voyance</span><span class="sxs-lookup"><span data-stu-id="d6601-214">Create a Voyance test user</span></span>

<span data-ttu-id="d6601-215">Questa sezione descrive come creare un utente chiamato Britta Simon in Voyance.</span><span class="sxs-lookup"><span data-stu-id="d6601-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="d6601-216">Voyance supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d6601-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d6601-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d6601-217">There is no action item for you in this section.</span></span> <span data-ttu-id="d6601-218">Durante il tentativo di accesso a Voyance viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="d6601-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d6601-219">Per creare un utente manualmente, contattare il [team di supporto di Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="d6601-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d6601-220">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6601-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="d6601-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Voyance.</span><span class="sxs-lookup"><span data-stu-id="d6601-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="d6601-223">**Per assegnare Britta Simon a Voyance, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6601-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="d6601-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6601-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d6601-226">Nell'elenco di applicazioni selezionare **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="d6601-226">In the applications list, select **Voyance**.</span></span>

    ![Collegamento di Voyance nell'elenco delle applicazioni](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="d6601-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d6601-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="d6601-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d6601-230">Click **Add** button.</span></span> <span data-ttu-id="d6601-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6601-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="d6601-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d6601-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6601-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d6601-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6601-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6601-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d6601-236">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6601-236">Test single sign-on</span></span>

<span data-ttu-id="d6601-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d6601-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6601-238">Quando si fa clic sul riquadro Voyance nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Voyance.</span><span class="sxs-lookup"><span data-stu-id="d6601-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6601-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d6601-239">Additional resources</span></span>

* [<span data-ttu-id="d6601-240">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6601-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6601-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6601-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

