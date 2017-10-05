---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public |Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TOPdesk - Public.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="b268e-103">Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="b268e-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="b268e-104">Questa esercitazione descrive come integrare TOPdesk - Public con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b268e-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b268e-105">L'integrazione di TOPdesk - Public con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268e-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b268e-106">È possibile controllare in Azure AD chi può accedere a TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="b268e-107">È possibile abilitare gli utenti per l'accesso automatico a TOPdesk - Public (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b268e-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b268e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b268e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b268e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b268e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b268e-110">Prerequisites</span></span>

<span data-ttu-id="b268e-111">Per configurare l'integrazione di Azure AD con TOPdesk - Public, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268e-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="b268e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b268e-113">Sottoscrizione di TOPdesk - Public abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b268e-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b268e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b268e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b268e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b268e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b268e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b268e-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b268e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b268e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b268e-118">Scenario description</span></span>
<span data-ttu-id="b268e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b268e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b268e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b268e-121">Aggiunta di TOPdesk - Public dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b268e-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="b268e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b268e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="b268e-123">Aggiunta di TOPdesk - Public dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b268e-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="b268e-124">Per configurare l'integrazione di TOPdesk - Public in Azure AD, è necessario aggiungere TOPdesk - Public dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b268e-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b268e-125">**Per aggiungere TOPdesk - Public dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b268e-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b268e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b268e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="b268e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b268e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b268e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b268e-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="b268e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b268e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="b268e-133">Nella casella di ricerca digitare **TOPdesk - Public**, selezionare **TOPdesk - Public** dal pannello dei risultati quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b268e-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Public nell'elenco dei risultati](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b268e-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b268e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b268e-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TOPdesk - Public usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b268e-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b268e-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di TOPdesk - Public che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="b268e-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="b268e-139">Per stabilire la relazione di collegamento, in TOPdesk - Public assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b268e-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b268e-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con TOPdesk - Public, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268e-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b268e-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b268e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b268e-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b268e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b268e-143">**[Creare un utente di test per TOPdesk - Public](#create-a-topdesk---public-test-user)**: per avere una controparte di Britta Simon in TOPdesk - Public collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b268e-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b268e-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b268e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b268e-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b268e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b268e-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione OPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="b268e-148">**Per configurare Single Sign-On di Azure AD con TOPdesk - Public, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b268e-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="b268e-149">Nella pagina di integrazione dell'applicazione **TOPdesk - Public** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b268e-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="b268e-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b268e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="b268e-153">Nella sezione **URL e dominio TOPdesk - Public** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="b268e-155">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-155">a.</span></span> <span data-ttu-id="b268e-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.topdesk.net`.</span><span class="sxs-lookup"><span data-stu-id="b268e-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="b268e-157">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-157">b.</span></span> <span data-ttu-id="b268e-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="b268e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="b268e-159">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-159">c.</span></span> <span data-ttu-id="b268e-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="b268e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b268e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b268e-161">These values are not real.</span></span> <span data-ttu-id="b268e-162">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="b268e-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b268e-163">L'URL di risposta è descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b268e-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="b268e-164">Per ottenere questi valori, contattare il [team di supporto clienti di TOPdesk - Public](https://help.topdesk.com/saas/enterprise/user/).</span><span class="sxs-lookup"><span data-stu-id="b268e-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="b268e-165">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="b268e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="b268e-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b268e-167">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b268e-169">Nella sezione **Configurazione di TOPdesk - Public** fare clic su **Configura TOPdesk - Public** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b268e-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b268e-170">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b268e-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="b268e-172">Accedere al sito aziendale di **TOPdesk - Public** come un amministratore.</span><span class="sxs-lookup"><span data-stu-id="b268e-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="b268e-173">Nel menu **TOPdesk** fare clic su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="b268e-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="b268e-174">![Impostazioni](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="b268e-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="b268e-175">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="b268e-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="b268e-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="b268e-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="b268e-177">Espandere il menu **Login Settings** (Impostazioni accesso) e quindi fare clic su **General** (Generale).</span><span class="sxs-lookup"><span data-stu-id="b268e-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="b268e-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="b268e-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="b268e-179">Nell'area **Public** (Publico) della sezione di configurazione **SAML login** (Accesso SAML) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="b268e-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="b268e-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="b268e-181">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-181">a.</span></span> <span data-ttu-id="b268e-182">Fare clic su **Download** per scaricare il file di metadati pubblici e quindi salvarlo in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="b268e-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="b268e-183">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-183">b.</span></span> <span data-ttu-id="b268e-184">Aprire il file dei metadati scaricato e quindi individuare il nodo **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="b268e-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="b268e-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="b268e-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="b268e-186">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-186">c.</span></span> <span data-ttu-id="b268e-187">Copiare il valore **AssertionConsumerService**, incollarlo nella casella di testo **URL di risposta** nella sezione **URL e dominio TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="b268e-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="b268e-188">Per creare un file del certificato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="b268e-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="b268e-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="b268e-190">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-190">a.</span></span> <span data-ttu-id="b268e-191">Aprire il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b268e-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="b268e-192">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-192">b.</span></span> <span data-ttu-id="b268e-193">Espandere il nodo **RoleDescriptor** con **xsi:type** corrispondente a **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="b268e-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="b268e-194">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-194">c.</span></span> <span data-ttu-id="b268e-195">Copiare il valore del nodo **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="b268e-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="b268e-196">d.</span><span class="sxs-lookup"><span data-stu-id="b268e-196">d.</span></span> <span data-ttu-id="b268e-197">Salvare il valore copiato di **X509Certificate** in un file locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="b268e-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="b268e-198">Nell'area **Public** (Pubblica) fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="b268e-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="b268e-199">![Login SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Login SAML")</span><span class="sxs-lookup"><span data-stu-id="b268e-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="b268e-200">Nella pagina **SAML configuration assistant** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="b268e-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="b268e-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="b268e-202">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-202">a.</span></span> <span data-ttu-id="b268e-203">Per caricare il file di metadati scaricato dal portale di Azure, in **Metadati della federazione** fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="b268e-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="b268e-204">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-204">b.</span></span> <span data-ttu-id="b268e-205">Per caricare il file del certificato, in **Certificate (RSA)** (Certificato RSA) fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="b268e-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="b268e-206">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-206">c.</span></span> <span data-ttu-id="b268e-207">Per caricare il file del logo ottenuto dal team di supporto del team di TOPdesk, in **Logo icon** (Icona logo) fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="b268e-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="b268e-208">d.</span><span class="sxs-lookup"><span data-stu-id="b268e-208">d.</span></span> <span data-ttu-id="b268e-209">Nella casella di testo **User name attribute** (Attributo nome utente) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="b268e-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="b268e-210">e.</span><span class="sxs-lookup"><span data-stu-id="b268e-210">e.</span></span> <span data-ttu-id="b268e-211">Nella casella di testo **Display name** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b268e-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="b268e-212">f.</span><span class="sxs-lookup"><span data-stu-id="b268e-212">f.</span></span> <span data-ttu-id="b268e-213">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b268e-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b268e-214">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b268e-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b268e-215">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b268e-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b268e-216">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b268e-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b268e-217">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b268e-217">Create an Azure AD test user</span></span>

