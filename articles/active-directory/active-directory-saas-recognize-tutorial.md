---
title: 'Esercitazione: Integrazione di Azure Active Directory con Recognize | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Recognize.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="f5065-103">Esercitazione: Integrazione di Azure Active Directory con Recognize</span><span class="sxs-lookup"><span data-stu-id="f5065-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="f5065-104">Questa esercitazione descrive come integrare Recognize con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5065-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5065-105">L'integrazione di Recognize con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5065-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5065-106">È possibile controllare in Azure AD chi può accedere a Recognize</span><span class="sxs-lookup"><span data-stu-id="f5065-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="f5065-107">È possibile abilitare gli utenti per l'accesso automatico a Recognize (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5065-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5065-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5065-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5065-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5065-110">Prerequisites</span></span>

<span data-ttu-id="f5065-111">Per configurare l'integrazione di Azure AD con Recognize, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5065-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="f5065-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5065-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5065-113">Sottoscrizione di Recognize abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5065-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5065-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5065-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5065-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5065-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5065-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f5065-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5065-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5065-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5065-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f5065-118">Scenario description</span></span>
<span data-ttu-id="f5065-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f5065-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5065-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5065-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5065-121">Aggiunta di Recognize dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5065-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="f5065-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="f5065-123">Aggiunta di Recognize dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5065-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="f5065-124">Per configurare l'integrazione di Recognize in Azure AD, è necessario aggiungere Recognize dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f5065-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5065-125">**Per aggiungere Recognize dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5065-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5065-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5065-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5065-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f5065-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5065-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5065-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f5065-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5065-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f5065-133">Nella casella di ricerca digitare **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="f5065-133">In the search box, type **Recognize**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="f5065-135">Nel pannello dei risultati selezionare **Recognize** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5065-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5065-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5065-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Recognize in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5065-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5065-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Recognize che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5065-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="f5065-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Recognize.</span><span class="sxs-lookup"><span data-stu-id="f5065-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="f5065-141">Per stabilire la relazione di collegamento, in Recognize assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="f5065-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5065-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Recognize, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5065-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5065-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f5065-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5065-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5065-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5065-145">**[Creazione di un utente di test di Recognize](#creating-a-recognize-test-user)**: per avere una controparte di Britta Simon in Recognize collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5065-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5065-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5065-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5065-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f5065-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5065-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5065-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Recognize.</span><span class="sxs-lookup"><span data-stu-id="f5065-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="f5065-150">**Per configurare Single Sign-On di Azure AD con Recognize, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5065-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="f5065-151">Nella pagina di integrazione dell'applicazione **Recognize** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f5065-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f5065-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f5065-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="f5065-155">Nella sezione **URL e dominio Recognize** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5065-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="f5065-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5065-157">a.</span></span> <span data-ttu-id="f5065-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://recognizeapp.com/<your-domain>/saml/sso`.</span><span class="sxs-lookup"><span data-stu-id="f5065-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="f5065-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5065-159">b.</span></span> <span data-ttu-id="f5065-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="f5065-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5065-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f5065-161">These values are not real.</span></span> <span data-ttu-id="f5065-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f5065-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5065-163">Contattare il [team di supporto client di Recognize ](mailto:support@recognizeapp.com) per ottenere l'URL Sign-On; è possibile ottenere il valore di identificazione aprendo l'URL metadati del provider di servizi dalla sezione delle impostazioni SSO illustrata più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5065-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="f5065-164">.</span><span class="sxs-lookup"><span data-stu-id="f5065-164">.</span></span> 
 
