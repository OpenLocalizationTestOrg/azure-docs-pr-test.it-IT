---
title: 'Esercitazione: Integrazione di Azure Active Directory con Birst Agile Business Analytics | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Birst Agile Business Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="fa748-103">Esercitazione: Integrazione di Azure Active Directory con Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="fa748-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="fa748-104">Questa esercitazione descrive come integrare Birst Agile Business Analytics con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa748-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa748-105">L'integrazione di Birst Agile Business Analytics con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa748-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fa748-106">È possibile controllare in Azure AD chi può accedere a Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="fa748-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="fa748-107">È possibile abilitare gli utenti per l'accesso automatico a Birst Agile Business Analytics (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa748-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa748-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fa748-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa748-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa748-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fa748-110">Prerequisites</span></span>

<span data-ttu-id="fa748-111">Per configurare l'integrazione di Azure AD con Birst Agile Business Analytics, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa748-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="fa748-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa748-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa748-113">Sottoscrizione di Birst Agile Business Analytics abilitata all'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fa748-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa748-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fa748-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa748-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa748-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa748-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fa748-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa748-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa748-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa748-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fa748-118">Scenario description</span></span>
<span data-ttu-id="fa748-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fa748-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa748-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa748-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa748-121">Aggiunta di Birst Agile Business Analytics dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fa748-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="fa748-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="fa748-123">Aggiunta di Birst Agile Business Analytics dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fa748-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="fa748-124">Per configurare l'integrazione di Birst Agile Business Analytics in Azure AD, è necessario aggiungere Birst Agile Business Analytics dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fa748-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fa748-125">**Per aggiungere Birst Agile Business Analytics dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fa748-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fa748-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fa748-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa748-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fa748-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fa748-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa748-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fa748-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa748-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fa748-133">Nella casella di ricerca digitare **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fa748-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="fa748-135">Nel pannello dei risultati selezionare **Birst Agile Business Analytics** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa748-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa748-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa748-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Birst Agile Business Analytics usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fa748-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fa748-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Birst Agile Business Analytics corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa748-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="fa748-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa748-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="fa748-141">Per stabilire la relazione di collegamento, in Birst Agile Business Analytics assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="fa748-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fa748-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Birst Agile Business Analytics, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa748-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fa748-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fa748-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fa748-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa748-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa748-145">**[Creazione di un utente di test di Birst Agile Business Analytics](#creating-a-birst-agile-business-analytics-test-user)**: per avere una controparte di Britta Simon in Birst Agile Business Analytics collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa748-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa748-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa748-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa748-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="fa748-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa748-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa748-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa748-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="fa748-150">**Per configurare l'accesso Single Sign-On di Azure AD con Birst Agile Business Analytics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fa748-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="fa748-151">Nella pagina di integrazione dell'applicazione **Birst Agile Business Analytics** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fa748-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fa748-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fa748-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="fa748-155">Nella sezione **URL e dominio Birst Agile Business Analytics** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fa748-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="fa748-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fa748-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="fa748-158">L'URL dipende dal data center in cui si trova l'account Birst:</span><span class="sxs-lookup"><span data-stu-id="fa748-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="fa748-159">Se il data center si trova negli Stati Uniti, usare il modello seguente: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fa748-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="fa748-160">Se il data center si trova in Europa, usare il modello seguente: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fa748-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa748-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="fa748-161">This value is not real.</span></span> <span data-ttu-id="fa748-162">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="fa748-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fa748-163">Per ottenere questo valore, contattare il [team di supporto clienti di Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="fa748-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="fa748-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="fa748-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="fa748-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fa748-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa748-168">Nella sezione **Configurazione di Birst Agile Business Analytics** fare clic su **Configura Birst Agile Business Analytics** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="fa748-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fa748-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="fa748-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="fa748-171">Per configurare l'accesso Single Sign-On sul lato **Birst Agile Business Analytics**, è necessario inviare il file **Certificato (Base64)** scaricato, l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="fa748-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="fa748-172">Segnalare al team Birst che questa integrazione richiede l'algoritmo SHA256 (SHA1 non sarà supportato), in modo che il team possa impostare l'accesso Single Sign-On nel server appropriato, ad esempio **app2101** e così via.</span><span class="sxs-lookup"><span data-stu-id="fa748-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="fa748-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="fa748-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fa748-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="fa748-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fa748-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa748-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa748-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa748-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa748-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fa748-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa748-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fa748-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fa748-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa748-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="fa748-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa748-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="fa748-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa748-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fa748-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa748-188">a.</span><span class="sxs-lookup"><span data-stu-id="fa748-188">a.</span></span> <span data-ttu-id="fa748-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa748-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa748-190">b.</span><span class="sxs-lookup"><span data-stu-id="fa748-190">b.</span></span> <span data-ttu-id="fa748-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa748-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa748-192">c.</span><span class="sxs-lookup"><span data-stu-id="fa748-192">c.</span></span> <span data-ttu-id="fa748-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="fa748-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fa748-194">d.</span><span class="sxs-lookup"><span data-stu-id="fa748-194">d.</span></span> <span data-ttu-id="fa748-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fa748-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="fa748-196">Creazione di un utente test di Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="fa748-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="fa748-197">Questa sezione descrive come creare un utente chiamato Britta Simon in Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa748-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="fa748-198">Collaborare con il [team di supporto di Birst Agile Business Analytics](mailto:info@birst.com) per aggiungere gli utenti all'account Birst.</span><span class="sxs-lookup"><span data-stu-id="fa748-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fa748-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa748-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fa748-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa748-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fa748-202">**Per assegnare Britta Simon a Birst Agile Business Analytics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fa748-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="fa748-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa748-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fa748-205">Nell'elenco di applicazioni selezionare **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fa748-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="fa748-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fa748-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fa748-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fa748-209">Click **Add** button.</span></span> <span data-ttu-id="fa748-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa748-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fa748-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="fa748-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fa748-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fa748-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa748-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa748-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa748-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fa748-215">Testing single sign-on</span></span>

<span data-ttu-id="fa748-216">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fa748-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="fa748-217">Quando si fa clic sul riquadro Birst Agile Business Analytics nel pannello di accesso, viene effettuato automaticamente l'accesso all'applicazione Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa748-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fa748-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fa748-218">Additional resources</span></span>

* [<span data-ttu-id="fa748-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa748-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa748-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa748-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

