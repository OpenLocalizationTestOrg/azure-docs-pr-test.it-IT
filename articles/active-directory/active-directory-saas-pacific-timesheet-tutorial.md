---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pacific Timesheet | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Pacific Timesheet.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: fda06c340430d19bea035a2cab2f318fe8a5998c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="2e908-103">Esercitazione: Integrazione di Azure Active Directory con Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="2e908-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="2e908-104">Questa esercitazione descrive come integrare Pacific Timesheet con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e908-104">In this tutorial, you learn how to integrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e908-105">L'integrazione di Pacific Timesheet con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e908-105">Integrating Pacific Timesheet with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e908-106">È possibile controllare in Azure AD chi può accedere a Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="2e908-106">You can control in Azure AD who has access to Pacific Timesheet</span></span>
- <span data-ttu-id="2e908-107">È possibile abilitare gli utenti per l'accesso automatico a Pacific Timesheet (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-107">You can enable your users to automatically get signed-on to Pacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e908-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e908-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2e908-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e908-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e908-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2e908-110">Prerequisites</span></span>

<span data-ttu-id="2e908-111">Per configurare l'integrazione di Azure AD con Pacific Timesheet sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e908-111">To configure Azure AD integration with Pacific Timesheet, you need the following items:</span></span>

- <span data-ttu-id="2e908-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e908-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e908-113">Sottoscrizione di Pacific Timesheet abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e908-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e908-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2e908-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e908-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e908-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e908-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2e908-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e908-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e908-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e908-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2e908-118">Scenario description</span></span>
<span data-ttu-id="2e908-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2e908-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e908-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e908-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e908-121">Aggiunta di Pacific Timesheet dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2e908-121">Adding Pacific Timesheet from the gallery</span></span>
2. <span data-ttu-id="2e908-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-the-gallery"></a><span data-ttu-id="2e908-123">Aggiunta di Pacific Timesheet dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2e908-123">Adding Pacific Timesheet from the gallery</span></span>
<span data-ttu-id="2e908-124">Per configurare l'integrazione di Pacific Timesheet in Azure AD, è necessario aggiungere Pacific Timesheet dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2e908-124">To configure the integration of Pacific Timesheet into Azure AD, you need to add Pacific Timesheet from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e908-125">**Per aggiungere Pacific Timesheet dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e908-125">**To add Pacific Timesheet from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e908-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2e908-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e908-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2e908-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e908-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e908-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2e908-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="2e908-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2e908-133">Nella casella di ricerca digitare **Pacific Timesheet**.</span><span class="sxs-lookup"><span data-stu-id="2e908-133">In the search box, type **Pacific Timesheet**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="2e908-135">Nel pannello dei risultati selezionare **Pacific Timesheet** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2e908-135">In the results panel, select **Pacific Timesheet**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e908-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e908-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pacific Timesheet con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e908-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e908-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Pacific Timesheet che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e908-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pacific Timesheet is to a user in Azure AD.</span></span> <span data-ttu-id="2e908-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="2e908-140">In other words, a link relationship between an Azure AD user and the related user in Pacific Timesheet needs to be established.</span></span>

