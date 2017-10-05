---
title: 'Esercitazione: Integrazione di Azure Active Directory con SuccessFactors | Microsoft Docs'
description: Informazioni su come usare SuccessFactors con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="1051a-103">Esercitazione: Integrazione di Azure Active Directory con SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="1051a-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="1051a-104">Questa esercitazione descrive l'integrazione di SuccessFactors con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1051a-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1051a-105">L'integrazione di SuccessFactors con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1051a-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1051a-106">È possibile controllare in Azure AD chi può accedere a SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="1051a-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="1051a-107">È possibile abilitare gli utenti per l'accesso automatico a SuccessFactors (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="1051a-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="1051a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1051a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1051a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1051a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1051a-110">Prerequisites</span></span>
<span data-ttu-id="1051a-111">Per configurare l'integrazione di Azure AD con SuccessFactors, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1051a-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="1051a-112">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="1051a-112">A valid Azure subscription</span></span>
* <span data-ttu-id="1051a-113">Un tenant in SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="1051a-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="1051a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1051a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1051a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1051a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1051a-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1051a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1051a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1051a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1051a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1051a-118">Scenario description</span></span>
<span data-ttu-id="1051a-119">L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1051a-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1051a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1051a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1051a-121">Aggiunta di SuccessFactors dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1051a-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="1051a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="1051a-123">Aggiunta di SuccessFactors dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1051a-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="1051a-124">Per configurare l'integrazione di SuccessFactors in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1051a-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1051a-125">**Per aggiungere SuccessFactors dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1051a-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1051a-126">Nel portale di Azure classico fare clic su **Active Directory**nel pannello di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1051a-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][1]
2. <span data-ttu-id="1051a-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="1051a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1051a-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="1051a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][2]
4. <span data-ttu-id="1051a-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="1051a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="1051a-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="1051a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][4]
6. <span data-ttu-id="1051a-135">Nella **casella di ricerca** digitare **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="1051a-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][5]
7. <span data-ttu-id="1051a-137">Nel riquadro dei risultati selezionare **SuccessFactors**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1051a-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1051a-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1051a-140">Questa sezione descrive come configurare e testare l'accesso Single Sign-On di Azure AD con SuccessFactors con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1051a-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1051a-141">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SuccessFactors che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="1051a-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="1051a-143">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **nome utente** in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="1051a-144">Per configurare e testare l'accesso Single Sign-On di Azure AD con SuccessFactors, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1051a-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1051a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1051a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1051a-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1051a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1051a-147">**[Creazione di un utente test SuccessFactors](#creating-a-successfactors-test-user)** : per avere una controparte di Britta Simon in SuccessFactors collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1051a-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1051a-149">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1051a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1051a-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="1051a-151">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure classico e viene configurato l'accesso Single Sign-On nell'applicazione SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="1051a-152">**Per configurare l'accesso Single Sign-On di Azure AD con SuccessFactors, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1051a-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="1051a-153">Nella pagina di integrazione dell'applicazione **SuccessFactors** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1051a-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][7]
2. <span data-ttu-id="1051a-155">Nella pagina **How would you like users to sign on to SuccessFactors** (Stabilire come si desidera che gli utenti accedano a SuccessFactors) selezionare **Single Sign-On di Microsoft Azure AD**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1051a-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][8]
3. <span data-ttu-id="1051a-157">Nella pagina **Configura URL app** seguire questa procedura e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1051a-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][9]
   
    <span data-ttu-id="1051a-159">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-159">a.</span></span> <span data-ttu-id="1051a-160">Nella casella di testo **URL accesso** digitare un URL corrispondente al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="1051a-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="1051a-161">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-161">b.</span></span> <span data-ttu-id="1051a-162">Nella casella di testo **URL di risposta** digitare un URL corrispondente al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="1051a-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="1051a-163">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-163">c.</span></span> <span data-ttu-id="1051a-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1051a-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="1051a-165">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="1051a-165">Please note that these are not the real values.</span></span> <span data-ttu-id="1051a-166">È necessario aggiornare questi valori con l'URL di accesso, l'ID e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="1051a-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="1051a-167">Per ottenere questi valori, contattare il [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="1051a-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="1051a-168">Nella pagina **Configure single sign-on at SuccessFactors** (Configura accesso Single Sign-On in SuccessFactors) fare clic su **Scarica certificato** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="1051a-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][10]

