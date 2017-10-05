---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cherwell | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Cherwell.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: 27fedb9caa1ef27693b2267df285d62aab78bc24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="32675-103">Esercitazione: Integrazione di Azure Active Directory con Cherwell</span><span class="sxs-lookup"><span data-stu-id="32675-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="32675-104">Questa esercitazione descrive come integrare Cherwell con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32675-104">In this tutorial, you learn how to integrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32675-105">L'integrazione di Cherwell con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32675-105">Integrating Cherwell with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32675-106">È possibile controllare in Azure AD chi può accedere a Cherwell</span><span class="sxs-lookup"><span data-stu-id="32675-106">You can control in Azure AD who has access to Cherwell</span></span>
- <span data-ttu-id="32675-107">È possibile abilitare gli utenti per l'accesso automatico a Cherwell (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="32675-107">You can enable your users to automatically get signed-on to Cherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32675-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32675-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32675-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32675-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32675-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32675-110">Prerequisites</span></span>

<span data-ttu-id="32675-111">Per configurare l'integrazione di Azure AD con Cherwell, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32675-111">To configure Azure AD integration with Cherwell, you need the following items:</span></span>

- <span data-ttu-id="32675-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32675-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32675-113">Sottoscrizione di Cherwell abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32675-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32675-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32675-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32675-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="32675-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32675-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="32675-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32675-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32675-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32675-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="32675-118">Scenario description</span></span>
<span data-ttu-id="32675-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="32675-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32675-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="32675-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32675-121">Aggiunta di Cherwell dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32675-121">Adding Cherwell from the gallery</span></span>
2. <span data-ttu-id="32675-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32675-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-the-gallery"></a><span data-ttu-id="32675-123">Aggiunta di Cherwell dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32675-123">Adding Cherwell from the gallery</span></span>
<span data-ttu-id="32675-124">Per configurare l'integrazione di Cherwell in Azure AD, è necessario aggiungere Cherwell dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="32675-124">To configure the integration of Cherwell into Azure AD, you need to add Cherwell from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32675-125">**Per aggiungere Cherwell dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32675-125">**To add Cherwell from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32675-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32675-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32675-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="32675-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32675-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32675-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="32675-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="32675-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="32675-133">Nella casella di ricerca digitare **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="32675-133">In the search box, type **Cherwell**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="32675-135">Nel pannello dei risultati selezionare **Cherwell** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32675-135">In the results panel, select **Cherwell**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32675-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32675-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32675-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cherwell usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32675-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32675-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Cherwell corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32675-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cherwell is to a user in Azure AD.</span></span> <span data-ttu-id="32675-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Cherwell.</span><span class="sxs-lookup"><span data-stu-id="32675-140">In other words, a link relationship between an Azure AD user and the related user in Cherwell needs to be established.</span></span>

<span data-ttu-id="32675-141">Per stabilire la relazione di collegamento, in Cherwell assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="32675-141">In Cherwell, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32675-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Cherwell, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="32675-142">To configure and test Azure AD single sign-on with Cherwell, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32675-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="32675-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32675-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32675-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32675-145">**[Creazione di un utente di test di Cherwell](#creating-a-cherwell-test-user)**: per avere una controparte di Britta Simon in Cherwell collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32675-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - to have a counterpart of Britta Simon in Cherwell that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32675-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32675-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32675-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="32675-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32675-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32675-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32675-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Cherwell.</span><span class="sxs-lookup"><span data-stu-id="32675-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="32675-150">**Per configurare l'accesso Single Sign-On di Azure AD con Cherwell, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32675-150">**To configure Azure AD single sign-on with Cherwell, perform the following steps:**</span></span>

1. <span data-ttu-id="32675-151">Nella pagina di integrazione dell'applicazione **Cherwell** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="32675-151">In the Azure portal, on the **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="32675-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="32675-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="32675-155">Nella sezione **URL e dominio Cherwell** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32675-155">On the **Cherwell Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="32675-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="32675-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32675-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="32675-158">This value is not real.</span></span> <span data-ttu-id="32675-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="32675-159">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="32675-160">Per ottenere questo valore, contattare il [team di supporto di Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="32675-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) to get this value.</span></span>
 
4. <span data-ttu-id="32675-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="32675-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="32675-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="32675-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32675-165">Nella sezione **Configurazione di Cherwell** fare clic su **Configura Cherwell** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="32675-165">On the **Cherwell Configuration** section, click **Configure Cherwell** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32675-166">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="32675-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="32675-168">Per configurare l'accesso Single Sign-On sul lato **Cherwell**, è necessario inviare il file **Certificato (Base64)** scaricato, l'**URL del servizio Single Sign-On SAML** e l'**ID di entità SAML** al [team di supporto di Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="32675-168">To configure single sign-on on **Cherwell** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="32675-169">Il team di supporto di Cherwell si occuperà dell'effettiva configurazione dell'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="32675-169">Your Cherwell support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="32675-170">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="32675-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="32675-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="32675-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32675-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="32675-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32675-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32675-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32675-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32675-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="32675-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32675-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="32675-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32675-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32675-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32675-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32675-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="32675-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32675-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="32675-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32675-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32675-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32675-186">a.</span><span class="sxs-lookup"><span data-stu-id="32675-186">a.</span></span> <span data-ttu-id="32675-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32675-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32675-188">b.</span><span class="sxs-lookup"><span data-stu-id="32675-188">b.</span></span> <span data-ttu-id="32675-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32675-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32675-190">c.</span><span class="sxs-lookup"><span data-stu-id="32675-190">c.</span></span> <span data-ttu-id="32675-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="32675-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32675-192">d.</span><span class="sxs-lookup"><span data-stu-id="32675-192">d.</span></span> <span data-ttu-id="32675-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32675-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="32675-194">Creazione di un utente di test di Cherwell</span><span class="sxs-lookup"><span data-stu-id="32675-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="32675-195">Per consentire agli utenti di Azure AD di accedere a Cherwell, è necessario effettuarne il provisioning in Cherwell.</span><span class="sxs-lookup"><span data-stu-id="32675-195">To enable Azure AD users to log in to Cherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="32675-196">Nel caso di Cherwell, gli account utente devono essere creati dal [team di supporto di Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="32675-196">In the case of Cherwell, the user accounts need to be created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="32675-197">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Cherwell per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32675-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32675-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32675-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32675-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Cherwell.</span><span class="sxs-lookup"><span data-stu-id="32675-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cherwell.</span></span>

![Assegna utente][200] 

<span data-ttu-id="32675-201">**Per assegnare Britta Simon a Cherwell, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32675-201">**To assign Britta Simon to Cherwell, perform the following steps:**</span></span>

1. <span data-ttu-id="32675-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32675-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="32675-204">Nell'elenco delle applicazioni selezionare **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="32675-204">In the applications list, select **Cherwell**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="32675-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="32675-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="32675-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="32675-208">Click **Add** button.</span></span> <span data-ttu-id="32675-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32675-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="32675-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="32675-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32675-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32675-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32675-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32675-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32675-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32675-214">Testing single sign-on</span></span>

<span data-ttu-id="32675-215">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="32675-215">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="32675-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32675-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32675-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="32675-217">Additional resources</span></span>

* [<span data-ttu-id="32675-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32675-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32675-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32675-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