<span data-ttu-id="b268e-218">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b268e-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="b268e-220">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b268e-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b268e-221">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="b268e-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b268e-223">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b268e-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b268e-225">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b268e-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b268e-227">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-227">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b268e-229">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-229">a.</span></span> <span data-ttu-id="b268e-230">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b268e-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b268e-231">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-231">b.</span></span> <span data-ttu-id="b268e-232">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b268e-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b268e-233">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-233">c.</span></span> <span data-ttu-id="b268e-234">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="b268e-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b268e-235">d.</span><span class="sxs-lookup"><span data-stu-id="b268e-235">d.</span></span> <span data-ttu-id="b268e-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b268e-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="b268e-237">Creare un utente di test di TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="b268e-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="b268e-238">Per consentire agli utenti di Azure AD di accedere a TOPdesk - Public, è necessario eseguirne il provisioning in TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="b268e-239">Nel caso di TOPdesk - Public, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b268e-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b268e-240">Per configurare il provisioning utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="b268e-241">Accedere al sito aziendale di **TOPdesk - Public** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b268e-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="b268e-242">Nel menu presente sulla parte superiore fare clic su **TOPdesk \> New (Nuovo) \> Support Files (File di supporto) \> Person (Persona)**.</span><span class="sxs-lookup"><span data-stu-id="b268e-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="b268e-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span><span class="sxs-lookup"><span data-stu-id="b268e-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="b268e-244">Nella finestra di dialogo New Person seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b268e-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b268e-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span><span class="sxs-lookup"><span data-stu-id="b268e-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="b268e-246">a.</span><span class="sxs-lookup"><span data-stu-id="b268e-246">a.</span></span> <span data-ttu-id="b268e-247">Fare clic sulla scheda General.</span><span class="sxs-lookup"><span data-stu-id="b268e-247">Click the General tab.</span></span>

    <span data-ttu-id="b268e-248">b.</span><span class="sxs-lookup"><span data-stu-id="b268e-248">b.</span></span> <span data-ttu-id="b268e-249">Digitare il cognome dell'utente, ad esempio Simon, nella casella di testo **Surname** (Cognome)</span><span class="sxs-lookup"><span data-stu-id="b268e-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="b268e-250">c.</span><span class="sxs-lookup"><span data-stu-id="b268e-250">c.</span></span> <span data-ttu-id="b268e-251">Selezionare un **Site** per l'account.</span><span class="sxs-lookup"><span data-stu-id="b268e-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="b268e-252">d.</span><span class="sxs-lookup"><span data-stu-id="b268e-252">d.</span></span> <span data-ttu-id="b268e-253">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b268e-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="b268e-254">È possibile usare qualsiasi altro strumento o API di creazione account utente fornita da TOPdesk - Public per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b268e-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b268e-255">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b268e-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="b268e-256">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="b268e-258">**Per assegnare Britta Simon a TOPdesk - Public, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b268e-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="b268e-259">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b268e-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b268e-261">Nell'elenco delle applicazioni selezionare **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="b268e-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![Collegamento TOPdesk - Public nell'elenco delle applicazioni](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="b268e-263">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b268e-263">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="b268e-265">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b268e-265">Click **Add** button.</span></span> <span data-ttu-id="b268e-266">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b268e-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="b268e-268">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b268e-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b268e-269">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b268e-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b268e-270">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b268e-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b268e-271">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b268e-271">Test single sign-on</span></span>

<span data-ttu-id="b268e-272">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b268e-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b268e-273">Quando si fa clic sul riquadro TOPdesk - Public nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="b268e-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="b268e-274">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b268e-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b268e-275">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b268e-275">Additional resources</span></span>

* [<span data-ttu-id="b268e-276">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b268e-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b268e-277">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b268e-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

