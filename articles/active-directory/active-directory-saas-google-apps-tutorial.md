---
title: 'Esercitazione: integrazione di Azure Active Directory con Google Apps in Azure| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="1ebcf-103">Esercitazione: Integrazione di Azure Active Directory con Google Apps</span><span class="sxs-lookup"><span data-stu-id="1ebcf-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="1ebcf-104">Questa esercitazione descrive come integrare Google Apps con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ebcf-105">L'integrazione di Google Apps con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ebcf-106">È possibile controllare in Azure AD chi accede a Google Apps</span><span class="sxs-lookup"><span data-stu-id="1ebcf-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="1ebcf-107">È possibile abilitare gli utenti per l'accesso automatico a Google Apps, ovvero l'accesso Single Sign-On, con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ebcf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ebcf-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ebcf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1ebcf-110">Prerequisites</span></span>

<span data-ttu-id="1ebcf-111">Per configurare l'integrazione di Azure AD con Google Apps sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="1ebcf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ebcf-113">Sottoscrizione di Google Apps abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1ebcf-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ebcf-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ebcf-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ebcf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ebcf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="1ebcf-118">Esercitazione video</span><span class="sxs-lookup"><span data-stu-id="1ebcf-118">Video tutorial</span></span>
<span data-ttu-id="1ebcf-119">Come abilitare Single Sign-On in Google Apps in 2 minuti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="1ebcf-120">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="1ebcf-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="1ebcf-121">**D: I dispositivi Chromebooks e altri dispositivi Chrome sono compatibili con Single Sign-On di Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="1ebcf-122">R: Sì, gli utenti possono accedere ai dispositivi Chromebook con le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="1ebcf-123">Per informazioni sui motivi per cui agli utenti può essere richiesto di immettere le credenziali due volte, vedere questo [articolo del supporto tecnico di Google Apps](https://support.google.com/chrome/a/answer/6060880) .</span><span class="sxs-lookup"><span data-stu-id="1ebcf-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="1ebcf-124">**D: Se si abilita il Single Sign-On, gli utenti potranno usare le credenziali di Azure AD per accedere a qualsiasi prodotto di Google, ad esempio Google Classroom, GMail, Google Drive, YouTube e così via?**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="1ebcf-125">R: Sì, a seconda delle [Google Apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) che si sceglie di abilitare o disabilitare per la propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="1ebcf-126">**D: È possibile abilitare il Single Sign-On solo per un sottoinsieme di utenti di Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="1ebcf-127">R: No, l'attivazione del Single Sign-On richiede immediatamente a tutti gli utenti di Google Apps di autenticarsi con le proprie credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="1ebcf-128">Poiché Google Apps non supporta più provider di identità, il provider di identità per l'ambiente di Google Apps può essere AD Azure o Google, ma non entrambi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="1ebcf-129">**D: Se un utente ha eseguito l'accesso tramite Windows, viene autenticano automaticamente in Google Apps senza che venga richiesta una password?**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="1ebcf-130">R: Sono disponibili due opzioni per l'abilitazione di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="1ebcf-131">Nel primo caso gli utenti possono accedere ai dispositivi Windows 10 tramite [Aggiunta ad Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="1ebcf-132">In alternativa, gli utenti possono accedere ai dispositivi Windows appartenenti a un dominio di Active Directory locale abilitato per il Single Sign-On in Azure AD tramite una distribuzione di [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) .</span><span class="sxs-lookup"><span data-stu-id="1ebcf-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="1ebcf-133">Per entrambe le opzioni è necessario eseguire la procedura descritta nell'esercitazione seguente per abilitare il Single Sign-On tra Azure AD e Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ebcf-134">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1ebcf-134">Scenario description</span></span>
<span data-ttu-id="1ebcf-135">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ebcf-136">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ebcf-137">Aggiunta di Google Apps dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1ebcf-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="1ebcf-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="1ebcf-139">Aggiunta di Google Apps dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1ebcf-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="1ebcf-140">Per configurare l'integrazione di Google Apps in Azure AD, è necessario aggiungere Google Apps dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ebcf-141">**Per aggiungere Google Apps dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ebcf-142">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ebcf-144">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ebcf-145">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-145">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1ebcf-147">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1ebcf-149">Nella casella di ricerca digitare **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-149">In the search box, type **Google Apps**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="1ebcf-151">Nel pannello dei risultati selezionare **Google Apps** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ebcf-153">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ebcf-154">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Google Apps usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1ebcf-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ebcf-155">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Google Apps che corrisponde all'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="1ebcf-156">In altre parole, deve essere stabilita una relazione di collegamento tra l'utente di Azure AD e l'utente correlato in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="1ebcf-157">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="1ebcf-158">Per configurare e testare l'accesso Single Sign-On di Azure AD con Google Apps, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ebcf-159">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ebcf-160">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ebcf-161">**[Creazione di un utente test di Google Apps](#creating-a-google-apps-test-user)**: per avere una controparte di Britta Simon in Google Apps collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ebcf-162">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ebcf-163">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ebcf-164">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ebcf-165">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="1ebcf-166">**Per configurare l'accesso Single Sign-On di Azure AD con Google Apps, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="1ebcf-167">Nella pagina di integrazione dell'applicazione **Google Apps** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1ebcf-169">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="1ebcf-171">Nella sezione **Google Apps Domain and URLs** (URL e dominio di Google Apps) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="1ebcf-173">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="1ebcf-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ebcf-174">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="1ebcf-174">This value is not real.</span></span> <span data-ttu-id="1ebcf-175">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="1ebcf-176">Contattare il [team di supporto di Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="1ebcf-177">Nella sezione **SAML Signing Certificate** (Certificato di firma SAML) fare clic su **Certificate** e quindi salvare il certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="1ebcf-179">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1ebcf-179">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ebcf-181">Nella sezione **Google Apps Configuration** (Configurazione di Google Apps) fare clic su **Configure Google Apps** (Configura Google Apps) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ebcf-182">Copiare l'**URL di disconnessione, l'URL di modifica password e l'URL del servizio Single Sign-On SAML** dalla sezione di **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="1ebcf-184">Aprire una nuova scheda nel browser e accedere a [Console di amministrazione di Google Apps](http://admin.google.com/) utilizzando l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="1ebcf-185">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-185">Click **Security**.</span></span> <span data-ttu-id="1ebcf-186">Se non viene visualizzato il collegamento, può essere nascosto sotto il menu **More Controls** nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Fare clic su sicurezza.][10]

9. <span data-ttu-id="1ebcf-188">Nella pagina **Security** (Sicurezza) fare clic su **Set up single sign-on (SSO)** (Configurazione Single Sign-On (SSO)).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Fare clic su SSO.][11]