2. <span data-ttu-id="1051a-170">In un'altra finestra del Web browser accedere al **portale di amministrazione di SuccessFactors** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1051a-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="1051a-171">Vedere **Sicurezza applicazione** e **Single Sign On Feature** (Funzionalità di accesso Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="1051a-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="1051a-172">Inserire un valore qualsiasi in **Reset Token** (Reimposta token) e fare clic su **Save Token** (Salva token) per abilitare SSO SAML.</span><span class="sxs-lookup"><span data-stu-id="1051a-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][11]

    > [!NOTE] 
    > <span data-ttu-id="1051a-174">Questo valore viene usato solo come opzione di attivazione o disattivazione.</span><span class="sxs-lookup"><span data-stu-id="1051a-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="1051a-175">Se viene salvato un valore, SSO SAML è ON.</span><span class="sxs-lookup"><span data-stu-id="1051a-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="1051a-176">Se viene salvato un valore vuoto, SSO SAML è OFF.</span><span class="sxs-lookup"><span data-stu-id="1051a-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="1051a-177">Nella schermata sottostante eseguire le azioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="1051a-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][12]
   
    <span data-ttu-id="1051a-179">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-179">a.</span></span> <span data-ttu-id="1051a-180">Selezionare il pulsante di opzione **SAML v2 SSO** (SSO SAML v2)</span><span class="sxs-lookup"><span data-stu-id="1051a-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="1051a-181">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-181">b.</span></span> <span data-ttu-id="1051a-182">Impostare SAML Asserting Party Name (Nome dell'entità di asserzione SAML) ad esempio SAML Issuer + Company name ((Autorità di certificazione SAML) + Nome società).</span><span class="sxs-lookup"><span data-stu-id="1051a-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="1051a-183">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-183">c.</span></span> <span data-ttu-id="1051a-184">Nella casella di testo **SAML Issuer** (Autorità di certificazione SAML) inserire il valore di **URL autorità di certificazione** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="1051a-185">d.</span><span class="sxs-lookup"><span data-stu-id="1051a-185">d.</span></span> <span data-ttu-id="1051a-186">Selezionare **Response(Customer Generated/IdP/AP)** (Risposta - Generata da cliente/IdP/AP) per **Require Mandatory Signature** (Richiedi firma obbligatoria).</span><span class="sxs-lookup"><span data-stu-id="1051a-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="1051a-187">e.</span><span class="sxs-lookup"><span data-stu-id="1051a-187">e.</span></span> <span data-ttu-id="1051a-188">Selezionare **Abilitato** per **Enable SAML Flag** (Abilita flag SAML).</span><span class="sxs-lookup"><span data-stu-id="1051a-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="1051a-189">f.</span><span class="sxs-lookup"><span data-stu-id="1051a-189">f.</span></span> <span data-ttu-id="1051a-190">Selezionare **No** per **Login Request Signature(SF Generated/SP/RP)** (Firma richiesta di accesso - Generata da SF/SP/RP).</span><span class="sxs-lookup"><span data-stu-id="1051a-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="1051a-191">g.</span><span class="sxs-lookup"><span data-stu-id="1051a-191">g.</span></span> <span data-ttu-id="1051a-192">Selezionare **Browser/Post Profile** (Profilo browser/post) per **SAML Profile** (Profilo SAML).</span><span class="sxs-lookup"><span data-stu-id="1051a-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="1051a-193">h.</span><span class="sxs-lookup"><span data-stu-id="1051a-193">h.</span></span> <span data-ttu-id="1051a-194">Selezionare **No** per **Enforce Certificate Valid Period** (Applicare periodo di validità certificato).</span><span class="sxs-lookup"><span data-stu-id="1051a-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="1051a-195">i.</span><span class="sxs-lookup"><span data-stu-id="1051a-195">i.</span></span> <span data-ttu-id="1051a-196">Copiare il contenuto del file del certificato scaricato, copiarlo e incollarlo nella casella di testo **SAML Verifying Certificate** (Verifica certificato SAML).</span><span class="sxs-lookup"><span data-stu-id="1051a-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1051a-197">Il contenuto del certificato deve avere i tag di inizio e fine certificato.</span><span class="sxs-lookup"><span data-stu-id="1051a-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="1051a-198">Passare a SAML V2 e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1051a-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][13]
   
    <span data-ttu-id="1051a-200">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-200">a.</span></span> <span data-ttu-id="1051a-201">Selezionare **Sì** per **Support SP-initiated Global Logout** (Supporto disconnessione globale avviata da SP).</span><span class="sxs-lookup"><span data-stu-id="1051a-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="1051a-202">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-202">b.</span></span> <span data-ttu-id="1051a-203">Nella casella di testo **Global Logout Service URL (LogoutRequest destination)** (URL del servizio disconnessione globale - Destinazione LogoutRequest) inserire il valore di **URL disconnessione remota** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="1051a-204">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-204">c.</span></span> <span data-ttu-id="1051a-205">Selezionare **No** per **Require sp must encrypt all NameID element** (Richiesta a sp di crittografare tutti gli elementi NameID).</span><span class="sxs-lookup"><span data-stu-id="1051a-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="1051a-206">d.</span><span class="sxs-lookup"><span data-stu-id="1051a-206">d.</span></span> <span data-ttu-id="1051a-207">Selezionare **non specificato** per **NameID Format** (Formato NameID).</span><span class="sxs-lookup"><span data-stu-id="1051a-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="1051a-208">e.</span><span class="sxs-lookup"><span data-stu-id="1051a-208">e.</span></span> <span data-ttu-id="1051a-209">Selezionare **Sì** per **Enable sp initiated login (AuthnRequest)** (Abilita accesso avviato da sp - AuthnRequest).</span><span class="sxs-lookup"><span data-stu-id="1051a-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="1051a-210">f.</span><span class="sxs-lookup"><span data-stu-id="1051a-210">f.</span></span> <span data-ttu-id="1051a-211">Nella casella di testo **Send request as Company-Wide issuer** (Invia richiesta come autorità di certificazione a livello di azienda) inserire il valore di **URL accesso remoto** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1051a-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="1051a-212">Eseguire questi passaggi se si vuole che i nomi utente di account di accesso utente non facciano distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="1051a-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="1051a-213">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-213">a.</span></span> <span data-ttu-id="1051a-214">Vedere **Impostazioni società** in basso.</span><span class="sxs-lookup"><span data-stu-id="1051a-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="1051a-215">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-215">b.</span></span> <span data-ttu-id="1051a-216">Selezionare la casella di controllo accanto alla **Enable Non-Case-Sensitive Username**(Abilita nome utente senza distinzione maiuscole/minuscole).</span><span class="sxs-lookup"><span data-stu-id="1051a-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="1051a-217">c.Fare clic su **Save**(Salva).</span><span class="sxs-lookup"><span data-stu-id="1051a-217">c.Click **Save**.</span></span>
   
    ![Configura accesso Single Sign-On][29]

    > [!NOTE] 
    > <span data-ttu-id="1051a-219">Se si prova ad abilitare questa opzione, il sistema controlla se verrà creato un nome di account di accesso SAML duplicato.</span><span class="sxs-lookup"><span data-stu-id="1051a-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="1051a-220">Ad esempio, se il cliente ha nomi utente Utente1 e utente1.</span><span class="sxs-lookup"><span data-stu-id="1051a-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="1051a-221">L'annullamento della distinzione maiuscole/minuscole crea questi duplicati.</span><span class="sxs-lookup"><span data-stu-id="1051a-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="1051a-222">Il sistema visualizza un messaggio di errore e non abilita la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1051a-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="1051a-223">Il cliente dovrà modificare uno dei nomi utente in modo che sia effettivamente scritto diversamente.</span><span class="sxs-lookup"><span data-stu-id="1051a-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="1051a-224">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1051a-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Applicazioni][14]
