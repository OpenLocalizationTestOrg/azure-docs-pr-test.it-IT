---
title: 'Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Questetra BPM Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="97583-103">Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="97583-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="97583-104">Questa esercitazione descrive l'integrazione di Questetra BPM Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97583-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="97583-105">L'integrazione di Questetra BPM Suite con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="97583-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="97583-106">È possibile controllare in Azure AD chi può accedere a Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="97583-107">È possibile abilitare gli utenti per l'accesso automatico a Questetra BPM Suite (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="97583-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="97583-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="97583-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97583-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97583-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="97583-110">Prerequisites</span></span>
<span data-ttu-id="97583-111">Per configurare l'integrazione di Azure AD con Questetra BPM Suite, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="97583-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="97583-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-112">An Azure AD subscription</span></span>
* <span data-ttu-id="97583-113">Sottoscrizione di [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="97583-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97583-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="97583-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="97583-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="97583-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="97583-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="97583-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="97583-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97583-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="97583-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="97583-118">Scenario Description</span></span>
<span data-ttu-id="97583-119">L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="97583-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="97583-120">Lo scenario descritto in questa esercitazione è costituito da tre blocchi principali:</span><span class="sxs-lookup"><span data-stu-id="97583-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="97583-121">Aggiunta di Questetra BPM Suite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="97583-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="97583-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97583-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="97583-123">Aggiunta di Questetra BPM Suite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="97583-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="97583-124">Per configurare l'integrazione di Questetra BPM Suite in Azure AD, è necessario aggiungere Questetra BPM Suite dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="97583-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97583-125">**Per aggiungere Questetra BPM Suite dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="97583-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97583-126">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="97583-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="97583-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="97583-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="97583-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="97583-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="97583-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="97583-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="97583-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="97583-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="97583-135">Nella casella di ricerca digitare **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="97583-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="97583-137">Nel riquadro dei risultati selezionare **Questetra BPM Suite** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97583-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97583-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97583-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97583-139">Questa sezione descrive come configurare e testare l'accesso Single Sign-On di Azure AD con Questetra BPM Suite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="97583-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="97583-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Questetra BPM Suite che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="97583-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="97583-142">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **nome utente** in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="97583-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Questetra BPM Suite, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="97583-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97583-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="97583-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97583-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97583-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97583-146">**[Creazione di un utente test di Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)** : per avere una controparte di Britta Simon in Questetra BPM Suite collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="97583-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97583-148">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="97583-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97583-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97583-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="97583-150">Questa sezione descrive come abilitare Single Sign-On di Azure AD nel portale di Azure classico e configurare l'accesso Single Sign-On nell'applicazione Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="97583-151">**Per configurare Single Sign-On di Azure AD con Questetra BPM Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="97583-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="97583-152">Nella pagina di integrazione dell'applicazione **Questetra BPM Suite** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="97583-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][8]

2. <span data-ttu-id="97583-154">Nella pagina **How would you like users to sign on to Questetra BPM Suite** (Stabilire come si desidera che gli utenti accedano a Questetra BPM Suite) selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="97583-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. <span data-ttu-id="97583-156">In un'altra finestra del Web browser accedere al sito aziendale di **Questetra BPM Suite** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="97583-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="97583-157">Nel menu in alto fare clic su **System Settings**(Impostazioni di sistema).</span><span class="sxs-lookup"><span data-stu-id="97583-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][10]

5. <span data-ttu-id="97583-159">Per aprire la pagina **SingleSignOnSAML** fare clic su **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="97583-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][11]

6. <span data-ttu-id="97583-161">Nella pagina della finestra di dialogo **Configurare le impostazioni dell'app** del portale di Azure classico seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configurare le impostazioni dell'app][13]
   
    <span data-ttu-id="97583-163">a.</span><span class="sxs-lookup"><span data-stu-id="97583-163">a.</span></span> <span data-ttu-id="97583-164">Nella sezione SP Information (Informazioni SP) del sito aziendale di **Questetra BPM Suite** copiare il valore dell'**URL del servizio contenitore di Azure** e incollarlo nella casella di testo **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="97583-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="97583-165">b.</span><span class="sxs-lookup"><span data-stu-id="97583-165">b.</span></span> <span data-ttu-id="97583-166">Nella sezione SP Information (Informazioni SP) del sito aziendale di **Questetra BPM Suite** copiare il valore dell'**ID entità** e incollarlo nella casella di testo **URL autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="97583-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="97583-167">c.</span><span class="sxs-lookup"><span data-stu-id="97583-167">c.</span></span> <span data-ttu-id="97583-168">Nella sezione SP Information (Informazioni SP) del sito aziendale di **Questetra BPM Suite** copiare il valore dell'**URL del servizio contenitore di Azure** e incollarlo nella casella di testo **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="97583-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="97583-169">d.</span><span class="sxs-lookup"><span data-stu-id="97583-169">d.</span></span> <span data-ttu-id="97583-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="97583-170">Click **Next**.</span></span>

7. <span data-ttu-id="97583-171">Nella pagina **Configure single sign-on at Questetra BPM Suite** (Configura accesso Single Sign-On in Questetra BPM Suite) fare clic su **Scarica certificato** e quindi salvare il file del certificato localmente nel computer.</span><span class="sxs-lookup"><span data-stu-id="97583-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configura accesso Single Sign-On][14]

8. <span data-ttu-id="97583-173">Nel sito aziendale di **Questetra BPM Suite** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][15]
   
    <span data-ttu-id="97583-175">a.</span><span class="sxs-lookup"><span data-stu-id="97583-175">a.</span></span> <span data-ttu-id="97583-176">Selezionare **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="97583-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="97583-177">b.</span><span class="sxs-lookup"><span data-stu-id="97583-177">b.</span></span> <span data-ttu-id="97583-178">Nel portale di Azure classico copiare il valore dell'**URL autorità di certificazione** e incollarlo nella casella di testo **ID entità**.</span><span class="sxs-lookup"><span data-stu-id="97583-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="97583-179">c.</span><span class="sxs-lookup"><span data-stu-id="97583-179">c.</span></span> <span data-ttu-id="97583-180">Nel portale di Azure classico copiare il valore dell'**URL servizio Single Sign-On** e incollarlo nella casella di testo **URL pagina di accesso**.</span><span class="sxs-lookup"><span data-stu-id="97583-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="97583-181">d.</span><span class="sxs-lookup"><span data-stu-id="97583-181">d.</span></span> <span data-ttu-id="97583-182">Nel portale di Azure classico copiare il valore dell'**URL servizio Single Sign-Out** e incollarlo nella casella di testo **Sign-out page URL** (URL pagina di disconnessione).</span><span class="sxs-lookup"><span data-stu-id="97583-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="97583-183">e.</span><span class="sxs-lookup"><span data-stu-id="97583-183">e.</span></span> <span data-ttu-id="97583-184">Nella casella di testo **NameID format** (Formato ID nome) digitare **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="97583-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="97583-185">f.</span><span class="sxs-lookup"><span data-stu-id="97583-185">f.</span></span> <span data-ttu-id="97583-186">Creare un file con codifica Base 64 dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="97583-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="97583-187">Per informazioni dettagliate, vedere il video che illustra [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="97583-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="97583-188">g.</span><span class="sxs-lookup"><span data-stu-id="97583-188">g.</span></span> <span data-ttu-id="97583-189">Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **Validation certificate** .</span><span class="sxs-lookup"><span data-stu-id="97583-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="97583-190">h.</span><span class="sxs-lookup"><span data-stu-id="97583-190">h.</span></span> <span data-ttu-id="97583-191">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="97583-191">Click **Save**.</span></span>