10. <span data-ttu-id="1ebcf-190">Eseguire le seguenti modifiche di configurazione:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-190">Perform the following configuration changes:</span></span>
   
    ![Configurare SSL][12]
   
    <span data-ttu-id="1ebcf-192">a.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-192">a.</span></span> <span data-ttu-id="1ebcf-193">Selezionare **Setup SSO with third party identity provider** (Configurare l'accesso SSO con un provider di terze parti).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="1ebcf-194">b.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-194">b.</span></span> <span data-ttu-id="1ebcf-195">Nel campo **Sign-in page URL** (URL pagina di accesso) di Google Apps incollare il valore dell'**URL del servizio Single Sign-On** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1ebcf-196">c.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-196">c.</span></span> <span data-ttu-id="1ebcf-197">Nel campo **Sign-out page URL** (URL pagina di disconnessione) di Google Apps incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1ebcf-198">d.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-198">d.</span></span> <span data-ttu-id="1ebcf-199">Nel campo **Change password URL** (URL per la modifica della password) di Google Apps incollare il valore dell'**URL di modifica della password** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1ebcf-200">e.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-200">e.</span></span> <span data-ttu-id="1ebcf-201">In Google Apps per il **certificato di verifica**, caricare il certificato che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1ebcf-202">f.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-202">f.</span></span> <span data-ttu-id="1ebcf-203">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1ebcf-204">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ebcf-205">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ebcf-206">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ebcf-207">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ebcf-208">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1ebcf-210">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ebcf-211">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ebcf-213">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ebcf-215">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ebcf-217">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1ebcf-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ebcf-219">a.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-219">a.</span></span> <span data-ttu-id="1ebcf-220">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ebcf-221">b.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-221">b.</span></span> <span data-ttu-id="1ebcf-222">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ebcf-223">c.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-223">c.</span></span> <span data-ttu-id="1ebcf-224">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ebcf-225">d.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-225">d.</span></span> <span data-ttu-id="1ebcf-226">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="1ebcf-227">Creazione di un utente test di Google Apps</span><span class="sxs-lookup"><span data-stu-id="1ebcf-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="1ebcf-228">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="1ebcf-229">Google Apps supporta il provisioning automatico abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="1ebcf-230">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-230">There is no action for you in this section.</span></span> <span data-ttu-id="1ebcf-231">Se un utente non esiste in Google Apps, ne viene creato uno nuovo quando si tenta di accedere a Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="1ebcf-232">Se è necessario creare un utente manualmente, contattare il [team di supporto di Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="1ebcf-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ebcf-233">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ebcf-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ebcf-234">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1ebcf-236">**Per assegnare Britta Simon a Google Apps, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1ebcf-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="1ebcf-237">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1ebcf-239">Nell'elenco di applicazioni selezionare **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-239">In the applications list, select **Google Apps**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="1ebcf-241">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1ebcf-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-243">Click **Add** button.</span></span> <span data-ttu-id="1ebcf-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1ebcf-246">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ebcf-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ebcf-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ebcf-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1ebcf-249">Testing single sign-on</span></span>

<span data-ttu-id="1ebcf-250">In questa sezione per testare le impostazioni dell'accesso Single Sign-On, aprire il Riquadro di accesso all'indirizzo [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), quindi accedere all'account di test e fare clic sul riquadro **Google Apps** nel Riquadro di accesso.</span><span class="sxs-lookup"><span data-stu-id="1ebcf-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ebcf-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1ebcf-251">Additional resources</span></span>

* [<span data-ttu-id="1ebcf-252">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ebcf-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ebcf-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ebcf-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1ebcf-254">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="1ebcf-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png