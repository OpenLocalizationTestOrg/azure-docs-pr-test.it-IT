---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Sign | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Adobe Sign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="0961c-103">Esercitazione: Integrazione di Azure Active Directory con Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="0961c-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="0961c-104">Questa esercitazione descrive come integrare Adobe Sign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0961c-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0961c-105">L'integrazione di Adobe Sign con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0961c-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0961c-106">È possibile controllare in Azure AD chi può accedere a Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="0961c-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="0961c-107">È possibile abilitare gli utenti per l'accesso automatico a Adobe Sign (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0961c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0961c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0961c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0961c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0961c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0961c-110">Prerequisites</span></span>

<span data-ttu-id="0961c-111">Per configurare l'integrazione di Azure AD con Adobe Sign, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0961c-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="0961c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0961c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0961c-113">Sottoscrizione di Adobe Sign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0961c-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0961c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0961c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0961c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0961c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0961c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0961c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0961c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0961c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0961c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0961c-118">Scenario description</span></span>
<span data-ttu-id="0961c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0961c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0961c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0961c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0961c-121">Aggiunta di Adobe Sign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0961c-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="0961c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="0961c-123">Aggiunta di Adobe Sign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0961c-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="0961c-124">Per configurare l'integrazione di Adobe Sign in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0961c-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0961c-125">**Per aggiungere Adobe Sign dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0961c-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0961c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0961c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0961c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0961c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0961c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0961c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0961c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0961c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0961c-133">Nella casella di ricerca digitare **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="0961c-133">In the search box, type **Adobe Sign**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="0961c-135">Nel pannello dei risultati selezionare **Adobe Sign** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0961c-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0961c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0961c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Sign usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0961c-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0961c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Adobe Sign che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0961c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="0961c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="0961c-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="0961c-141">Per stabilire la relazione di collegamento, in Adobe Sign assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="0961c-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0961c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Adobe Sign, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0961c-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0961c-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0961c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0961c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0961c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0961c-145">**[Creazione di un utente di test di Adobe Sign](#creating-an-adobe-sign-test-user)**: per avere una controparte di Britta Simon in Adobe Sign collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0961c-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0961c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0961c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0961c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0961c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0961c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0961c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="0961c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="0961c-150">**Per configurare l'accesso Single Sign-On di Azure AD con Adobe Sign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0961c-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="0961c-151">Nella pagina di integrazione dell'applicazione **Adobe Sign** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0961c-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0961c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0961c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="0961c-155">Nella sezione **Adobe Sign Domain and URLs** (URL e dominio Adobe Sign) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0961c-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="0961c-157">a.</span><span class="sxs-lookup"><span data-stu-id="0961c-157">a.</span></span> <span data-ttu-id="0961c-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.echosign.com/`.</span><span class="sxs-lookup"><span data-stu-id="0961c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="0961c-159">b.</span><span class="sxs-lookup"><span data-stu-id="0961c-159">b.</span></span> <span data-ttu-id="0961c-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="0961c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0961c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0961c-161">These values are not real.</span></span> <span data-ttu-id="0961c-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0961c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0961c-163">Per ottenere questi valori, contattare il [team di supporto clienti di Adobe Sign](https://helpx.adobe.com/in/contact/support.html).</span><span class="sxs-lookup"><span data-stu-id="0961c-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="0961c-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="0961c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="0961c-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0961c-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0961c-168">Nella sezione **Adobe Sign Configuration** (Configurazione Adobe Sign) fare clic su **Configure Adobe Sign** (Configura Adobe Sign) per aprire la finestra **Configure sign-on** (Configura accesso).</span><span class="sxs-lookup"><span data-stu-id="0961c-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0961c-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0961c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="0961c-171">In un'altra finestra del Web browser accedere al sito aziendale di Adobe Sign come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0961c-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="0961c-172">Nel menu in alto fare clic su **Account** e quindi nel riquadro di spostamento a sinistra fare clic su **SAML Settings** (Impostazioni SAML) in **Account Settings** (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="0961c-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="0961c-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="0961c-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="0961c-174">Nella sezione relativa alle impostazioni SAML, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0961c-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="0961c-175">![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="0961c-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="0961c-176">a.</span><span class="sxs-lookup"><span data-stu-id="0961c-176">a.</span></span> <span data-ttu-id="0961c-177">Per **SAML Mode** (Modalità SAML), selezionare **SAML Mandatory** (SAML obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="0961c-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="0961c-178">b.</span><span class="sxs-lookup"><span data-stu-id="0961c-178">b.</span></span> <span data-ttu-id="0961c-179">Selezionare **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span><span class="sxs-lookup"><span data-stu-id="0961c-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="0961c-180">c.</span><span class="sxs-lookup"><span data-stu-id="0961c-180">c.</span></span> <span data-ttu-id="0961c-181">In **User Creation** (Creazione utente), selezionare **Automatically add users authenticated through SAML** (Aggiungi automaticamente gli utenti autenticati tramite SAML).</span><span class="sxs-lookup"><span data-stu-id="0961c-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="0961c-182">Continuare e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0961c-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="0961c-183">![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="0961c-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="0961c-184">a.</span><span class="sxs-lookup"><span data-stu-id="0961c-184">a.</span></span> <span data-ttu-id="0961c-185">Incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure nella casella di testo **IdP Entity ID** (ID entità IdP).</span><span class="sxs-lookup"><span data-stu-id="0961c-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="0961c-186">b.</span><span class="sxs-lookup"><span data-stu-id="0961c-186">b.</span></span> <span data-ttu-id="0961c-187">Incollare **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure nella casella di testo **IdP Login URL** (ID accesso IdP).</span><span class="sxs-lookup"><span data-stu-id="0961c-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="0961c-188">c.</span><span class="sxs-lookup"><span data-stu-id="0961c-188">c.</span></span> <span data-ttu-id="0961c-189">Incollare l'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **IdP Logout URL** (ID disconnessione IdP).</span><span class="sxs-lookup"><span data-stu-id="0961c-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="0961c-190">d.</span><span class="sxs-lookup"><span data-stu-id="0961c-190">d.</span></span> <span data-ttu-id="0961c-191">Aprire **Certificate(Base64)** scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **IdP Certificate** (Certificato IdP)</span><span class="sxs-lookup"><span data-stu-id="0961c-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="0961c-192">e.</span><span class="sxs-lookup"><span data-stu-id="0961c-192">e.</span></span> <span data-ttu-id="0961c-193">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="0961c-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0961c-194">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0961c-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0961c-195">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0961c-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0961c-196">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0961c-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0961c-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="0961c-198">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0961c-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0961c-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0961c-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0961c-201">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0961c-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0961c-203">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0961c-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0961c-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0961c-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0961c-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0961c-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0961c-209">a.</span><span class="sxs-lookup"><span data-stu-id="0961c-209">a.</span></span> <span data-ttu-id="0961c-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0961c-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0961c-211">b.</span><span class="sxs-lookup"><span data-stu-id="0961c-211">b.</span></span> <span data-ttu-id="0961c-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0961c-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0961c-213">c.</span><span class="sxs-lookup"><span data-stu-id="0961c-213">c.</span></span> <span data-ttu-id="0961c-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0961c-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0961c-215">d.</span><span class="sxs-lookup"><span data-stu-id="0961c-215">d.</span></span> <span data-ttu-id="0961c-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0961c-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="0961c-217">Creazione di un utente di test di Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="0961c-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="0961c-218">Per consentire agli utenti di Azure AD di accedere a Adobe Sign, è necessario eseguirne il provisioning in Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="0961c-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="0961c-219">Nel caso di Adobe Sign, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="0961c-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="0961c-220">È possibile usare qualsiasi altro strumento o API di creazione di account utente forniti da Adobe Sign per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="0961c-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="0961c-221">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0961c-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0961c-222">Accedere al sito aziendale di **Adobe Sign** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0961c-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="0961c-223">Nel menu in alto fare clic su **Account** e quindi nel riquadro di spostamento a sinistra fare clic su **Users & Groups** (Utenti e gruppi) e su **Create a new user** (Crea nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="0961c-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="0961c-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="0961c-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="0961c-225">Nella sezione **Create New User** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0961c-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="0961c-226">![Crea utente](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="0961c-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="0961c-227">a.</span><span class="sxs-lookup"><span data-stu-id="0961c-227">a.</span></span> <span data-ttu-id="0961c-228">Digitare l'**indirizzo di posta elettronica**, il **nome** e il **cognome** di un account utente AAD valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="0961c-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="0961c-229">b.</span><span class="sxs-lookup"><span data-stu-id="0961c-229">b.</span></span> <span data-ttu-id="0961c-230">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="0961c-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="0961c-231">Il titolare dell'account di Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="0961c-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0961c-232">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0961c-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0961c-233">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="0961c-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0961c-235">**Per assegnare Britta Simon a Adobe Sign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0961c-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="0961c-236">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0961c-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0961c-238">Nell'elenco di applicazioni selezionare **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="0961c-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="0961c-240">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0961c-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0961c-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0961c-242">Click **Add** button.</span></span> <span data-ttu-id="0961c-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0961c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0961c-245">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0961c-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0961c-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0961c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0961c-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0961c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0961c-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0961c-248">Testing single sign-on</span></span>

<span data-ttu-id="0961c-249">Quando si fa clic sul riquadro Adobe Sign nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="0961c-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="0961c-250">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0961c-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0961c-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0961c-251">Additional resources</span></span>

* [<span data-ttu-id="0961c-252">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0961c-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0961c-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0961c-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

