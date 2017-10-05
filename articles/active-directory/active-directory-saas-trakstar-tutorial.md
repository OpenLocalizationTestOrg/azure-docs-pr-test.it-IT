---
title: 'Esercitazione: Integrazione di Azure Active Directory con Trakstar | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Trakstar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 757429aa187e6536489b6636a0a11d122c7f9378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="8ca82-103">Esercitazione: Integrazione di Azure Active Directory con Trakstar</span><span class="sxs-lookup"><span data-stu-id="8ca82-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="8ca82-104">Questa esercitazione descrive come integrare Teamwork con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ca82-104">In this tutorial, you learn how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ca82-105">L'integrazione di Trakstar con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ca82-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ca82-106">È possibile controllare in Azure AD chi può accedere a Trakstar</span><span class="sxs-lookup"><span data-stu-id="8ca82-106">You can control in Azure AD who has access to Trakstar</span></span>
- <span data-ttu-id="8ca82-107">È possibile abilitare gli utenti per l'accesso automatico a Trakstar (Single Sign-On) con l'account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ca82-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca82-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8ca82-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ca82-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ca82-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8ca82-110">Prerequisites</span></span>

<span data-ttu-id="8ca82-111">Per configurare l'integrazione di Azure AD con Trakstar, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ca82-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

- <span data-ttu-id="8ca82-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ca82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ca82-113">Sottoscrizione di Trakstar abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ca82-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ca82-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8ca82-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ca82-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ca82-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ca82-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8ca82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ca82-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ca82-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ca82-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8ca82-118">Scenario description</span></span>
<span data-ttu-id="8ca82-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8ca82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ca82-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ca82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ca82-121">Aggiunta di Trakstar dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8ca82-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="8ca82-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="8ca82-123">Aggiunta di Trakstar dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8ca82-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="8ca82-124">Per configurare l'integrazione di Trakstar in Azure AD, è necessario aggiungere Trakstar dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8ca82-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ca82-125">**Per aggiungere Trakstar dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8ca82-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ca82-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8ca82-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ca82-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ca82-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8ca82-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ca82-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8ca82-133">Nella casella di ricerca digitare **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-133">In the search box, type **Trakstar**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="8ca82-135">Nel pannello dei risultati selezionare **Trakstar** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ca82-135">In the results panel, select **Trakstar**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ca82-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ca82-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Trakstar in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ca82-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ca82-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Trakstar che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ca82-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar is to a user in Azure AD.</span></span> <span data-ttu-id="8ca82-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-140">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>

<span data-ttu-id="8ca82-141">Per stabilire la relazione di collegamento, in Trakstar assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-141">In Trakstar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ca82-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Trakstar, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ca82-142">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ca82-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8ca82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ca82-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ca82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ca82-145">**[Creazione di un utente test di Trakstar](#creating-a-trakstar-test-user)**: per avere una controparte di Britta Simon in Trakstar collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ca82-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ca82-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ca82-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ca82-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8ca82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ca82-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ca82-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="8ca82-150">**Per configurare l'accesso Single Sign-On di Azure AD con Trakstar, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8ca82-150">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="8ca82-151">Nella pagina di integrazione dell'applicazione **Trakstar** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-151">In the Azure portal, on the **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8ca82-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8ca82-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="8ca82-155">Nella sezione **URL e dominio Trakstar** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8ca82-155">On the **Trakstar Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="8ca82-157">a.</span><span class="sxs-lookup"><span data-stu-id="8ca82-157">a.</span></span> <span data-ttu-id="8ca82-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`.</span><span class="sxs-lookup"><span data-stu-id="8ca82-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="8ca82-159">b.</span><span class="sxs-lookup"><span data-stu-id="8ca82-159">b.</span></span> <span data-ttu-id="8ca82-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="8ca82-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ca82-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8ca82-161">These values are not real.</span></span> <span data-ttu-id="8ca82-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="8ca82-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8ca82-163">Per ottenere questi valori, contattare il [team di supporto clienti di Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="8ca82-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) to get these values.</span></span> 
 
4. <span data-ttu-id="8ca82-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="8ca82-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="8ca82-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8ca82-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ca82-168">Nella sezione **Configurazione di Trakstar** fare clic su **Configura Trakstar** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-168">On the **Trakstar Configuration** section, click **Configure Trakstar** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8ca82-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8ca82-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="8ca82-171">Per configurare l'accesso Single Sign-On sul lato **Trakstar**, è necessario inviare il file di **Certificato (Base64)** scaricato, **l'URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="8ca82-171">To configure single sign-on on **Trakstar** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8ca82-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8ca82-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ca82-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8ca82-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ca82-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ca82-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ca82-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ca82-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca82-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8ca82-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ca82-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ca82-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8ca82-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ca82-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8ca82-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ca82-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ca82-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8ca82-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ca82-187">a.</span><span class="sxs-lookup"><span data-stu-id="8ca82-187">a.</span></span> <span data-ttu-id="8ca82-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ca82-189">b.</span><span class="sxs-lookup"><span data-stu-id="8ca82-189">b.</span></span> <span data-ttu-id="8ca82-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ca82-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ca82-191">c.</span><span class="sxs-lookup"><span data-stu-id="8ca82-191">c.</span></span> <span data-ttu-id="8ca82-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8ca82-193">d.</span><span class="sxs-lookup"><span data-stu-id="8ca82-193">d.</span></span> <span data-ttu-id="8ca82-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="8ca82-195">Creazione di un utente test di Trakstar</span><span class="sxs-lookup"><span data-stu-id="8ca82-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="8ca82-196">Questa sezione descrive come creare un utente chiamato Britta Simon in Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-196">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="8ca82-197">Collaborare con il [team di supporto di Trakstar](mailto:integrations@trakstar.com) per aggiungere utenti all'account Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) to add the users in the Trakstar account.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ca82-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca82-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ca82-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakstar.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8ca82-201">**Per assegnare Britta Simon a Trakstar, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8ca82-201">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="8ca82-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8ca82-204">Nell'elenco di applicazioni selezionare **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-204">In the applications list, select **Trakstar**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="8ca82-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8ca82-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8ca82-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-208">Click **Add** button.</span></span> <span data-ttu-id="8ca82-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8ca82-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8ca82-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ca82-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ca82-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ca82-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ca82-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ca82-214">Testing single sign-on</span></span>

<span data-ttu-id="8ca82-215">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ca82-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="8ca82-216">Quando si fa clic sul riquadro Trakstar nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione Trakstar.</span><span class="sxs-lookup"><span data-stu-id="8ca82-216">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8ca82-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8ca82-217">Additional resources</span></span>

* [<span data-ttu-id="8ca82-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ca82-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ca82-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ca82-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png