4. <span data-ttu-id="f5065-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f5065-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="f5065-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f5065-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5065-169">Nella sezione **Configurazione di Recognize** fare clic su **Configura Recognize** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f5065-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5065-170">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f5065-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="f5065-172">In un'altra finestra del browser Web accedere al tenant Recognize come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f5065-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="f5065-173">In alto a destra fare clic su **Menu**.</span><span class="sxs-lookup"><span data-stu-id="f5065-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="f5065-174">Passare a **Company Admin** (Amministrazione società).</span><span class="sxs-lookup"><span data-stu-id="f5065-174">Go to **Company Admin**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="f5065-176">Nella barra di spostamento a sinistra fare clic su **Settings**(Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="f5065-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="f5065-178">Nella sezione **SSO Settings** (Impostazioni SSO) seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="f5065-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="f5065-180">a.</span><span class="sxs-lookup"><span data-stu-id="f5065-180">a.</span></span> <span data-ttu-id="f5065-181">In **Enable SSO** (Abilita SSO) selezionare **ON**.</span><span class="sxs-lookup"><span data-stu-id="f5065-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="f5065-182">b.</span><span class="sxs-lookup"><span data-stu-id="f5065-182">b.</span></span> <span data-ttu-id="f5065-183">Nella casella di testo **IDP Entity ID** (ID entità IdP) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f5065-184">c.</span><span class="sxs-lookup"><span data-stu-id="f5065-184">c.</span></span> <span data-ttu-id="f5065-185">Nella casella di testo **SSO Target URL** (URL di destinazione SSO) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f5065-186">d.</span><span class="sxs-lookup"><span data-stu-id="f5065-186">d.</span></span> <span data-ttu-id="f5065-187">Nella casella di testo **SLO Target URL** (URL SLO di destinazione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="f5065-188">e.</span><span class="sxs-lookup"><span data-stu-id="f5065-188">e.</span></span> <span data-ttu-id="f5065-189">Aprire il file **Certificate (Base64)** scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato**.</span><span class="sxs-lookup"><span data-stu-id="f5065-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="f5065-190">f.</span><span class="sxs-lookup"><span data-stu-id="f5065-190">f.</span></span> <span data-ttu-id="f5065-191">Fare clic sul pulsante **Save settings** (Salva impostazioni).</span><span class="sxs-lookup"><span data-stu-id="f5065-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="f5065-192">Accanto alla sezione **SSO Settings** (Impostazioni Single Sign-On) copiare l'URL in **Service Provider Metadata url** (URL metadati del provider di servizio).</span><span class="sxs-lookup"><span data-stu-id="f5065-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="f5065-194">In una pagina del browser fare clic sul collegamento **Metadata URL** (URL metadati) per scaricare il documento di metadati.</span><span class="sxs-lookup"><span data-stu-id="f5065-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="f5065-195">Quindi copiare il valore EntityDescriptor (entityID) dal file e incollarlo nella casella di testo **Identificatore** nella sezione **URL e dominio Recognize** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="f5065-197">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f5065-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5065-198">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f5065-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5065-199">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5065-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5065-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5065-201">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5065-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f5065-203">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5065-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5065-204">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5065-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5065-206">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f5065-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5065-208">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f5065-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5065-210">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5065-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5065-212">a.</span><span class="sxs-lookup"><span data-stu-id="f5065-212">a.</span></span> <span data-ttu-id="f5065-213">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5065-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5065-214">b.</span><span class="sxs-lookup"><span data-stu-id="f5065-214">b.</span></span> <span data-ttu-id="f5065-215">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5065-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5065-216">c.</span><span class="sxs-lookup"><span data-stu-id="f5065-216">c.</span></span> <span data-ttu-id="f5065-217">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f5065-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5065-218">d.</span><span class="sxs-lookup"><span data-stu-id="f5065-218">d.</span></span> <span data-ttu-id="f5065-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f5065-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="f5065-220">Creazione di un utente test di Recognize</span><span class="sxs-lookup"><span data-stu-id="f5065-220">Creating a Recognize test user</span></span>

<span data-ttu-id="f5065-221">Per consentire agli utenti di Azure AD di accedere a Recognize, è necessario eseguirne il provisioning in Recognize.</span><span class="sxs-lookup"><span data-stu-id="f5065-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="f5065-222">Nel caso di Recognize, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f5065-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="f5065-223">Questa app non supporta il provisioning SCIM, ma dispone di una sincronizzazione utente alternativa che esegue il provisioning degli utenti.</span><span class="sxs-lookup"><span data-stu-id="f5065-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="f5065-224">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5065-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f5065-225">Accedere al sito aziendale di Recognize come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f5065-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="f5065-226">In alto a destra fare clic su **Menu**.</span><span class="sxs-lookup"><span data-stu-id="f5065-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="f5065-227">Passare a **Company Admin** (Amministrazione società).</span><span class="sxs-lookup"><span data-stu-id="f5065-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="f5065-228">Nella barra di spostamento a sinistra fare clic su **Settings**(Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="f5065-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="f5065-229">Nella sezione **User Sync** (Sincronizzazione utente) seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="f5065-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="f5065-230">![Nuovo utente](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="f5065-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="f5065-231">a.</span><span class="sxs-lookup"><span data-stu-id="f5065-231">a.</span></span> <span data-ttu-id="f5065-232">In **Sync Enabled** (Sincronizzazione abilitata) selezionare **ON**.</span><span class="sxs-lookup"><span data-stu-id="f5065-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="f5065-233">b.</span><span class="sxs-lookup"><span data-stu-id="f5065-233">b.</span></span> <span data-ttu-id="f5065-234">In **Choose sync provider** (Scegli provider di sincronizzazione) selezionare **Microsoft/Office 365**.</span><span class="sxs-lookup"><span data-stu-id="f5065-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="f5065-235">c.</span><span class="sxs-lookup"><span data-stu-id="f5065-235">c.</span></span> <span data-ttu-id="f5065-236">Fare clic su **Run User Sync** (Esegui sincronizzazione utente).</span><span class="sxs-lookup"><span data-stu-id="f5065-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5065-237">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5065-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5065-238">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Recognize.</span><span class="sxs-lookup"><span data-stu-id="f5065-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f5065-240">**Per assegnare Britta Simon a Recognize, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5065-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="f5065-241">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5065-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f5065-243">Nell'elenco di applicazioni selezionare **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="f5065-243">In the applications list, select **Recognize**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="f5065-245">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f5065-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f5065-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5065-247">Click **Add** button.</span></span> <span data-ttu-id="f5065-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5065-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f5065-250">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f5065-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5065-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f5065-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5065-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5065-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5065-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5065-253">Testing single sign-on</span></span>

<span data-ttu-id="f5065-254">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f5065-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5065-255">Quando si fa clic sul riquadro Recognize nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Recognize.</span><span class="sxs-lookup"><span data-stu-id="f5065-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="f5065-256">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5065-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5065-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f5065-257">Additional resources</span></span>

* [<span data-ttu-id="f5065-258">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5065-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5065-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5065-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

