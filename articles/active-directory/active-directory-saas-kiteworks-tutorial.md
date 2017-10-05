---
title: Esercitazione Integrazione di Azure Active Directory con Kiteworks | Microsoft Docs
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="28868-103">Esercitazione Integrazione di Azure Active Directory con Kiteworks</span><span class="sxs-lookup"><span data-stu-id="28868-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="28868-104">Questa esercitazione descrive come integrare Kiteworks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28868-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28868-105">L'integrazione di Kiteworks con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="28868-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="28868-106">È possibile controllare in Azure AD chi può accedere a Kiteworks</span><span class="sxs-lookup"><span data-stu-id="28868-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="28868-107">È possibile abilitare gli utenti per l'accesso automatico a Kiteworks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28868-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28868-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="28868-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28868-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28868-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="28868-110">Prerequisites</span></span>

<span data-ttu-id="28868-111">Per configurare l'integrazione di Azure AD con Kiteworks, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="28868-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="28868-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28868-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28868-113">Sottoscrizione di Kiteworks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="28868-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28868-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="28868-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28868-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="28868-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28868-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="28868-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28868-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28868-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28868-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="28868-118">Scenario description</span></span>
<span data-ttu-id="28868-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="28868-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28868-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="28868-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28868-121">Aggiunta di Kiteworks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="28868-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="28868-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="28868-123">Aggiunta di Kiteworks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="28868-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="28868-124">Per configurare l'integrazione di Kiteworks in Azure AD, è necessario aggiungere Kiteworks dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="28868-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28868-125">**Per aggiungere Kiteworks dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="28868-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28868-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="28868-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28868-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="28868-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="28868-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="28868-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="28868-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="28868-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="28868-133">Nella casella di ricerca digitare **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="28868-133">In the search box, type **Kiteworks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="28868-135">Nel pannello dei risultati selezionare **Kiteworks** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="28868-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28868-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28868-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kiteworks mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28868-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28868-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Kiteworks corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28868-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="28868-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="28868-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="28868-141">Per stabilire la relazione di collegamento, in Kiteworks assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="28868-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="28868-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Kiteworks, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="28868-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28868-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="28868-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28868-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28868-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28868-145">**[Creazione di un utente test di Kiteworks](#creating-a-kiteworks-test-user)**: per avere una controparte di Britta Simon in Kiteworks collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28868-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="28868-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28868-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28868-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="28868-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28868-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28868-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="28868-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="28868-150">**Per configurare l'accesso Single Sign-On di Azure AD con Kiteworks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="28868-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="28868-151">Nella pagina di integrazione dell'applicazione **Kiteworks** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="28868-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="28868-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="28868-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="28868-155">Nella sezione **URL e dominio Kiteworks** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="28868-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="28868-157">a.</span><span class="sxs-lookup"><span data-stu-id="28868-157">a.</span></span> <span data-ttu-id="28868-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.kiteworks.com`.</span><span class="sxs-lookup"><span data-stu-id="28868-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="28868-159">b.</span><span class="sxs-lookup"><span data-stu-id="28868-159">b.</span></span> <span data-ttu-id="28868-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="28868-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28868-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="28868-161">These values are not real.</span></span> <span data-ttu-id="28868-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="28868-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="28868-163">Per ottenere questi valori contattare il [team di supporto clienti di Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="28868-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="28868-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="28868-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="28868-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="28868-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="28868-168">Nella sezione **Configurazione di Kiteworks** fare clic su **Configura Kiteworks** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="28868-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="28868-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="28868-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="28868-171">Accedere al sito aziendale di Kiteworks come amministratore.</span><span class="sxs-lookup"><span data-stu-id="28868-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="28868-172">Nel barra degli strumenti in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="28868-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="28868-174">Nella sezione **Authentication and Authorization** (Autenticazione e autorizzazione) fare clic su **SSO Setup** (Configurazione SSO).</span><span class="sxs-lookup"><span data-stu-id="28868-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="28868-176">Nella pagina di configurazione dell’accesso Single Sign-On, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="28868-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="28868-178">a.</span><span class="sxs-lookup"><span data-stu-id="28868-178">a.</span></span> <span data-ttu-id="28868-179">Selezionare **Autentica tramite Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="28868-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="28868-180">b.</span><span class="sxs-lookup"><span data-stu-id="28868-180">b.</span></span> <span data-ttu-id="28868-181">Selezionare **Avvia richiesta autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="28868-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="28868-182">c.</span><span class="sxs-lookup"><span data-stu-id="28868-182">c.</span></span> <span data-ttu-id="28868-183">Nella casella di testo **IdP Entity ID** (ID entità IdP) incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28868-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="28868-184">d.</span><span class="sxs-lookup"><span data-stu-id="28868-184">d.</span></span> <span data-ttu-id="28868-185">Nella casella di testo **URL servizio Single Sign-On** incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28868-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="28868-186">e.</span><span class="sxs-lookup"><span data-stu-id="28868-186">e.</span></span> <span data-ttu-id="28868-187">Nella casella di testo **URL servizio punto di disconnessione singolo** incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28868-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="28868-188">f.</span><span class="sxs-lookup"><span data-stu-id="28868-188">f.</span></span> <span data-ttu-id="28868-189">Aprire il certificato scaricato nel Blocco note, copiare il contenuto e incollarlo nella casella di testo **RSA Public Key Certificate** .</span><span class="sxs-lookup"><span data-stu-id="28868-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="28868-190">g.</span><span class="sxs-lookup"><span data-stu-id="28868-190">g.</span></span> <span data-ttu-id="28868-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="28868-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="28868-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="28868-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="28868-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="28868-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="28868-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28868-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28868-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="28868-196">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28868-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="28868-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="28868-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28868-199">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="28868-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28868-201">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="28868-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28868-203">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="28868-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28868-205">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="28868-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28868-207">a.</span><span class="sxs-lookup"><span data-stu-id="28868-207">a.</span></span> <span data-ttu-id="28868-208">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28868-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28868-209">b.</span><span class="sxs-lookup"><span data-stu-id="28868-209">b.</span></span> <span data-ttu-id="28868-210">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28868-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28868-211">c.</span><span class="sxs-lookup"><span data-stu-id="28868-211">c.</span></span> <span data-ttu-id="28868-212">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="28868-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="28868-213">d.</span><span class="sxs-lookup"><span data-stu-id="28868-213">d.</span></span> <span data-ttu-id="28868-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="28868-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="28868-215">Creazione di un utente test per Kiteworks</span><span class="sxs-lookup"><span data-stu-id="28868-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="28868-216">Questa sezione descrive come creare un utente chiamato Britta Simon in Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="28868-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="28868-217">Kiteworks supporta il provisioning JIT (just-in-time), che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="28868-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="28868-218">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="28868-218">There is no action item for you in this section.</span></span> <span data-ttu-id="28868-219">Durante un tentativo di accesso a Kiteworks viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="28868-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="28868-220">Per creare un utente manualmente è necessario contattare il [team di supporto di Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="28868-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="28868-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="28868-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="28868-222">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="28868-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="28868-224">**Per assegnare Britta Simon a Kiteworks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="28868-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="28868-225">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="28868-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="28868-227">Nell'elenco di applicazioni selezionare **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="28868-227">In the applications list, select **Kiteworks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="28868-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="28868-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="28868-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="28868-231">Click **Add** button.</span></span> <span data-ttu-id="28868-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="28868-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="28868-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="28868-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="28868-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="28868-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28868-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="28868-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28868-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="28868-237">Testing single sign-on</span></span>

<span data-ttu-id="28868-238">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="28868-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="28868-239">Quando si fa clic sul riquadro Kiteworks nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="28868-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28868-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="28868-240">Additional resources</span></span>

* [<span data-ttu-id="28868-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28868-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28868-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28868-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