1. <span data-ttu-id="97583-192">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="97583-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Cos'è Azure AD Connect][17]

2. <span data-ttu-id="97583-194">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="97583-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Cos'è Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97583-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97583-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="97583-197">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="97583-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="97583-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="97583-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97583-199">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="97583-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creare un utente test di Azure AD][100] 

2. <span data-ttu-id="97583-201">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="97583-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="97583-202">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="97583-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creare un utente test di Azure AD][101] 

4. <span data-ttu-id="97583-204">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="97583-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creare un utente test di Azure AD][102] 

5. <span data-ttu-id="97583-206">Nella pagina della finestra di dialogo **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creare un utente test di Azure AD][103]
   
    <span data-ttu-id="97583-208">a.</span><span class="sxs-lookup"><span data-stu-id="97583-208">a.</span></span> <span data-ttu-id="97583-209">In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="97583-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="97583-210">b.</span><span class="sxs-lookup"><span data-stu-id="97583-210">b.</span></span> <span data-ttu-id="97583-211">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97583-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="97583-212">c.</span><span class="sxs-lookup"><span data-stu-id="97583-212">c.</span></span> <span data-ttu-id="97583-213">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="97583-213">Click Next.</span></span>

6. <span data-ttu-id="97583-214">Nella pagina della finestra di dialogo **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creare un utente test di Azure AD][104] 
   
    <span data-ttu-id="97583-216">a.</span><span class="sxs-lookup"><span data-stu-id="97583-216">a.</span></span> <span data-ttu-id="97583-217">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="97583-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="97583-218">b.</span><span class="sxs-lookup"><span data-stu-id="97583-218">b.</span></span> <span data-ttu-id="97583-219">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="97583-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="97583-220">c.</span><span class="sxs-lookup"><span data-stu-id="97583-220">c.</span></span> <span data-ttu-id="97583-221">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="97583-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="97583-222">d.</span><span class="sxs-lookup"><span data-stu-id="97583-222">d.</span></span> <span data-ttu-id="97583-223">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="97583-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="97583-224">e.</span><span class="sxs-lookup"><span data-stu-id="97583-224">e.</span></span> <span data-ttu-id="97583-225">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="97583-225">Click **Next**.</span></span>

