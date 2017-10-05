---
title: 'Esercitazione: integrazione di Azure Active Directory con LCVista | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LCVista.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="0d854-103">Esercitazione: integrazione di Azure Active Directory con LCVista</span><span class="sxs-lookup"><span data-stu-id="0d854-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="0d854-104">Questa esercitazione descrive come integrare LCVista con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d854-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d854-105">L'integrazione di LCVista con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d854-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d854-106">È possibile controllare in Azure AD chi può accedere a LCVista</span><span class="sxs-lookup"><span data-stu-id="0d854-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="0d854-107">È possibile abilitare gli utenti per l'accesso automatico ad LCVista (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d854-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d854-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0d854-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d854-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d854-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d854-110">Prerequisites</span></span>

<span data-ttu-id="0d854-111">Per configurare l'integrazione di Azure AD con LCVista, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d854-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="0d854-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d854-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d854-113">Sottoscrizione di LCVista abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0d854-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d854-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d854-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d854-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d854-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d854-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0d854-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d854-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d854-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d854-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0d854-118">Scenario description</span></span>
<span data-ttu-id="0d854-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0d854-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d854-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d854-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d854-121">Aggiunta di LCVista dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0d854-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="0d854-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="0d854-123">Aggiunta di LCVista dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0d854-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="0d854-124">Per configurare l'integrazione di LCVista in Azure AD, è necessario aggiungere LCVista dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0d854-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d854-125">**Per aggiungere LCVista dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0d854-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d854-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0d854-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d854-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0d854-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d854-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d854-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0d854-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d854-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0d854-133">Nella casella di ricerca digitare **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="0d854-133">In the search box, type **LCVista**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="0d854-135">Nel pannello dei risultati selezionare **LCVista** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d854-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d854-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d854-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LCVista in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d854-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0d854-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di LCVista che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d854-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="0d854-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="0d854-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Nome utente** in LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="0d854-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con LCVista, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d854-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d854-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0d854-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d854-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d854-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d854-145">**[Creazione di un utente test di LCVista](#creating-a-lcvista-test-user)**: per avere una controparte di Britta Simon in LCVista collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0d854-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d854-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d854-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d854-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0d854-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d854-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d854-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="0d854-150">**Per configurare Single Sign-On di Azure AD con LCVista, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0d854-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="0d854-151">Nella pagina di integrazione dell'applicazione **LCVista** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0d854-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0d854-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0d854-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="0d854-155">Nella sezione **URL e dominio LCVista** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0d854-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="0d854-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d854-157">a.</span></span> <span data-ttu-id="0d854-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.lcvista.com/rainier/login`.</span><span class="sxs-lookup"><span data-stu-id="0d854-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="0d854-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d854-159">b.</span></span> <span data-ttu-id="0d854-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="0d854-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="0d854-161">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="0d854-161">These values are not the real.</span></span> <span data-ttu-id="0d854-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0d854-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="0d854-163">Per ottenere questi valori, contattare il [team di supporto clienti di LCVista](https://lcvista.com/contact).</span><span class="sxs-lookup"><span data-stu-id="0d854-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="0d854-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="0d854-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="0d854-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0d854-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0d854-168">Nella sezione **Configurazione di LCVista** fare clic su **Configura LCVista** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="0d854-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d854-169">Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="0d854-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="0d854-171">Accedere all'applicazione LCVista come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0d854-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="0d854-172">Nella sezione **Configurazione SAML** selezionare **Enable SAML login** (Abilita accesso SAML) e immettere i dettagli, come indicato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="0d854-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="0d854-174">a.</span><span class="sxs-lookup"><span data-stu-id="0d854-174">a.</span></span> <span data-ttu-id="0d854-175">Incollare l'**URL autorità di certificazione** che è stata copiata da Azure AD nella sezione **ID entità**.</span><span class="sxs-lookup"><span data-stu-id="0d854-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="0d854-176">b.</span><span class="sxs-lookup"><span data-stu-id="0d854-176">b.</span></span> <span data-ttu-id="0d854-177">Incollare l'**URL servizio Single Sign-On** che è stata copiata da Azure AD nella sezione **URL**.</span><span class="sxs-lookup"><span data-stu-id="0d854-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="0d854-178">c.</span><span class="sxs-lookup"><span data-stu-id="0d854-178">c.</span></span> <span data-ttu-id="0d854-179">Da Metadati (XML) che è stato scaricato dal portale di Azure, copiare il valore **X509Certificate** e incollarlo nella sezione **Certificato x509**.</span><span class="sxs-lookup"><span data-stu-id="0d854-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="0d854-180">d.</span><span class="sxs-lookup"><span data-stu-id="0d854-180">d.</span></span> <span data-ttu-id="0d854-181">Nella casella di testo **Attributo nome** incollare il valore `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="0d854-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="0d854-182">e.</span><span class="sxs-lookup"><span data-stu-id="0d854-182">e.</span></span> <span data-ttu-id="0d854-183">Nella casella di testo **Attributo cognome** incollare il valore `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="0d854-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="0d854-184">f.</span><span class="sxs-lookup"><span data-stu-id="0d854-184">f.</span></span> <span data-ttu-id="0d854-185">Nella casella di testo **Attributo posta elettronica** incollare il valore `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0d854-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="0d854-186">g.</span><span class="sxs-lookup"><span data-stu-id="0d854-186">g.</span></span> <span data-ttu-id="0d854-187">Nella casella di testo **Attributo nome utente** incollare il valore `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="0d854-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="0d854-188">e.</span><span class="sxs-lookup"><span data-stu-id="0d854-188">e.</span></span> <span data-ttu-id="0d854-189">Fare clic su **Salva** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0d854-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="0d854-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0d854-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0d854-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0d854-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0d854-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d854-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d854-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d854-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d854-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0d854-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0d854-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d854-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0d854-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d854-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0d854-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d854-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0d854-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d854-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0d854-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d854-205">a.</span><span class="sxs-lookup"><span data-stu-id="0d854-205">a.</span></span> <span data-ttu-id="0d854-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d854-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d854-207">b.</span><span class="sxs-lookup"><span data-stu-id="0d854-207">b.</span></span> <span data-ttu-id="0d854-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d854-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d854-209">c.</span><span class="sxs-lookup"><span data-stu-id="0d854-209">c.</span></span> <span data-ttu-id="0d854-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0d854-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0d854-211">d.</span><span class="sxs-lookup"><span data-stu-id="0d854-211">d.</span></span> <span data-ttu-id="0d854-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0d854-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="0d854-213">Creazione di un utente test LCVista</span><span class="sxs-lookup"><span data-stu-id="0d854-213">Creating a LCVista test user</span></span>