<span data-ttu-id="2e908-141">Per stabilire la relazione di collegamento, in Pacific Timesheet assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="2e908-141">In Pacific Timesheet, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e908-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Pacific Timesheet è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e908-142">To configure and test Azure AD single sign-on with Pacific Timesheet, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e908-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2e908-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e908-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e908-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e908-145">**[Creazione di un utente test di Pacific Timesheet](#creating-a-pacific-timesheet-test-user)**: per avere una controparte di Britta Simon in Pacific Timesheet collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e908-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - to have a counterpart of Britta Simon in Pacific Timesheet that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e908-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e908-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e908-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2e908-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e908-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e908-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="2e908-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="2e908-150">**Per configurare l'accesso Single Sign-On di Azure AD con Pacific Timesheet, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e908-150">**To configure Azure AD single sign-on with Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="2e908-151">Nella pagina di integrazione dell'applicazione **Pacific Timesheet** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2e908-151">In the Azure portal, on the **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2e908-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2e908-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="2e908-155">Nella sezione **URL e dominio Pacific Timesheet** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e908-155">On the **Pacific Timesheet Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="2e908-157">a.</span><span class="sxs-lookup"><span data-stu-id="2e908-157">a.</span></span> <span data-ttu-id="2e908-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="2e908-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="2e908-159">b.</span><span class="sxs-lookup"><span data-stu-id="2e908-159">b.</span></span> <span data-ttu-id="2e908-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="2e908-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e908-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2e908-161">These values are not real.</span></span> <span data-ttu-id="2e908-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="2e908-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2e908-163">Per ottenere questi valori, contattare il [team di supporto clienti di Pacific Timesheet](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="2e908-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to get these values.</span></span>
 
4. <span data-ttu-id="2e908-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="2e908-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="2e908-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2e908-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e908-168">Nella sezione **Configurazione Pacific Timesheet** fare clic su **Configure Pacific Timesheet** (Configura Pacific Timesheet) per aprire la finestra **Configure sign-on** (Configura accesso sign-on).</span><span class="sxs-lookup"><span data-stu-id="2e908-168">On the **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2e908-169">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="2e908-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="2e908-171">Per configurare l'accesso Single Sign-On sul lato **Pacific Timesheet**, è necessario inviare il file **Certificato (Base64)** scaricato, l'**URL del servizio Single Sign-On SAML** e l'**ID di entità SAML** al [team di supporto di Pacific Timesheet](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="2e908-171">To configure single sign-on on **Pacific Timesheet** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="2e908-172">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="2e908-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2e908-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2e908-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2e908-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="2e908-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2e908-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e908-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e908-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e908-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e908-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2e908-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e908-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e908-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2e908-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e908-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2e908-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e908-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2e908-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e908-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e908-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e908-188">a.</span><span class="sxs-lookup"><span data-stu-id="2e908-188">a.</span></span> <span data-ttu-id="2e908-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e908-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e908-190">b.</span><span class="sxs-lookup"><span data-stu-id="2e908-190">b.</span></span> <span data-ttu-id="2e908-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2e908-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e908-192">c.</span><span class="sxs-lookup"><span data-stu-id="2e908-192">c.</span></span> <span data-ttu-id="2e908-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2e908-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e908-194">d.</span><span class="sxs-lookup"><span data-stu-id="2e908-194">d.</span></span> <span data-ttu-id="2e908-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2e908-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="2e908-196">Creazione di un utente di test di Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="2e908-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="2e908-197">In questa sezione viene creato un utente di nome Britta Simon in Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="2e908-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="2e908-198">Collaborare con il [team di supporto di Pacific Timesheet](http://www.pacifictimesheet.com/support) per creare un utente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2e908-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to create a user in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e908-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e908-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e908-200">In questa sezione, Britta Simon viene abilitata all'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="2e908-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pacific Timesheet.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2e908-202">**Per assegnare Britta Simon a Pacific Timesheet, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e908-202">**To assign Britta Simon to Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="2e908-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e908-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2e908-205">Nell'elenco di applicazioni selezionare **Pacific Timesheet**.</span><span class="sxs-lookup"><span data-stu-id="2e908-205">In the applications list, select **Pacific Timesheet**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="2e908-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2e908-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2e908-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2e908-209">Click **Add** button.</span></span> <span data-ttu-id="2e908-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e908-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2e908-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2e908-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e908-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2e908-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e908-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e908-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e908-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e908-215">Testing single sign-on</span></span>

<span data-ttu-id="2e908-216">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2e908-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e908-217">Quando si fa clic sul riquadro Pacific Timesheet nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="2e908-217">When you click the Pacific Timesheet tile in the Access Panel, you should get automatically signed-on to your Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e908-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2e908-218">Additional resources</span></span>

* [<span data-ttu-id="2e908-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e908-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e908-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e908-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