7. <span data-ttu-id="97583-226">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="97583-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creare un utente test di Azure AD][105]  

8. <span data-ttu-id="97583-228">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creare un utente test di Azure AD][106]   
   
    <span data-ttu-id="97583-230">a.</span><span class="sxs-lookup"><span data-stu-id="97583-230">a.</span></span> <span data-ttu-id="97583-231">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="97583-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="97583-232">b.</span><span class="sxs-lookup"><span data-stu-id="97583-232">b.</span></span> <span data-ttu-id="97583-233">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="97583-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="97583-234">Creazione di un utente test di Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="97583-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="97583-235">Questa sezione descrive come creare un utente chiamato Britta Simon in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="97583-236">**Per creare un utente test denominato Britta Simon in Questetra BPM Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="97583-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="97583-237">Accedere al sito aziendale di Questetra BPM Suite come amministratore.</span><span class="sxs-lookup"><span data-stu-id="97583-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="97583-238">Scegliere **Impostazioni di sistema > Elenco utenti > Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="97583-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="97583-239">Nella finestra di dialogo New User (Nuovo utente) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97583-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Creare un utente test][300] 
   
    <span data-ttu-id="97583-241">a.</span><span class="sxs-lookup"><span data-stu-id="97583-241">a.</span></span> <span data-ttu-id="97583-242">Nella casella di testo **Name** digitare il nome utente di Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="97583-243">b.</span><span class="sxs-lookup"><span data-stu-id="97583-243">b.</span></span> <span data-ttu-id="97583-244">Nella casella di testo **Email** digitare il nome utente di Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97583-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="97583-245">c.</span><span class="sxs-lookup"><span data-stu-id="97583-245">c.</span></span> <span data-ttu-id="97583-246">Nella casella di testo **Password** digitare una password.</span><span class="sxs-lookup"><span data-stu-id="97583-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="97583-247">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="97583-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97583-248">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97583-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="97583-249">Questa sezione descrive come abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Cos'è Azure AD Connect][200]

<span data-ttu-id="97583-251">**Per assegnare Britta Simon a Questetra BPM Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="97583-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="97583-252">Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory scegliere **Applicazioni** dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="97583-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Cos'è Azure AD Connect][201]
2. <span data-ttu-id="97583-254">Nell'elenco delle applicazioni selezionare **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="97583-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Cos'è Azure AD Connect][205]
3. <span data-ttu-id="97583-256">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="97583-256">In the menu on the top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][202]
4. <span data-ttu-id="97583-258">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="97583-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Cos'è Azure AD Connect][203]
5. <span data-ttu-id="97583-260">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="97583-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Cos'è Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="97583-262">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="97583-262">Testing Single Sign-On</span></span>
<span data-ttu-id="97583-263">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97583-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="97583-264">Quando si fa clic sul riquadro Questetra BPM Suite nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="97583-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97583-265">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="97583-265">Additional Resources</span></span>
* [<span data-ttu-id="97583-266">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97583-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97583-267">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97583-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
