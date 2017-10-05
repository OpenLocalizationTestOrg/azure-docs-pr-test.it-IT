---
title: 'Esercitazione: Integrazione di Azure Active Directory con FreshDesk | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="65c25-103">Esercitazione: Integrazione di Azure Active Directory con FreshDesk</span><span class="sxs-lookup"><span data-stu-id="65c25-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="65c25-104">Questa esercitazione descrive come integrare FreshDesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65c25-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65c25-105">L'integrazione di FreshDesk con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="65c25-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65c25-106">È possibile controllare in Azure AD chi può accedere a FreshDesk</span><span class="sxs-lookup"><span data-stu-id="65c25-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="65c25-107">È possibile abilitare gli utenti per l'accesso automatico a FreshDesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65c25-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="65c25-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="65c25-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65c25-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65c25-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65c25-110">Prerequisites</span></span>

<span data-ttu-id="65c25-111">Per configurare l'integrazione di Azure AD con FreshDesk, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="65c25-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="65c25-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c25-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65c25-113">Sottoscrizione di FreshDesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="65c25-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65c25-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="65c25-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65c25-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="65c25-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65c25-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="65c25-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="65c25-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65c25-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65c25-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="65c25-118">Scenario description</span></span>
<span data-ttu-id="65c25-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="65c25-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65c25-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="65c25-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65c25-121">Aggiunta di FreshDesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="65c25-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="65c25-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="65c25-123">Aggiunta di FreshDesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="65c25-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="65c25-124">Per configurare l'integrazione di FreshDesk in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="65c25-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65c25-125">**Per aggiungere FreshDesk dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="65c25-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65c25-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="65c25-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65c25-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="65c25-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65c25-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="65c25-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="65c25-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="65c25-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="65c25-133">Nella casella di ricerca digitare **Freshdesk**.</span><span class="sxs-lookup"><span data-stu-id="65c25-133">In the search box, type **FreshDesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="65c25-135">Nel pannello dei risultati selezionare **FreshDesk** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="65c25-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65c25-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65c25-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FreshDesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="65c25-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65c25-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di FreshDesk che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c25-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="65c25-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="65c25-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="65c25-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con FreshDesk, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="65c25-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65c25-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="65c25-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65c25-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65c25-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65c25-145">**[Creazione di un utente test di FreshDesk](#creating-a-freshdesk-test-user)**: per avere una controparte di Britta Simon in FreshDesk collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c25-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="65c25-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c25-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65c25-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="65c25-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65c25-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65c25-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="65c25-150">**Per configurare l'accesso Single Sign-On di Azure AD con FreshDesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="65c25-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="65c25-151">Nella pagina di integrazione dell'applicazione **FreshDesk** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="65c25-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="65c25-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="65c25-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="65c25-155">Nella sezione **FreshDesk Domain and URLs** (Dominio e URL FreshDesk), immettere un valore per **URL di accesso** come: `https://<tenant-name>.freshdesk.com` o qualsiasi altro valore suggerito da FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="65c25-157">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="65c25-157">Please note that this is not the real value.</span></span> <span data-ttu-id="65c25-158">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="65c25-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="65c25-159">Per ottenere tale valore, contattare il [team di supporto di FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="65c25-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="65c25-160">Nella sezione **SAML Signing Certificate** (Certificato di firma SAML) fare clic su **Certificate** e quindi salvare il certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="65c25-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="65c25-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="65c25-162">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65c25-164">Nella sezione **FreshDesk Configuration** (Configurazione di FreshDesk) fare clic su **Configure FreshDesk** (Configura FreshDesk) per aprire la finestra Configura accesso.</span><span class="sxs-lookup"><span data-stu-id="65c25-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="65c25-165">Copiare l’URL servizio Single Sign-On SAML e l’URL Sign-Out dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="65c25-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="65c25-167">In un'altra finestra del Web browser accedere al sito aziendale di Freshdesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="65c25-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="65c25-168">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="65c25-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="65c25-169">![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="65c25-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="65c25-170">Nella scheda **General Settings** fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="65c25-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="65c25-171">![Sicurezza](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="65c25-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="65c25-172">Nella sezione **Security** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="65c25-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="65c25-173">![Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="65c25-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="65c25-174">a.</span><span class="sxs-lookup"><span data-stu-id="65c25-174">a.</span></span> <span data-ttu-id="65c25-175">Per **Single Sign On (SSO)** selezionare **On**.</span><span class="sxs-lookup"><span data-stu-id="65c25-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="65c25-176">b.</span><span class="sxs-lookup"><span data-stu-id="65c25-176">b.</span></span> <span data-ttu-id="65c25-177">Selezionare **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="65c25-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="65c25-178">c.</span><span class="sxs-lookup"><span data-stu-id="65c25-178">c.</span></span> <span data-ttu-id="65c25-179">Digitare l’ **URL servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **SAML Login URL** (URL accesso SAML).</span><span class="sxs-lookup"><span data-stu-id="65c25-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="65c25-180">d.</span><span class="sxs-lookup"><span data-stu-id="65c25-180">d.</span></span> <span data-ttu-id="65c25-181">Digitare l’ **URL Sign-Out** copiato dal portale di Azure nella casella di testo **URL disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="65c25-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="65c25-182">e.</span><span class="sxs-lookup"><span data-stu-id="65c25-182">e.</span></span> <span data-ttu-id="65c25-183">Copiare il valore di **Identificazione personale** dal certificato scaricato dal portale di Azure e quindi incollarlo nella casella di testo **Impronta digitale certificato di protezione**.</span><span class="sxs-lookup"><span data-stu-id="65c25-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="65c25-184">Per informazioni dettagliate, vedere il video che illustra [come recuperare il valore di identificazione personale di un certificato](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="65c25-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="65c25-185">f.</span><span class="sxs-lookup"><span data-stu-id="65c25-185">f.</span></span> <span data-ttu-id="65c25-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="65c25-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65c25-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="65c25-188">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="65c25-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="65c25-190">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65c25-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65c25-191">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="65c25-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65c25-193">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="65c25-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65c25-195">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="65c25-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65c25-197">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="65c25-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65c25-199">a.</span><span class="sxs-lookup"><span data-stu-id="65c25-199">a.</span></span> <span data-ttu-id="65c25-200">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65c25-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65c25-201">b.</span><span class="sxs-lookup"><span data-stu-id="65c25-201">b.</span></span> <span data-ttu-id="65c25-202">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65c25-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65c25-203">c.</span><span class="sxs-lookup"><span data-stu-id="65c25-203">c.</span></span> <span data-ttu-id="65c25-204">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="65c25-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65c25-205">d.</span><span class="sxs-lookup"><span data-stu-id="65c25-205">d.</span></span> <span data-ttu-id="65c25-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="65c25-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="65c25-207">Creazione di un utente test di FreshDesk</span><span class="sxs-lookup"><span data-stu-id="65c25-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="65c25-208">Per consentire agli utenti di Azure AD di accedere a FreshDesk, è necessario eseguirne il provisioning in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="65c25-209">Nel caso di FreshDesk, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="65c25-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="65c25-210">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="65c25-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="65c25-211">Accedere al tenant di **Freshdesk** .</span><span class="sxs-lookup"><span data-stu-id="65c25-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="65c25-212">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="65c25-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="65c25-213">![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="65c25-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="65c25-214">Nella scheda **General Settings** fare clic su **Agents**.</span><span class="sxs-lookup"><span data-stu-id="65c25-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="65c25-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="65c25-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="65c25-216">Fare clic su **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="65c25-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="65c25-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span><span class="sxs-lookup"><span data-stu-id="65c25-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="65c25-218">Nella finestra di dialogo Agent Information seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="65c25-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="65c25-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span><span class="sxs-lookup"><span data-stu-id="65c25-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="65c25-220">a.</span><span class="sxs-lookup"><span data-stu-id="65c25-220">a.</span></span> <span data-ttu-id="65c25-221">Nella casella di testo **Full Name** , digitare il nome dell'account Azure AD di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="65c25-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="65c25-222">b.</span><span class="sxs-lookup"><span data-stu-id="65c25-222">b.</span></span> <span data-ttu-id="65c25-223">Nella casella di testo **Email** , digitare l’indirizzo di posta elettronica dell'account Azure AD di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="65c25-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="65c25-224">c.</span><span class="sxs-lookup"><span data-stu-id="65c25-224">c.</span></span> <span data-ttu-id="65c25-225">Nella casella di testo **Title** , digitare il titolo dell'account Azure AD di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="65c25-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="65c25-226">d.</span><span class="sxs-lookup"><span data-stu-id="65c25-226">d.</span></span> <span data-ttu-id="65c25-227">Selezionare **Agents role** e quindi fare clic su **Assign**.</span><span class="sxs-lookup"><span data-stu-id="65c25-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="65c25-228">e.</span><span class="sxs-lookup"><span data-stu-id="65c25-228">e.</span></span> <span data-ttu-id="65c25-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="65c25-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="65c25-230">Il titolare dell'account AD riceverà un messaggio di posta elettronica contenente un collegamento da selezionare per confermare e attivare l'account.</span><span class="sxs-lookup"><span data-stu-id="65c25-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="65c25-231">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Freshdesk per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="65c25-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="65c25-232">a FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65c25-233">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c25-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65c25-234">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Box.</span><span class="sxs-lookup"><span data-stu-id="65c25-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Assegna utente][200] 

<span data-ttu-id="65c25-236">**Per assegnare Britta Simon a FreshDesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="65c25-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="65c25-237">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="65c25-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="65c25-239">Nell'elenco delle applicazioni, selezionare **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="65c25-239">In the applications list, select **FreshDesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="65c25-241">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="65c25-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="65c25-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="65c25-243">Click **Add** button.</span></span> <span data-ttu-id="65c25-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="65c25-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="65c25-246">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="65c25-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65c25-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="65c25-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65c25-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="65c25-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65c25-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="65c25-249">Testing single sign-on</span></span>

<span data-ttu-id="65c25-250">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="65c25-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65c25-251">Quando si fa clic sul riquadro FreshDesk nel pannello di accesso, si apre la pagina per accedere all'applicazione FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="65c25-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65c25-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="65c25-252">Additional resources</span></span>

* [<span data-ttu-id="65c25-253">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65c25-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65c25-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65c25-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

