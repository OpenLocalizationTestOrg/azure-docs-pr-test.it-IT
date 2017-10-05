---
title: 'Esercitazione: Integrazione di Azure Active Directory con Marketo | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="4c1aa-103">Esercitazione: Integrazione di Azure Active Directory con Marketo</span><span class="sxs-lookup"><span data-stu-id="4c1aa-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="4c1aa-104">Questa esercitazione descrive come integrare Marketo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c1aa-105">L'integrazione di Marketo con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c1aa-106">È possibile controllare in Azure AD chi può accedere a Marketo</span><span class="sxs-lookup"><span data-stu-id="4c1aa-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="4c1aa-107">È possibile abilitare gli utenti per l'accesso automatico a Marketo (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c1aa-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c1aa-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c1aa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c1aa-110">Prerequisites</span></span>

<span data-ttu-id="4c1aa-111">Per configurare l'integrazione di Azure AD con Marketo, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="4c1aa-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c1aa-113">Sottoscrizione di Marketo abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c1aa-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c1aa-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c1aa-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c1aa-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c1aa-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c1aa-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4c1aa-118">Scenario description</span></span>
<span data-ttu-id="4c1aa-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c1aa-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c1aa-121">Aggiunta di Marketo dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c1aa-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="4c1aa-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="4c1aa-123">Aggiunta di Marketo dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c1aa-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="4c1aa-124">Per configurare l'integrazione di Marketo in Azure AD, è necessario aggiungere Marketo dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c1aa-125">**Per aggiungere Marketo dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c1aa-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c1aa-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c1aa-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4c1aa-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4c1aa-133">Nella casella di ricerca digitare **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-133">In the search box, type **Marketo**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="4c1aa-135">Nel pannello dei risultati selezionare **Marketo** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c1aa-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c1aa-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Marketo mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c1aa-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c1aa-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Marketo che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="4c1aa-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="4c1aa-141">Per stabilire la relazione di collegamento, in Marketo assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c1aa-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Marketo, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c1aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c1aa-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c1aa-145">**[Creazione di un utente test di Marketo](#creating-a-marketo-test-user)**: per avere una controparte di Britta Simon in Marketo collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c1aa-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c1aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c1aa-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c1aa-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="4c1aa-150">**Per configurare l'accesso Single Sign-On di Azure AD con Marketo, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="4c1aa-151">Nella pagina di integrazione dell'applicazione **Marketo** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4c1aa-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="4c1aa-155">Nella sezione **URL e dominio Marketo** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="4c1aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-157">a.</span></span> <span data-ttu-id="4c1aa-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4c1aa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="4c1aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-159">b.</span></span> <span data-ttu-id="4c1aa-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="4c1aa-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c1aa-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4c1aa-161">These values are not real.</span></span> <span data-ttu-id="4c1aa-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4c1aa-163">Per ottenere questi valori contattare il [team di supporto di Marketo](http://investors.marketo.com/contactus.cfm).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="4c1aa-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="4c1aa-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4c1aa-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c1aa-168">Nella sezione **Configurazione di Marketo** fare clic su **Configura Marketo** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c1aa-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="4c1aa-171">Per ottenere l'ID Munchkin dell'applicazione, accedere a Marketo usando le credenziali di amministratore ed eseguire le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="4c1aa-172">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-172">a.</span></span> <span data-ttu-id="4c1aa-173">Accedere all'app Marketo usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4c1aa-174">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-174">b.</span></span> <span data-ttu-id="4c1aa-175">Fare clic sul pulsante **Admin** (Amministratore) nel riquadro di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4c1aa-177">c.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-177">c.</span></span> <span data-ttu-id="4c1aa-178">Passare al menu Integration (Integrazione) e fare clic sul **collegamento Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="4c1aa-180">d.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-180">d.</span></span> <span data-ttu-id="4c1aa-181">Copiare l'ID Munchkin visualizzato sullo schermo e completare il valore per l'URL di risposta nella configurazione guidata di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="4c1aa-183">Per configurare l'accesso Single Sign-On nell'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="4c1aa-184">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-184">a.</span></span> <span data-ttu-id="4c1aa-185">Accedere all'app Marketo usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4c1aa-186">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-186">b.</span></span> <span data-ttu-id="4c1aa-187">Fare clic sul pulsante **Admin** (Amministratore) nel riquadro di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4c1aa-189">c.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-189">c.</span></span> <span data-ttu-id="4c1aa-190">Passare al menu Integration (Integrazione) e fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="4c1aa-192">d.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-192">d.</span></span> <span data-ttu-id="4c1aa-193">Per abilitare le impostazioni SAML fare clic sul pulsante **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="4c1aa-195">e.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-195">e.</span></span> <span data-ttu-id="4c1aa-196">Impostazioni dell'accesso Single Sign-On **abilitate**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="4c1aa-197">f.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-197">f.</span></span> <span data-ttu-id="4c1aa-198">Incollare il valore **SAML Entity ID** (ID entità SAML) nella casella di testo **Issuer ID** (ID autorità emittente).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="4c1aa-199">g.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-199">g.</span></span> <span data-ttu-id="4c1aa-200">Nella casella di testo **Entity ID** (ID entità) immettere l'URL come `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="4c1aa-201">h.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-201">h.</span></span> <span data-ttu-id="4c1aa-202">Selezionare User ID Location (Percorso ID utente) come **elemento Name Identifier** (Identificatore nome).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="4c1aa-204">Se l'identificatore utente non è un valore UPN, modificarlo nella scheda degli attributi.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="4c1aa-205">i.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-205">i.</span></span> <span data-ttu-id="4c1aa-206">Caricare il certificato scaricato dalla configurazione guidata di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="4c1aa-207">Fare clic su **Save** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="4c1aa-208">j.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-208">j.</span></span> <span data-ttu-id="4c1aa-209">Modificare le impostazioni delle pagine di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="4c1aa-210">k.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-210">k.</span></span> <span data-ttu-id="4c1aa-211">Incollare **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) nella casella di testo **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="4c1aa-212">l.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-212">l.</span></span> <span data-ttu-id="4c1aa-213">Incollare il valore di **Sign-Out URL** (URL di disconnessione) nella casella di testo **URL disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="4c1aa-214">m.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-214">m.</span></span> <span data-ttu-id="4c1aa-215">In **Error URL** (URL errore) copiare l'**URL istanza** di Marketo e fare clic su **Save** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="4c1aa-217">Per abilitare l'accesso Single Sign-On per gli utenti, completare le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="4c1aa-218">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-218">a.</span></span> <span data-ttu-id="4c1aa-219">Accedere all'app Marketo usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4c1aa-220">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-220">b.</span></span> <span data-ttu-id="4c1aa-221">Fare clic sul pulsante **Admin** (Amministratore) nel riquadro di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4c1aa-223">c.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-223">c.</span></span> <span data-ttu-id="4c1aa-224">Passare al menu **Security** (Sicurezza) e fare clic su **Login Settings** (Impostazioni di accesso).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="4c1aa-226">d.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-226">d.</span></span> <span data-ttu-id="4c1aa-227">Selezionare l'opzione **Require SSO** (Richiedi SSO) e usare **Save** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="4c1aa-229">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c1aa-230">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c1aa-231">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c1aa-232">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1aa-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c1aa-233">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4c1aa-235">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c1aa-236">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c1aa-238">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c1aa-240">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c1aa-242">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c1aa-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c1aa-244">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-244">a.</span></span> <span data-ttu-id="4c1aa-245">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c1aa-246">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-246">b.</span></span> <span data-ttu-id="4c1aa-247">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c1aa-248">c.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-248">c.</span></span> <span data-ttu-id="4c1aa-249">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c1aa-250">d.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-250">d.</span></span> <span data-ttu-id="4c1aa-251">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="4c1aa-252">Creazione di un utente test di Marketo</span><span class="sxs-lookup"><span data-stu-id="4c1aa-252">Creating a Marketo test user</span></span>

<span data-ttu-id="4c1aa-253">In questa sezione viene creato un utente chiamato Britta Simon in Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="4c1aa-254">Seguire questa procedura per creare un utente nella piattaforma Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="4c1aa-255">Accedere all'app Marketo usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="4c1aa-256">Fare clic sul pulsante **Admin** (Amministratore) nel riquadro di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="4c1aa-258">Passare al menu **Security** (Sicurezza) e fare clic su **Users & Roles** (Utenti e ruoli).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="4c1aa-260">Fare clic sul collegamento **Invite New User** (Invita nuovo utente) nella scheda Users (Utenti).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="4c1aa-262">La procedura guidata (Invita nuovo utente) immetterà i valori per le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="4c1aa-263">a.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-263">a.</span></span> <span data-ttu-id="4c1aa-264">Immettere l'indirizzo di **Email** (Posta elettronica) dell'utente nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="4c1aa-266">b.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-266">b.</span></span> <span data-ttu-id="4c1aa-267">Immettere il valore per **First Name** (Nome) nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="4c1aa-268">c.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-268">c.</span></span> <span data-ttu-id="4c1aa-269">Immettere il valore per **Last Name** (Cognome) nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="4c1aa-270">d.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-270">d.</span></span> <span data-ttu-id="4c1aa-271">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-271">Click **Next**</span></span>

6. <span data-ttu-id="4c1aa-272">Nella scheda **Permissions** (Autorizzazioni) selezionare i **ruoli utente** e fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="4c1aa-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="4c1aa-274">Fare clic sul pulsante **Send** (Invia) per inoltrare l'invito all'utente.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="4c1aa-276">L'utente riceve la notifica tramite posta elettronica e deve fare clic sul collegamento e modificare la password per attivare l'account.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c1aa-277">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1aa-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c1aa-278">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4c1aa-280">**Per assegnare Britta Simon a Marketo, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c1aa-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="4c1aa-281">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4c1aa-283">Nell'elenco di applicazioni, selezionare **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-283">In the applications list, select **Marketo**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="4c1aa-285">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4c1aa-287">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-287">Click **Add** button.</span></span> <span data-ttu-id="4c1aa-288">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4c1aa-290">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c1aa-291">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c1aa-292">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c1aa-293">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c1aa-293">Testing single sign-on</span></span>

<span data-ttu-id="4c1aa-294">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c1aa-295">Quando si fa clic sul riquadro Marketo nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Marketo.</span><span class="sxs-lookup"><span data-stu-id="4c1aa-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c1aa-296">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4c1aa-296">Additional resources</span></span>

* [<span data-ttu-id="4c1aa-297">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c1aa-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c1aa-298">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c1aa-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