<span data-ttu-id="0d854-214">In questa sezione viene creato un utente chiamato Britta Simon in LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="0d854-215">È necessario contattare il [team di supporto LCVista Client](https://lcvista.com/contact) per aggiungere gli utenti nell'applicazione LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0d854-216">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d854-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0d854-217">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso ad LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0d854-219">**Per assegnare Britta Simon a LCVista, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0d854-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="0d854-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d854-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0d854-222">Nell'elenco di applicazioni selezionare **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="0d854-222">In the applications list, select **LCVista**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="0d854-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0d854-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0d854-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d854-226">Click **Add** button.</span></span> <span data-ttu-id="0d854-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0d854-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0d854-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0d854-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d854-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0d854-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d854-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0d854-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d854-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0d854-232">Testing single sign-on</span></span>

<span data-ttu-id="0d854-233">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0d854-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="0d854-234">Fare clic sul riquadro LCVista nel Pannello di accesso e si verrà reindirizzati alla pagina di accesso dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0d854-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="0d854-235">Dopo aver eseguito l'accesso, si verrà registrati nell'applicazione LCVista.</span><span class="sxs-lookup"><span data-stu-id="0d854-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="0d854-236">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0d854-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d854-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0d854-237">Additional resources</span></span>

* [<span data-ttu-id="0d854-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d854-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d854-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d854-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