2. <span data-ttu-id="1051a-226">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="1051a-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applicazioni][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1051a-228">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="1051a-229">Questa sezione descrive come creare un utente di test chiamato Britta Simon nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="1051a-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][16]

<span data-ttu-id="1051a-231">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1051a-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1051a-232">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1051a-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD][17]
2. <span data-ttu-id="1051a-234">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="1051a-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1051a-235">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="1051a-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD][18]
4. <span data-ttu-id="1051a-237">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="1051a-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD][19]
5. <span data-ttu-id="1051a-239">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1051a-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][20]
   
    <span data-ttu-id="1051a-241">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-241">a.</span></span> <span data-ttu-id="1051a-242">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1051a-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="1051a-243">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-243">b.</span></span> <span data-ttu-id="1051a-244">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1051a-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="1051a-245">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-245">c.</span></span> <span data-ttu-id="1051a-246">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1051a-246">Click **Next**.</span></span>
6. <span data-ttu-id="1051a-247">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1051a-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][21]
   
    <span data-ttu-id="1051a-249">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-249">a.</span></span> <span data-ttu-id="1051a-250">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1051a-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="1051a-251">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-251">b.</span></span> <span data-ttu-id="1051a-252">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1051a-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="1051a-253">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-253">c.</span></span> <span data-ttu-id="1051a-254">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1051a-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="1051a-255">d.</span><span class="sxs-lookup"><span data-stu-id="1051a-255">d.</span></span> <span data-ttu-id="1051a-256">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1051a-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="1051a-257">e.</span><span class="sxs-lookup"><span data-stu-id="1051a-257">e.</span></span> <span data-ttu-id="1051a-258">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1051a-258">Click **Next**.</span></span>
