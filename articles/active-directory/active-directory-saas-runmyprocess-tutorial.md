---
title: 'Esercitazione: Integrazione di Azure Active Directory con RunMyProcess | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="5a91f-103">Esercitazione: Integrazione di Azure Active Directory con RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a91f-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="5a91f-104">Questa esercitazione descrive come integrare RunMyProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a91f-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a91f-105">L'integrazione di RunMyProcess con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a91f-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5a91f-106">È possibile controllare in Azure AD chi può accedere a RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a91f-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="5a91f-107">È possibile abilitare gli utenti per l'accesso automatico a RunMyProcess (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a91f-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a91f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5a91f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a91f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a91f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5a91f-110">Prerequisites</span></span>

<span data-ttu-id="5a91f-111">Per configurare l'integrazione di Azure AD con RunMyProcess, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a91f-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="5a91f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a91f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a91f-113">Sottoscrizione di RunMyProcess abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5a91f-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a91f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5a91f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a91f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a91f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a91f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5a91f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a91f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a91f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a91f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5a91f-118">Scenario description</span></span>
<span data-ttu-id="5a91f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5a91f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a91f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a91f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a91f-121">Aggiunta di RunMyProcess dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5a91f-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="5a91f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="5a91f-123">Aggiunta di RunMyProcess dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5a91f-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="5a91f-124">Per configurare l'integrazione di RunMyProcess in Azure AD, è necessario aggiungere RunMyProcess dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5a91f-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5a91f-125">**Per aggiungere RunMyProcess dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5a91f-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5a91f-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5a91f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a91f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5a91f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5a91f-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="5a91f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5a91f-133">Nella casella di ricerca digitare **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-133">In the search box, type **RunMyProcess**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="5a91f-135">Nel pannello dei risultati selezionare **RunMyProcess** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5a91f-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a91f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a91f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RunMyProcess in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5a91f-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a91f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di RunMyProcess che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a91f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="5a91f-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a91f-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="5a91f-141">Per stabilire la relazione di collegamento, in RunMyProcess assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5a91f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con RunMyProcess, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a91f-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5a91f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5a91f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5a91f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a91f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a91f-145">**[Creazione di un utente di test di RunMyProcess](#creating-a-runmyprocess-test-user)**: per avere una controparte di Britta Simon in RunMyProcess collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a91f-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a91f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a91f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a91f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="5a91f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a91f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a91f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a91f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="5a91f-150">**Per configurare l'accesso Single Sign-On di Azure AD con RunMyProcess, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5a91f-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5a91f-151">Nella pagina di integrazione dell'applicazione **RunMyProcess** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5a91f-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5a91f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="5a91f-155">Nella sezione **URL e dominio RunMyProcess** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5a91f-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="5a91f-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="5a91f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a91f-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="5a91f-158">The value is not real.</span></span> <span data-ttu-id="5a91f-159">aggiornarlo con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="5a91f-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="5a91f-160">Per ottenere il valore, contattare il [team di supporto client di RunMyProcess](mailto:support@runmyprocess.com).</span><span class="sxs-lookup"><span data-stu-id="5a91f-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="5a91f-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="5a91f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="5a91f-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5a91f-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a91f-165">Nella sezione **Configurazione di RunMyProcess** fare clic su **Configura RunMyProcess** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5a91f-166">Copiare **l'URL di disconnessione e l'URL servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="5a91f-168">In un'altra finestra del Web browser accedere al tenant di RunMyProcess come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5a91f-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="5a91f-169">Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Configuration** (Configurazione).</span><span class="sxs-lookup"><span data-stu-id="5a91f-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="5a91f-171">Passare alla sezione **Authentication method** (Metodo di autenticazione) e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5a91f-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="5a91f-173">a.</span><span class="sxs-lookup"><span data-stu-id="5a91f-173">a.</span></span> <span data-ttu-id="5a91f-174">In **Metodo** selezionare **SSO con Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="5a91f-175">b.</span><span class="sxs-lookup"><span data-stu-id="5a91f-175">b.</span></span> <span data-ttu-id="5a91f-176">Nella casella di testo **SSO redirect** (Reindirizzamento SSO) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a91f-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a91f-177">c.</span><span class="sxs-lookup"><span data-stu-id="5a91f-177">c.</span></span> <span data-ttu-id="5a91f-178">Nella casella di testo **Logout redirect** (Reindirizzamento disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a91f-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a91f-179">d.</span><span class="sxs-lookup"><span data-stu-id="5a91f-179">d.</span></span> <span data-ttu-id="5a91f-180">Nella casella di testo **Formato ID nome** digitare il valore di **Formato identificatore nome** come **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="5a91f-181">e.</span><span class="sxs-lookup"><span data-stu-id="5a91f-181">e.</span></span> <span data-ttu-id="5a91f-182">Copiare il contenuto del file del certificato scaricato e incollarlo nella casella di testo **Certificate** (Certificato).</span><span class="sxs-lookup"><span data-stu-id="5a91f-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="5a91f-183">f.</span><span class="sxs-lookup"><span data-stu-id="5a91f-183">f.</span></span> <span data-ttu-id="5a91f-184">Fare clic sull'icona di **salvataggio**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="5a91f-185">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="5a91f-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5a91f-186">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="5a91f-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5a91f-187">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a91f-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a91f-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a91f-189">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a91f-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5a91f-191">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a91f-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5a91f-192">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5a91f-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a91f-194">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="5a91f-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a91f-196">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a91f-198">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5a91f-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a91f-200">a.</span><span class="sxs-lookup"><span data-stu-id="5a91f-200">a.</span></span> <span data-ttu-id="5a91f-201">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a91f-202">b.</span><span class="sxs-lookup"><span data-stu-id="5a91f-202">b.</span></span> <span data-ttu-id="5a91f-203">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5a91f-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a91f-204">c.</span><span class="sxs-lookup"><span data-stu-id="5a91f-204">c.</span></span> <span data-ttu-id="5a91f-205">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5a91f-206">d.</span><span class="sxs-lookup"><span data-stu-id="5a91f-206">d.</span></span> <span data-ttu-id="5a91f-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="5a91f-208">Creazione di un utente test di RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a91f-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="5a91f-209">Per consentire agli utenti di Azure AD di accedere a RunMyProcess, è necessario eseguirne il provisioning in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a91f-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="5a91f-210">Nel caso di RunMyProcess, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5a91f-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="5a91f-211">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5a91f-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5a91f-212">Accedere al sito aziendale di RunMyProcess come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5a91f-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="5a91f-213">Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Users** (Utenti), quindi fare clic su **New User** (Nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="5a91f-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="5a91f-214">![Nuovo utente](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="5a91f-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="5a91f-215">Nella sezione **Impostazioni utente** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a91f-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5a91f-216">![Profilo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profilo")</span><span class="sxs-lookup"><span data-stu-id="5a91f-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="5a91f-217">a.</span><span class="sxs-lookup"><span data-stu-id="5a91f-217">a.</span></span> <span data-ttu-id="5a91f-218">Digitare il **nome** e l'**indirizzo di posta elettronica** di un account di Azure AD valido di cui si desidera eseguire il provisioning nelle relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="5a91f-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="5a91f-219">b.</span><span class="sxs-lookup"><span data-stu-id="5a91f-219">b.</span></span> <span data-ttu-id="5a91f-220">Selezionare una **lingua IDE**, una **lingua** e un **profilo**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="5a91f-221">c.</span><span class="sxs-lookup"><span data-stu-id="5a91f-221">c.</span></span> <span data-ttu-id="5a91f-222">Selezionare **Inviami un messaggio di posta elettronica di creazione account**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="5a91f-223">d.</span><span class="sxs-lookup"><span data-stu-id="5a91f-223">d.</span></span> <span data-ttu-id="5a91f-224">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5a91f-225">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da RunMyProcess per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a91f-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5a91f-226">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a91f-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5a91f-227">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a91f-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5a91f-229">**Per assegnare Britta Simon a RunMyProcess, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5a91f-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5a91f-230">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5a91f-232">Nell'elenco di applicazioni selezionare **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="5a91f-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5a91f-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5a91f-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-236">Click **Add** button.</span></span> <span data-ttu-id="5a91f-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5a91f-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="5a91f-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5a91f-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a91f-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5a91f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a91f-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5a91f-242">Testing single sign-on</span></span>

<span data-ttu-id="5a91f-243">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5a91f-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5a91f-244">Quando si fa clic sul riquadro RunMyProcess nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a91f-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a91f-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5a91f-245">Additional resources</span></span>

* [<span data-ttu-id="5a91f-246">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a91f-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a91f-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a91f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