7. <span data-ttu-id="1051a-259">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="1051a-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD][22]
8. <span data-ttu-id="1051a-261">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1051a-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][23]
   
    <span data-ttu-id="1051a-263">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-263">a.</span></span> <span data-ttu-id="1051a-264">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="1051a-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="1051a-265">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-265">b.</span></span> <span data-ttu-id="1051a-266">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="1051a-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="1051a-267">Creazione di un utente test SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="1051a-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="1051a-268">Per consentire agli utenti di Azure AD di accedere a SuccessFactors, è necessario eseguirne il provisioning in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="1051a-269">Nel caso di SuccessFactors, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1051a-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="1051a-270">Per creare utenti in SuccessFactors, è necessario contattare il [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="1051a-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1051a-271">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="1051a-272">Questa sezione descrive come abilitare Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Assegna utente][24]

<span data-ttu-id="1051a-274">**Per assegnare Britta Simon a SuccessFactors, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1051a-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="1051a-275">Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="1051a-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][25]
2. <span data-ttu-id="1051a-277">Nell'elenco di applicazioni, selezionare **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="1051a-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Configura accesso Single Sign-On][26]
3. <span data-ttu-id="1051a-279">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="1051a-279">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][27]
4. <span data-ttu-id="1051a-281">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1051a-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1051a-282">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="1051a-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="1051a-284">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1051a-284">Testing single sign-on</span></span>
<span data-ttu-id="1051a-285">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1051a-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1051a-286">Quando si fa clic sul riquadro SuccessFactors nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="1051a-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1051a-287">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1051a-287">Additional resources</span></span>
* [<span data-ttu-id="1051a-288">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1051a-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1051a-289">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1051a-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
